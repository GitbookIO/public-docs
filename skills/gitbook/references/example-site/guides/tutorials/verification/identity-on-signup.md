---
icon: id-card
description: Add document + selfie verification to your sign-up flow without slowing down conversion.
---

# Add identity verification to sign-up

By the end of this tutorial you'll have a sign-up form that runs identity verification in the background, lets the customer continue using your product immediately, and gates higher-trust actions until verification completes. The build takes about 90 minutes.

This is the right pattern for any product where you need verified identity before high-value actions but don't want to lose customers at the front door.

{% hint style="info" %}
**Prerequisites.** A working sign-up flow in your app. Test API keys for Identity. Read [Identity verification](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/identity-verification) for the conceptual model.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Decide what's gated by verification

Two patterns most teams use:

* **Soft gate.** Customer can sign up and explore the product. Higher-value actions (withdraw funds, place a large order, post listings publicly) require verification.
* **Hard gate.** Customer can't reach the product without verification. Common for regulated verticals (finance, gambling, age-restricted goods).

Pick soft. It's better for conversion and you can always tighten later. The rest of this tutorial assumes soft.

{% endstep %}

{% step %}

### Create a verification session at sign-up

When the customer hits **Sign up**, your server creates an Identity verification session and stores the session ID on their user record:

{% tabs %}
{% tab title="Node" %}
```js
const customer = await evolve.customers.create({
  email: req.body.email,
  name: req.body.name,
});

const verification = await evolve.identity.verificationSessions.create({
  type: "identity",
  customer: customer.id,
  return_url: "https://yourapp.com/welcome",
});

await db.users.create({
  email: req.body.email,
  evolve_customer_id: customer.id,
  verification_session_id: verification.id,
  verification_status: "pending",
});

res.json({ verifyUrl: verification.url });
```
{% endtab %}

{% tab title="Python" %}
```python
customer = evolve.Customer.create(
    email=request.json["email"],
    name=request.json["name"],
)

verification = evolve.VerificationSession.create(
    type="identity",
    customer=customer.id,
    return_url="https://yourapp.com/welcome",
)

db.users.create(
    email=request.json["email"],
    evolve_customer_id=customer.id,
    verification_session_id=verification.id,
    verification_status="pending",
)

return jsonify(verifyUrl=verification.url)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Surface the verification step to the customer

The customer is in your product immediately. Show a banner or modal:

> Verify your identity to unlock [the high-trust actions]. Takes about a minute.

Link the banner to `verification.url`. Customers who click through complete the verification on Evolve's hosted flow. They come back to `return_url` when done.

You can dismiss the banner per-session (the customer might be on mobile and want to do it later), but keep it visible until verification completes.

{% endstep %}

{% step %}

### Listen for the webhook

Subscribe to the four verification-session events:

* `verification_session.verified` — update the user's status, unlock features.
* `verification_session.failed` — show the customer a retry path or escalate to support.
* `verification_session.manual_review` — leave the user in the "verifying" state; manual review usually resolves within an hour.
* `verification_session.expired` — the customer didn't complete in 24 hours; offer them a fresh link.

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "verification_session.verified") {
  await db.users.update(
    { verification_session_id: event.data.object.id },
    { verification_status: "verified" }
  );
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "verification_session.verified":
    db.users.update_where(
        verification_session_id=event.data.object.id,
        values={"verification_status": "verified"},
    )
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Gate the high-trust action

In your product, before letting the user perform a gated action, check their verification status:

```js
if (user.verification_status !== "verified") {
  return showVerificationRequiredModal();
}
```

The modal should re-link to the verification URL (or generate a fresh one if expired) and explain why the action requires verification. Customers who understand the *why* abandon less.

{% endstep %}

{% step %}

### Test the failure paths

In test mode, use these fixtures to test each path:

| Document fixture | Result |
| --- | --- |
| `test-dl-front.jpg` | Verified |
| `test-dl-expired.jpg` | Failed — `document_expired` |
| `test-dl-tampered.jpg` | Failed — `document_tampered` |
| `test-dl-unrecognized.jpg` | Manual review |

Walk through each one. Confirm your UI handles all four end-states correctly (success, retry, manual review, expired).

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Customers complete verification but our DB doesn't update"</summary>

Webhook handler bug almost always — most often forgetting to `await` the DB update or returning a non-2xx response. If your webhook returns anything other than 2xx, Evolve retries up to 10 times over 3 days, which can produce duplicate updates if the original eventually succeeded.

</details>

<details>

<summary>"Customers say the camera flow is broken on Safari"</summary>

iOS Safari requires HTTPS for camera access (no `http://` or `localhost` over an unsecured network). If you're testing locally, either tunnel via ngrok or use the dashboard's QR-code share feature to test on a phone connected to a real domain.

</details>

<details>

<summary>"How do I show the customer's verified name and DOB in our UI?"</summary>

After verification succeeds, retrieve the session and read the extracted fields. They're not on the webhook payload by default (privacy default). Show them in your UI with care — accidentally surfacing PII to other users is a leakage class our customers ask about most.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rotate-right" style="color:$primary;">:rotate-right:</i></h3></td><td><strong>Re-verification trigger</strong></td><td>When and how to re-run verification later.</td><td><a href="re-verification-trigger.md">re-verification-trigger.md</a></td></tr><tr><td><h3><i class="fa-building-columns" style="color:$primary;">:building-columns:</i></h3></td><td><strong>Bank verification with Plaid</strong></td><td>The "I'll take ACH from this customer" recipe.</td><td><a href="plaid-bank-verification.md">plaid-bank-verification.md</a></td></tr><tr><td><h3><i class="fa-briefcase" style="color:$primary;">:briefcase:</i></h3></td><td><strong>Verify a business (KYB)</strong></td><td>The same flow but for company customers.</td><td><a href="kyb.md">kyb.md</a></td></tr></tbody></table>
