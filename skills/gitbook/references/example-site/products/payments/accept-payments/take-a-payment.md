---
icon: circle-dollar-to-slot
description: The four ways to accept a payment, and which one is right for your situation.
---

# Take a payment

Evolve gives you four channels to accept payments. They share the same backend — the same fees, the same settlement, the same dashboard. The differences are in how much engineering work the integration needs and how much control you have over the customer experience.

## Pick a channel

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-link" style="color:$primary;">:link:</i></h3></td><td><strong>Payment links</strong></td><td>One URL per payment or product. No code at all.</td><td></td></tr><tr><td><h3><i class="fa-window-maximize" style="color:$primary;">:window-maximize:</i></h3></td><td><strong>Hosted Checkout</strong></td><td>Redirect to an Evolve-hosted checkout page. ~10 lines of code.</td><td></td></tr><tr><td><h3><i class="fa-puzzle-piece" style="color:$primary;">:puzzle-piece:</i></h3></td><td><strong>Embedded Elements</strong></td><td>Drop-in card and bank fields in your own page. Custom UI.</td><td></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>Direct API</strong></td><td>Full control. PCI scope is your responsibility.</td><td><a href="https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api">README.md</a></td></tr></tbody></table>

## When to use which

| Channel | Best for | Effort | Customization |
| --- | --- | --- | --- |
| **Payment links** | One-off invoices, social-media sales, pre-orders, donations | None | Logo and colors |
| **Hosted Checkout** | E-commerce checkouts, SaaS sign-ups, marketplaces | Low | Theme + custom fields |
| **Embedded Elements** | Branded checkout flows where the URL must stay yours | Medium | Full UI control around our fields |
| **Direct API** | Mobile apps, custom POS, complex marketplaces | High | Total |

{% if visitor.claims.unsigned.persona === "prospect" %}

{% hint style="info" icon="store" %}
**Selling on Shopify or another commerce platform?** You won't need any of these directly — install [Evolve for Shopify](https://app.gitbook.com/s/MBT3EDUK7DzXmR0k9cje/shopify) and the platform handles the channel choice for you.
{% endhint %}

{% endif %}

## Walkthrough: payment links

The lowest-friction option, and the one most teams use to test Evolve before committing to a deeper integration.

{% stepper %}
{% step %}

### Create the link

In **Payments → Payment links**, click **New link**. Set an amount, a description, and (optionally) a redirect URL for after payment. Click **Create**.

{% endstep %}

{% step %}

### Share it

Copy the link or download a QR code. Send it by email, paste it into a message, or embed it on your site.

{% endstep %}

{% step %}

### Watch it complete

When the customer pays, the new payment appears in **All payments** and (if you set one) the redirect URL fires.

{% endstep %}
{% endstepper %}

## Walkthrough: hosted Checkout

A redirect-based checkout you trigger from your site. You create a Checkout session on your server, redirect the customer, and Evolve sends them back when they're done.

For the integration steps, see the [Hosted Checkout guide](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api/checkout).

## Walkthrough: embedded Elements

Drop-in card and bank-account fields you can place inside your own page. The fields render in an iframe so the card data never touches your server — your PCI scope stays at SAQ A.

For the integration steps, see the [Elements guide](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api/elements).

## What happens after a payment

The lifecycle is the same regardless of which channel you used:

{% columns %}
{% column width="60%" %}

* The payment appears in **All payments** within seconds.
* Funds are added to your balance and included in the next [settlement](../reconciliation/settlement-files.md).
* If you've added webhook endpoints, a `payment.succeeded` event fires.
* The customer receives an email receipt (configurable in **Settings → Receipts**).

{% endcolumn %}

{% column %}

<a href="../concepts/payment-lifecycle.md" class="button secondary">See the full lifecycle</a>

{% endcolumn %}
{% endcolumns %}
