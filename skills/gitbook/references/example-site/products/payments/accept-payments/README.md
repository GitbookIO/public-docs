---
description: Charges, saved methods, 3-D Secure, smart routing, and failover.
icon: bolt
---

# Accept payments

This is the practical core of Evolve Payments — how to take money from a customer, what happens behind the scenes, and which controls you can turn on as your needs grow.

## Start here

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-circle-dollar-to-slot" style="color:$primary;">:circle-dollar-to-slot:</i></h3></td><td><strong>Take a payment</strong></td><td>The four channels for accepting money.</td><td><a href="take-a-payment.md">take-a-payment.md</a></td></tr><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><strong>Saved payment methods</strong></td><td>Charge the same customer again later.</td><td><a href="saved-payment-methods.md">saved-payment-methods.md</a></td></tr><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>3-D Secure and SCA</strong></td><td>Liability shift and the EU rules.</td><td><a href="3d-secure.md">3d-secure.md</a></td></tr></tbody></table>

## Optimize

Once your basic flow is in production, these controls help you push the approval rate up.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-route" style="color:$primary;">:route:</i></h3></td><td><strong>Smart routing</strong></td><td>Pick the route most likely to approve. <em>Growth+</em></td><td><a href="smart-routing.md">smart-routing.md</a></td></tr><tr><td><h3><i class="fa-arrows-spin" style="color:$primary;">:arrows-spin:</i></h3></td><td><strong>Failover and retries</strong></td><td>Re-route around acquirer outages. <em>Enterprise</em></td><td><a href="failover.md">failover.md</a></td></tr></tbody></table>

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="info" icon="arrow-up-right-from-square" %}
**Smart routing and failover are Growth and Enterprise features.** They're listed here so you can plan for them — see [pricing](https://gitbook.com) when you're ready to upgrade.
{% endhint %}

{% endif %}

## How a payment moves

Whether the payment is taken via a hosted link, embedded Checkout, or a custom integration, the same five things happen behind the scenes:

{% stepper %}
{% step %}

### Customer confirms

The customer enters card details on the hosted checkout, embedded Element, or your own form, then taps **Pay**.

{% endstep %}

{% step %}

### Evolve picks a route

If [smart routing](smart-routing.md) is on, Evolve picks the acquirer most likely to approve this card on this network. Otherwise the default acquirer is used.

{% endstep %}

{% step %}

### Network and issuer respond

The chosen acquirer sends the authorization to the card network. The issuer approves or declines, usually within a second.

{% endstep %}

{% step %}

### Capture happens

For one-step payments (the default), capture happens immediately. For two-step, you capture later from the dashboard or your code. See [Payment lifecycle](../concepts/payment-lifecycle.md).

{% endstep %}

{% step %}

### Funds land on your balance

The payment shows up as **Captured** on your dashboard within seconds, and is counted toward the next [settlement](../reconciliation/settlement-files.md). Anyone subscribed to webhooks gets a `payment.succeeded` event at this point.

{% endstep %}
{% endstepper %}

## Related

* [Payment lifecycle](../concepts/payment-lifecycle.md) — every state a charge can be in.
* [Errors and retries](../concepts/errors-and-retries.md) — what to do when a charge fails.
* [Webhooks](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks) — events emitted by every charge.
