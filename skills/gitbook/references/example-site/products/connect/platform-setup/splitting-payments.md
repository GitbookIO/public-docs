---
icon: percent
description: Application fees, flat fees, and conditional rules — how every payment gets split between platform and seller.
---

# Splitting payments

Every Connect payment gets split between you and the seller. The default split is a percentage of the gross amount as your **application fee**, with the remainder transferred to the seller's connected-account balance. Most platforms start with a flat percentage — <code class="expression">space.vars.default_application_fee_pct</code>% is the default — and add complexity over time.

This page covers what you can configure and how to think about it.

## Three components of a split

A single payment can have up to three platform-side line items:

{% columns %}
{% column width="33%" %}

### <i class="fa-percent" style="color:$primary;">:percent:</i> Application fee

A percentage of the gross amount. The most common revenue model for platforms.

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-dollar-sign" style="color:$primary;">:dollar-sign:</i> Flat fee

A fixed amount per transaction. Useful for covering processing costs.

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-coins" style="color:$primary;">:coins:</i> Pass-through fee

Where the seller pays the processing fee. Less common but supported.

{% endcolumn %}
{% endcolumns %}

The combination is fully flexible — you can have all three on a single payment, or just one, or none (rare but possible for promotional payments).

## A simple example

A buyer pays $100 on a marketplace where the platform charges a 5% application fee plus a $0.50 flat fee:

| Line item | Amount |
| --- | --- |
| Buyer's card charged | $100.00 |
| Card processing fee (Evolve) | -$2.90 |
| Application fee (platform) | -$5.00 |
| Flat fee (platform) | -$0.50 |
| Net to seller | $91.60 |

The platform's balance goes up by $5.50 ($5.00 + $0.50). The seller's balance goes up by $91.60. The processing fee is netted from the platform's side by default — but you can configure it to net from the seller's side instead (see [Pass-through fees](#pass-through-fees) below).

## Where you configure the split

Two places, depending on whether the split is per-payment or platform-wide.

### Platform default

In **Connect → Settings → Default split**, set the platform-wide default:

* Application fee percentage — applies to all charges unless overridden per-session.
* Flat fee amount — applies on top of the percentage.
* Currency-specific overrides — different rates per currency.

This default is what gets used on every payment unless you specify otherwise at session creation.

### Per-payment override

When you create a [checkout session](../embedded-checkout/hosted-vs-embedded.md), you can override the split:

```http
POST /v1/checkout_sessions
{
  "amount": 10000,
  "currency": "usd",
  "connected_account": "acct_3KsM12pL9q",
  "application_fee_amount": 700,
  "application_fee_currency": "usd"
}
```

This is the right place to put rules that depend on the specific transaction — different rates per product category, promotional discounts, deal-specific contracts.

## Conditional rules

Most platforms outgrow flat percentages. Common rules platforms add:

| Rule | Example |
| --- | --- |
| **By seller tier** | Top sellers pay 3%, standard sellers pay 5%, new sellers pay 7% during their first 90 days. |
| **By product category** | Digital goods 8%, physical goods 5%, services 12%. |
| **By transaction size** | 5% under $1,000; 3% from $1,000 to $10,000; 1.5% above $10,000. |
| **By currency** | 4% USD, 4.5% EUR, 5% other (covering FX margin). |
| **By time** | Black Friday promo — 0% application fee on a single weekend. |

You build these rules in your own code at session creation — Evolve doesn't have a built-in rules engine, since the right rules tend to be specific to the platform's business model. The rules are simple enough that platforms typically encode them as a function in their checkout-session-creation path.

## Pass-through fees

By default, the **card processing fee** (the 2.9% + $0.30 from the [Payments fee structure](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/fees-and-pricing)) comes off the platform's application fee. That means if you charge a 5% application fee on a $100 payment:

* Buyer pays $100.
* Seller gets $95.
* Platform gets $5 - $2.90 = $2.10. *(Processing comes off your side.)*

You can flip this so the seller absorbs the processing fee instead — `application_fee_includes_processing: false` on the session:

* Buyer pays $100.
* Seller gets $95 - $2.90 = $92.10. *(Processing comes off the seller's side.)*
* Platform gets $5.00.

Marketplaces that compete on take-rate often pass processing through to sellers; platforms that compete on seller experience usually absorb it.

## Refunds and the split

When a payment is refunded, the application fee is refunded **proportionally** by default. A full refund takes back the platform's full application fee; a partial refund takes back a proportional amount.

You can override this — for example, keep the application fee on a refund (the seller is bearing the full refund cost) — by specifying `refund_application_fee: false` on the refund. See [Refunds and disputes](refunds-and-disputes.md).

## What appears in reporting

Application fees show up in three places:

* **Per-payment**, on the charge timeline.
* **Per-seller**, on the seller's revenue summary.
* **Platform-wide**, in the application-fees report (your platform's revenue line).

The application-fees report is the most-watched dashboard for most Connect platforms — it's the daily revenue chart your CFO checks.

## Related

* [Onboarding sellers](onboarding-sellers.md) — set per-seller defaults during onboarding.
* [Payouts to sellers](payouts.md) — how the seller's balance becomes their payout.
* [Refunds and disputes](refunds-and-disputes.md) — what happens to the split when a payment reverses.
* [Fees and pricing (Payments)](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/fees-and-pricing) — the underlying processing fees.
