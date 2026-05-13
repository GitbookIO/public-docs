---
icon: rotate-right
description: Re-verify customers when something changes — chargebacks, large transactions, or address updates.
---

# Build a re-verification trigger

By the end of this tutorial you'll have a re-verification system that automatically triggers a fresh identity check on signals that warrant it — first chargeback, transaction over a threshold, or an address change — without disrupting the customer's day-to-day experience. The build takes about 90 minutes.

This is the right pattern for any team that needs to keep verification fresh past the initial onboarding — high-value commerce, regulated verticals, marketplaces.

{% hint style="info" %}
**Prerequisites.** [Identity verification on sign-up](identity-on-signup.md) finished. A working webhook handler. A way to send transactional emails to customers.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Pick your re-verification triggers

Three common ones, ranked by ROI:

* **First chargeback.** A customer's first dispute is the strongest fraud signal you'll get. Re-verify on it.
* **Transaction over threshold.** Pick an amount that reflects your average ticket size — usually 5x to 10x. Re-verify when a customer crosses it.
* **Material profile change.** Address change to a different country, phone number change, or email change. Re-verify on these.

For most teams, all three together produce a manageable volume of re-verifications without irritating customers.

{% endstep %}

{% step %}

### Subscribe to the trigger events

Add these webhook subscriptions:

* `charge.disputed` — for the first-chargeback trigger.
* `charge.succeeded` — for the threshold trigger (filter on amount).
* `customer.updated` — for the profile-change trigger.

{% endstep %}

{% step %}

### Implement the trigger logic

In your webhook handler:

{% tabs %}
{% tab title="Node" %}
```js
async function handleEvent(event) {
  const customerId = event.data.object.customer;
  const customer = await db.users.findOne({ evolve_customer_id: customerId });
  if (!customer) return;

  let shouldReverify = false;

  if (event.type === "charge.disputed") {
    if (customer.disputes_count === 0) shouldReverify = true;
    await db.users.update(customerId, { disputes_count: customer.disputes_count + 1 });
  }

  if (event.type === "charge.succeeded") {
    if (event.data.object.amount > 100_000) shouldReverify = true; // $1,000
  }

  if (event.type === "customer.updated") {
    const oldCountry = customer.address?.country;
    const newCountry = event.data.object.address?.country;
    if (oldCountry && newCountry && oldCountry !== newCountry) {
      shouldReverify = true;
    }
  }

  if (shouldReverify && !customer.reverification_pending) {
    await triggerReverification(customer);
  }
}
```
{% endtab %}

{% tab title="Python" %}
```python
def handle_event(event):
    customer_id = event.data.object.customer
    customer = db.users.find_by_evolve_id(customer_id)
    if not customer:
        return

    should_reverify = False

    if event.type == "charge.disputed":
        if customer.disputes_count == 0:
            should_reverify = True
        db.users.update(customer_id, disputes_count=customer.disputes_count + 1)

    if event.type == "charge.succeeded":
        if event.data.object.amount > 100_000:
            should_reverify = True

    if event.type == "customer.updated":
        old_country = (customer.address or {}).get("country")
        new_country = (event.data.object.address or {}).get("country")
        if old_country and new_country and old_country != new_country:
            should_reverify = True

    if should_reverify and not customer.reverification_pending:
        trigger_reverification(customer)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Trigger the re-verification

Create a fresh verification session and email the customer with the link:

{% tabs %}
{% tab title="Node" %}
```js
async function triggerReverification(customer) {
  const session = await evolve.identity.verificationSessions.create({
    type: "identity",
    customer: customer.evolve_customer_id,
    return_url: `https://yourapp.com/reverified?session={CHECKOUT_SESSION_ID}`,
    metadata: { reason: "scheduled_reverification" },
  });

  await db.users.update(customer.id, {
    reverification_pending: true,
    reverification_session_id: session.id,
  });

  await sendEmail(customer.email, "reverification_required", {
    verifyUrl: session.url,
  });
}
```
{% endtab %}

{% tab title="Python" %}
```python
def trigger_reverification(customer):
    session = evolve.VerificationSession.create(
        type="identity",
        customer=customer.evolve_customer_id,
        return_url="https://yourapp.com/reverified",
        metadata={"reason": "scheduled_reverification"},
    )

    db.users.update(
        customer.id,
        reverification_pending=True,
        reverification_session_id=session.id,
    )

    send_email(customer.email, "reverification_required",
               {"verifyUrl": session.url})
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Decide what to gate during re-verification

For most teams, the right policy is: customer can keep using the product for low-value actions, but high-value actions (large transactions, withdrawals) are paused until re-verification completes.

{% tabs %}
{% tab title="Node" %}
```js
function canPerformHighValueAction(user) {
  if (user.verification_status !== "verified") return false;
  if (user.reverification_pending) return false;
  return true;
}
```
{% endtab %}

{% tab title="Python" %}
```python
def can_perform_high_value_action(user):
    return user.verification_status == "verified" and not user.reverification_pending
```
{% endtab %}
{% endtabs %}

The gate should explain *why* — customers who don't understand abandon at 3x the rate.

{% endstep %}

{% step %}

### Handle the re-verification result

When re-verification succeeds:

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "verification_session.verified") {
  await db.users.update(
    { reverification_session_id: event.data.object.id },
    { reverification_pending: false, last_verified_at: new Date() }
  );
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "verification_session.verified":
    db.users.update_where(
        reverification_session_id=event.data.object.id,
        values={"reverification_pending": False, "last_verified_at": datetime.utcnow()},
    )
```
{% endtab %}
{% endtabs %}

If it fails, escalate — the customer's identity has potentially changed since first verification. Most teams send these to manual review for a human to assess.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Customers complain about being asked to verify again"</summary>

Most-cited cause is that the email and the gate don't explain why. The wording that works:

> We re-verify customers periodically to keep your account secure and meet our compliance obligations. Verification takes about a minute and only happens [reason].

Customers who understand it's about their security (not yours) abandon less.

</details>

<details>

<summary>"Re-verifications stack up — the same customer gets multiple"</summary>

Always check `reverification_pending` before triggering. If multiple events fire in a short window, one re-verification covers all of them.

</details>

<details>

<summary>"What about customers I want to verify on a fixed schedule?"</summary>

For regulatory regimes that mandate periodic re-verification (some KYC programs require every 12 months for high-risk customers), use the **scheduled re-verification** feature in the dashboard rather than building it yourself. Settings → Identity → Re-verification schedule.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-id-card" style="color:$primary;">:id-card:</i></h3></td><td><strong>Identity verification on sign-up</strong></td><td>The first verification this is a follow-up to.</td><td><a href="identity-on-signup.md">identity-on-signup.md</a></td></tr><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Prevent chargebacks</strong></td><td>Re-verification is one of many chargeback levers.</td><td><a href="../payment-flows/chargeback-prevention.md">chargeback-prevention.md</a></td></tr><tr><td><h3><i class="fa-briefcase" style="color:$primary;">:briefcase:</i></h3></td><td><strong>Verify a business (KYB)</strong></td><td>The business-side equivalent.</td><td><a href="kyb.md">kyb.md</a></td></tr></tbody></table>
