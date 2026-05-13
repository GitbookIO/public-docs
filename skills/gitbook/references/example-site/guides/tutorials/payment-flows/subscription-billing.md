---
icon: arrows-rotate
description: Build recurring billing — mandates, automatic retries, dunning emails, and cancellation.
---

# Build a subscription billing system

By the end of this tutorial you'll have a subscription system that signs customers up, charges them on a schedule, retries failed payments, and emails them before card expiry. The build takes about 90 minutes.

This is for SaaS products, membership sites, and anything else where you charge the same customer on a cadence.

{% hint style="info" %}
**Prerequisites.** You've completed [Accept a one-time payment](accept-one-time-payment.md). You'll reuse the Checkout session and webhook setup from there. A test API key with subscription support enabled (it is on Growth and Enterprise; on Starter you'll see an upsell prompt).
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Define a subscription plan in the dashboard

In **Subscriptions → Plans**, create a plan: name, currency, amount, interval (`month` or `year`), and trial length if any. Plans are reusable across customers — most teams have 3–5 plans, not one per customer.

{% endstep %}

{% step %}

### Create a Checkout session in subscription mode

When the customer signs up, create a Checkout session with `mode: "subscription"` and the plan ID:

{% tabs %}
{% tab title="Node" %}
```js
const session = await evolve.checkoutSessions.create({
  mode: "subscription",
  plan: "plan_pro_monthly",
  customer_email: req.body.email,
  success_url: "https://yourapp.com/welcome?session={CHECKOUT_SESSION_ID}",
  cancel_url: "https://yourapp.com/pricing",
});
```
{% endtab %}

{% tab title="Python" %}
```python
session = evolve.CheckoutSession.create(
    mode="subscription",
    plan="plan_pro_monthly",
    customer_email=request.json["email"],
    success_url="https://yourapp.com/welcome?session={CHECKOUT_SESSION_ID}",
    cancel_url="https://yourapp.com/pricing",
)
```
{% endtab %}
{% endtabs %}

The customer enters card details once. Evolve creates a **mandate** (their consent to recurring charges) and saves the card.

{% endstep %}

{% step %}

### Handle the subscription webhook events

Subscribe to four events on your webhook endpoint:

* `subscription.created` — first charge succeeded; provision access.
* `subscription.invoice_paid` — recurring charge succeeded; nothing to do.
* `subscription.invoice_failed` — charge failed; we'll retry. See next step.
* `subscription.canceled` — customer or you canceled; revoke access.

{% endstep %}

{% step %}

### Configure retry behavior

In **Subscriptions → Retry policy**, set the retry schedule for failed charges. The default is sensible — retry 3 times over 7 days, then cancel. Custom-tune if your cohort has known seasonal cash-flow patterns.

For each retry attempt, Evolve sends a `subscription.invoice_failed` event. You can email the customer with a "update your card" link that opens a Customer Portal session.

{% endstep %}

{% step %}

### Build a Customer Portal link

Don't build your own card-update UI. Use the hosted Customer Portal:

{% tabs %}
{% tab title="Node" %}
```js
app.post("/portal", async (req, res) => {
  const session = await evolve.customerPortalSessions.create({
    customer: req.user.evolveCustomerId,
    return_url: "https://yourapp.com/account",
  });
  res.redirect(session.url);
});
```
{% endtab %}

{% tab title="Python" %}
```python
@app.post("/portal")
def portal():
    session = evolve.CustomerPortalSession.create(
        customer=current_user.evolve_customer_id,
        return_url="https://yourapp.com/account",
    )
    return redirect(session.url)
```
{% endtab %}
{% endtabs %}

The customer can update their card, change plans, view invoices, and cancel — all without you writing the UI.

{% endstep %}

{% step %}

### Test the lifecycle

In test mode, use the timer feature in **Subscriptions → Test clock** to fast-forward through a year of billing in five minutes. Watch invoices generate, see a retry succeed, see a cancellation flow.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Customers don't know they signed up for recurring billing"</summary>

Show the recurring amount and cadence on your sign-up form, on the Checkout, and on the receipt. The card networks require this for mandate validity, and a clearly-disclosed mandate dramatically lowers your dispute rate.

</details>

<details>

<summary>"Retries fire while the customer is already updating their card"</summary>

When you receive `subscription.invoice_failed`, send the customer to the Customer Portal and pause retries for 24 hours via `evolve.subscriptions.pauseRetries(id)`. The customer updates their card, the subscription un-pauses, and the next attempt uses the new card.

</details>

<details>

<summary>"Account updater missed a re-issued card"</summary>

Account updater works for most major US issuers but isn't 100%. For high-value subscriptions, also email customers 30 days before card expiry asking them to update — see the **Subscriptions → Email templates** for the pre-built one.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><strong>Save cards for repeat customers</strong></td><td>The mandate model under the hood.</td><td><a href="save-cards.md">save-cards.md</a></td></tr><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>3-D Secure</strong></td><td>When required even on subscriptions.</td><td><a href="3d-secure.md">3d-secure.md</a></td></tr><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Prevent chargebacks</strong></td><td>Most subscription disputes are preventable.</td><td><a href="chargeback-prevention.md">chargeback-prevention.md</a></td></tr></tbody></table>
