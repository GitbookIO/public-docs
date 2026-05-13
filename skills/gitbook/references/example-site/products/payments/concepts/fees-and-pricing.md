---
icon: receipt
description: What each plan costs, what's included, and how fees show up in your settlements.
---

# Fees and pricing

Evolve's pricing has three components: a per-transaction fee, a small set of feature add-ons, and an optional same-day payout fee. There are no monthly minimums, no setup fees, and no card-network surcharges — what's listed here is what you pay.

{% if visitor.claims.unsigned.plan %}
## Your plan
{% endif %}

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="info" icon="layer-group" %}
**You're on Starter.** Card payments, USD only, T+3 payouts. Volume cap is **$50,000/month** — you'll get an email when you cross 80%, and we'll automatically suggest a Growth upgrade.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "growth" %}

{% hint style="info" icon="layer-group" %}
**You're on Growth.** Cards, ACH, debit, and four-currency support. T+2 payouts. Volume cap is **$1,000,000/month**.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="success" icon="layer-group" %}
**You're on Enterprise.** Custom pricing, all rails, all currencies, T+1 default with same-day available. Volume is uncapped.
{% endhint %}

{% endif %}

## Plan comparison

| | Starter | Growth | Enterprise |
| --- | --- | --- | --- |
| **Card (domestic)** | 2.9% + $0.30 | 2.7% + $0.30 | Custom (interchange-plus) |
| **Card (international)** | +1.5% | +1.0% | Custom |
| **ACH debit** | — | 0.8%, capped at $5 | Custom |
| **Wire transfer** | — | — | $20 flat |
| **SEPA / BACS** | — | — | Custom |
| **Currency conversion** | — | Wholesale + 0.5% | Wholesale + negotiated |
| **Dispute fee** | $15 | $15 | Negotiated |
| **Refund** | Free (network fee not returned) | Free (network fee not returned) | Free |
| **Same-day payouts** | — | — | +0.4% per transfer |
| **Monthly volume cap** | $50K | $1M | None |
| **Payout schedule** | T+3 | T+2 | T+1 (same-day available) |

## How fees appear in your settlement

Fees come out of your settlement, not your bank account — there's no separate invoice. Each settlement file has a per-payment breakdown:

| Column | Example |
| --- | --- |
| `gross_amount` | `42.00` |
| `processing_fee` | `-1.52` |
| `net_amount` | `40.48` |

Refunds and dispute fees show up as separate negative line items in the same file. See [Settlement files](../reconciliation/settlement-files.md) for the full schema.

## Add-ons

A few features carry their own pricing on top of your plan:

<details>

<summary>Smart routing (Growth and Enterprise)</summary>

Included on Growth. On Enterprise it's also included by default but can be configured per acquirer agreement. See [Smart routing](../accept-payments/smart-routing.md).

</details>

<details>

<summary>3-D Secure 2 (all plans)</summary>

Free for required transactions (e.g. EU SCA). Optional 3DS on non-required transactions costs $0.05 per attempt — usually worth it for the liability shift on high-value charges.

</details>

<details>

<summary>Same-day payouts (Enterprise only)</summary>

0.4% of each same-day payout, billed against the same payout. You can leave the default T+1 schedule and use same-day on demand from the dashboard.

</details>

<details>

<summary>Custom reports (Growth and Enterprise)</summary>

Included up to 50 saved reports per workspace. Above that, $50/month per additional 50. See [Custom reports](../reporting/custom-reports.md).

</details>

## Promised pricing

For Enterprise customers on a custom contract, your negotiated rates are the source of truth. The table above shows the standard published pricing — if your contract overrides any line, what's in the contract applies. You can always see your effective rates in **Settings → Billing**.

{% if visitor.claims.unsigned.plan === "enterprise" %}

<p><a href="https://gitbook.com" class="button primary">View your contracted rates</a></p>

{% endif %}
