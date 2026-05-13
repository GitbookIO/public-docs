---
icon: rotate-left
description: How to issue a refund, when funds reach the customer, and how it shows up on your books.
---

# Refunds

A refund returns funds to the original card or bank account the customer paid with. You can refund a payment in full or in part, as many times as you like up to the original amount, within your plan's refund window.

## Refund window by plan

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="info" icon="clock-rotate-left" %}
**You're on Starter** — you can refund a payment up to **60 days** after it was captured. After that, the only option is a manual ACH or wire from your own account.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "growth" %}

{% hint style="info" icon="clock-rotate-left" %}
**You're on Growth** — you can refund a payment up to **90 days** after it was captured. After that, the only option is a manual ACH or wire from your own account.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="success" icon="clock-rotate-left" %}
**You're on Enterprise** — you can refund a payment up to **180 days** after it was captured. Beyond that, your account team can arrange a one-off out-of-band refund.
{% endhint %}

{% endif %}

| Plan | Refund window |
| --- | --- |
| Starter | 60 days |
| Growth | 90 days |
| Enterprise | 180 days |

The window is measured from the **capture** date, not the original authorization. For two-step payments, that means the clock starts ticking when you capture, not when the customer paid.

## Issuing a refund

{% stepper %}
{% step %}

### Open the payment

Find the payment in **Payments → All payments** and click into it.

{% endstep %}

{% step %}

### Click "Refund"

You'll see a dialog with the maximum refundable amount, a free-text reason field, and an optional internal note.

{% endstep %}

{% step %}

### Pick full or partial

Refund the full amount, or enter a smaller amount. You can issue multiple partial refunds against the same payment until you've returned the full original amount.

{% endstep %}

{% step %}

### Confirm

The refund appears on the payment timeline immediately as **Pending**, then updates to **Succeeded** once it's accepted by the network — usually within a minute for cards, several days for ACH.

{% endstep %}
{% endstepper %}

The customer receives an email confirmation (configurable in **Settings → Receipts**), and a `refund.succeeded` webhook fires if you've subscribed to it.

## When the customer sees the money

Refund timing depends on the original payment method:

| Method | Time to customer's account |
| --- | --- |
| Card (Visa, Mastercard) | 5–10 business days |
| Card (Amex) | 5–10 business days |
| Card (Discover) | 5–10 business days |
| ACH debit | 5–7 business days |
| SEPA | 1–3 business days |
| Wire | Same day |

These are the issuer's posting times, not Evolve's processing times. Evolve initiates the refund within minutes; the lag is the customer's bank.

## How it shows up on your books

A refund appears on your settlement file as a `refund` row with a negative `net_amount`. Two important details for accounting:

<details>

<summary>The processing fee on the original payment is not returned</summary>

When you take a payment, Evolve charges the processing fee. When you refund it, the fee stays — you've already paid the network. The settlement file records this as the `fee` column being `0.00` on the refund row, but the original `fee` on the payment row remains. Net result: a refunded payment costs you the original processing fee in lost revenue.

</details>

<details>

<summary>Partial refunds are separate line items</summary>

Three partial refunds against one payment produce three `refund` rows on the settlement file, each with its own ID. The `source_id` column ties them all back to the original payment.

</details>

## Bulk refunds

For situations where you need to refund many payments at once — a recalled product, a service outage credit — you can issue refunds in bulk:

* **From the dashboard:** Filter to the payments you want to refund, click **Bulk action → Refund**, confirm.
* **From a CSV:** Upload a list of payment IDs and amounts under **Payments → Bulk refunds**.

Bulk refunds run in the background and you'll get an email when they complete. If any individual refund fails (typically because the payment is too old or already fully refunded), it's flagged on the result file and the rest still go through.

## Customer-initiated refund requests

Some teams expose a "Get a refund" flow to customers directly — most often through a customer portal or a help center. You can wire one up in two ways:

1. **Email-based** — a `mailto:` link routes the request to your support inbox; an agent issues the refund from the dashboard.
2. **Self-serve** — the customer requests a refund from your portal, your code calls the API, and the refund issues automatically.

Self-serve refunds are great for low-value, low-risk products. For higher-value items, route refunds through a human approval step — Evolve has no anti-fraud rules on refunds since they're considered low-risk by default.

## Related

* [Settlement files](settlement-files.md) — how refunds appear in your daily reconciliation.
* [Disputes and chargebacks](disputes.md) — what to do when a refund isn't enough and the customer disputes.
