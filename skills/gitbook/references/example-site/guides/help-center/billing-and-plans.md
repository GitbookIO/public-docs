---
icon: file-invoice-dollar
description: Plan tiers, invoices, volume pricing, and how to switch between plans.
---

# Billing and plans

## What's the difference between Starter, Growth, and Enterprise?

Three tiers, gating both feature access and pricing:

| | Starter | Growth | Enterprise |
| --- | --- | --- | --- |
| Per-transaction (cards) | 2.9% + $0.30 | 2.7% + $0.30 | Custom |
| Volume cap | $50K/mo | $1M/mo | Uncapped |
| Payout schedule | T+3 | T+2 | T+1 (same-day available) |
| Connect (marketplaces) | — | Up to 100 sellers | Unlimited |
| Identity verification | Basic only | Cards + ACH | All flows |
| SSO | — | ✅ | ✅ |
| Custom contracts | — | — | ✅ |

For the full breakdown, see [Payments → Fees and pricing](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/fees-and-pricing).

## How do I see my current plan?

**Settings → Billing → Current plan.** You'll see your tier, your current month's volume, your effective rates (which may differ from the published rates if you're on a custom contract), and your next invoice estimate.

## How do I change plans?

**Settings → Billing → Change plan**. Upgrades take effect immediately; downgrades take effect at the end of the current billing month (so you don't lose access mid-month).

To move to Enterprise, the **Contact sales** button starts the conversation. Most Enterprise contracts close in 2–4 weeks.

## When do I get charged?

Per-transaction fees are netted from your settlement file each day — not invoiced separately. Your bank deposit equals gross volume minus fees minus refunds.

Add-ons (custom reports beyond 50, dispute alerts, on-demand payouts, etc.) are invoiced monthly. Invoices arrive on the 1st of each month for the prior month's add-on usage.

## Where do I find my invoices?

**Settings → Billing → Invoices**. Each month's invoice is downloadable as PDF. For finance teams who want them auto-emailed, configure recipients under **Settings → Billing → Invoice delivery**.

## Can I get volume discounts?

Yes, on Enterprise. Volume discount tiers kick in starting at $10M annual processing volume; the specifics depend on your card mix, region, and risk profile. Contact your account team.

For Growth customers approaching $1M/month consistently, Enterprise is usually the better economics — the conversation is worth having even if you're not at the cap yet.

## Are there setup fees or monthly minimums?

No setup fees. No monthly minimums on Starter or Growth. Enterprise contracts may include a minimum monthly commitment; that's negotiated as part of the contract.

## What if I exceed my plan's volume cap?

On Starter, you'll get email warnings at 80% and 95% of cap. At 100%, new charges fail with `volume_cap_exceeded` until you upgrade. You can upgrade mid-month and the new cap applies immediately.

On Growth, the same warnings fire at 80% and 95% of $1M; there's no hard cap, but rates above the cap scale to a flat 3.4% + $0.30 to encourage Enterprise migration.

## What happens to my refund processing fees?

When you take a payment, Evolve charges you the processing fee. When you refund it, the fee stays — you've paid the network and that fee isn't recoverable. The refund goes through at no additional cost from Evolve, but the original processing fee on the payment becomes a sunk cost.

This isn't unique to Evolve — every major processor works this way. See the [community thread on decline-code triage](https://gitbookio.github.io/evolve-demo/connections/community/decline-codes-vs-card-decline-codes.html) for how teams typically book this.

## Why was my account flagged for risk review?

Risk reviews can fire for a few reasons: rapid volume growth, a change in card-mix or geographic mix, a rising dispute rate, or unusual chargeback patterns. The dashboard shows the review reason and what's needed.

Most risk reviews resolve within 2 business days with no action from you. If we need information, you'll get an email and the dashboard will show a banner. Contact your account team if it's been longer than 5 business days.

## Where can I find more answers?

* [Community forum](https://gitbookio.github.io/evolve-demo/connections/community/)
* [YouTube: Same-day payouts tradeoffs](https://gitbookio.github.io/evolve-demo/connections/blog/same-day-payouts-tradeoffs.html)
* [Payments → Fees and pricing](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/fees-and-pricing)
