---
icon: bookmark
description: Save customer cards for one-tap checkout, recurring billing, or unscheduled re-charges.
---

# Save cards for repeat customers

By the end of this tutorial you'll have a flow that saves a customer's card on first checkout, charges it again later without re-prompting, and handles card expiry through account updater. The build takes about 60 minutes.

This is the foundation for subscriptions, repeat-purchase flows, marketplaces, and "buy with one tap" UX.

{% hint style="info" %}
**Prerequisites.** [Accept a one-time payment](accept-one-time-payment.md) finished. Familiarity with the [Saved payment methods](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/accept-payments/saved-payment-methods) concept page helps.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Capture customer consent at first checkout

Show a checkbox or clear text on your checkout — "Save this card for future purchases" — that the customer must opt into. The card networks require explicit consent at the time of first payment.

For a typical e-commerce flow, the wording is something like:

> ☐ Save my card for next time

For a subscription flow, the wording is more directly mandate-like:

> By clicking Subscribe, I authorize Acme Corp to charge my card $19/month until I cancel.

{% endstep %}

{% step %}

### Pass `setup_future_usage` on the Checkout session

When the customer checks the consent box, set `setup_future_usage` on the session you create:

{% tabs %}
{% tab title="Node" %}
```js
const session = await evolve.checkoutSessions.create({
  amount: 4200,
  currency: "usd",
  customer_email: req.body.email,
  setup_future_usage: req.body.saveCard ? "off_session" : null,
  success_url: "...",
  cancel_url: "...",
});
```
{% endtab %}

{% tab title="Python" %}
```python
session = evolve.CheckoutSession.create(
    amount=4200,
    currency="usd",
    customer_email=request.json["email"],
    setup_future_usage="off_session" if request.json["save_card"] else None,
    success_url="...",
    cancel_url="...",
)
```
{% endtab %}
{% endtabs %}

`off_session` means you intend to charge the customer when they're not actively present (subscriptions, automatic re-orders). Use `on_session` for one-tap checkouts where the customer is on your site.

{% endstep %}

{% step %}

### Find the customer's saved methods

After the first successful payment, the saved card is attached to the customer record. List it on the customer:

{% tabs %}
{% tab title="Node" %}
```js
const methods = await evolve.paymentMethods.list({
  customer: "cus_4n2P3qR5sT6uV",
  type: "card",
});

console.log(methods.data[0].card.last4); // e.g. "4242"
```
{% endtab %}

{% tab title="Python" %}
```python
methods = evolve.PaymentMethod.list(
    customer="cus_4n2P3qR5sT6uV",
    type="card",
)
print(methods.data[0].card.last4)
```
{% endtab %}
{% endtabs %}

Display this on your customer's profile or order page as "Visa ending in 4242".

{% endstep %}

{% step %}

### Charge the saved method

For a follow-on charge, reference the customer and the saved method:

{% tabs %}
{% tab title="Node" %}
```js
const charge = await evolve.charges.create({
  amount: 1500,
  currency: "usd",
  customer: "cus_4n2P3qR5sT6uV",
  payment_method: "pm_3K2pL9qXa7",
  off_session: true,
  description: "Tipping for order #1042",
});
```
{% endtab %}

{% tab title="Python" %}
```python
charge = evolve.Charge.create(
    amount=1500,
    currency="usd",
    customer="cus_4n2P3qR5sT6uV",
    payment_method="pm_3K2pL9qXa7",
    off_session=True,
    description="Tipping for order #1042",
)
```
{% endtab %}
{% endtabs %}

`off_session: true` tells the issuer the customer isn't physically present, which matters for the SCA exemption decision.

{% endstep %}

{% step %}

### Turn on account updater

Cards expire. To minimize involuntary churn, enable account updater in **Settings → Cards → Account updater**. When the customer's bank reissues their card, the updated details are pulled in automatically — usually a week or two before the old expiry.

This is on by default for Growth and Enterprise. On Starter you have to enable it explicitly.

{% endstep %}

{% step %}

### Email customers before card expiry

Account updater isn't 100%. Belt-and-braces: email customers 30 days before card expiry asking them to update. Use the dashboard's pre-built template under **Customers → Email templates → Card expiry**.

The template links to your Customer Portal where they can update without you writing UI.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"My recurring charges keep failing with `authentication_required`"</summary>

Without a mandate, the issuer treats every recurring charge as a fresh customer-initiated transaction and may demand SCA. Make sure you're recording the mandate at first checkout (the `setup_future_usage` flag handles this when the consent UI is correctly worded).

</details>

<details>

<summary>"I want to charge a saved card from a different brand than the original"</summary>

You can't — the saved method is tied to the original card. If a customer wants to switch from Visa to Amex, they re-enter the new card via Customer Portal. The old card stays on file unless they remove it.

</details>

<details>

<summary>"Customers complain they can't see what cards I have on file"</summary>

Show the saved methods on the customer's profile and on every receipt. Customers who don't know what's saved sometimes "lose" cards and start their bank's chargeback flow when they see an unfamiliar charge.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-arrows-rotate" style="color:$primary;">:arrows-rotate:</i></h3></td><td><strong>Subscription billing</strong></td><td>Saved methods + a recurring schedule.</td><td><a href="subscription-billing.md">subscription-billing.md</a></td></tr><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>3-D Secure</strong></td><td>How saved-method MIT exemptions work.</td><td><a href="3d-secure.md">3d-secure.md</a></td></tr><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Prevent chargebacks</strong></td><td>Stop "lost card" disputes before they start.</td><td><a href="chargeback-prevention.md">chargeback-prevention.md</a></td></tr></tbody></table>
