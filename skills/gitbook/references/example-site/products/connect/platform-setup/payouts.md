---
icon: money-bill-transfer
description: How sellers' balances become payouts to their bank accounts.
---

# Payouts to sellers

Each seller has their own balance on Evolve, fed by transfers from charges they've completed (minus your application fees and any refunds). That balance pays out to their verified bank account on a schedule — daily, weekly, monthly, or on demand.

The platform doesn't touch this money. Once it's transferred to the seller's connected-account balance, it's their funds; they get paid out automatically and you can't pull it back unless you reverse a specific transfer.

## Default schedules

Three schedule shapes:

| Schedule | When sellers get paid | Best for |
| --- | --- | --- |
| **Daily** | T+1 (next business day after capture) | Marketplaces, food delivery, anything where seller cash flow matters |
| **Weekly** | Every Monday for the prior week | Subscription platforms, B2B SaaS |
| **Monthly** | 1st of the month for the prior month | Long-tail marketplaces, royalty payouts |
| **Manual** | When you trigger it | Platforms with custom scheduling |

You set the platform-wide default in **Connect → Settings → Default payout schedule**. Sellers can override their own schedule from their portal (within the bounds you allow).

## What flows through

The seller's balance equals everything in their favor minus everything against:

```
Charge transfers
- Refund deductions
- Dispute deductions (if assigned to seller)
- Direct charges from platform (if any)
+ Direct credits from platform
= Seller balance
```

When the schedule runs, the seller's full positive balance pays out — minus any reserves you've configured.

## Reserves

Some platforms hold a percentage of the seller's balance for a rolling window — common in marketplaces with high dispute exposure or platforms launching with new sellers.

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="info" %}
**Enterprise customers** can configure per-seller reserves with custom rules — e.g. "5% rolling reserve for new sellers, dropping to 0% after 90 days." Set in **Connect → Settings → Reserves**.
{% endhint %}

{% endif %}

A typical reserve config:

| Setting | Common value |
| --- | --- |
| **Reserve percentage** | 5–10% |
| **Reserve window** | 90 days rolling |
| **Applies to** | All new sellers in their first 90 days |

The reserve sits on the seller's balance but isn't paid out. Each day, the oldest 1/90th rolls off (90-day window) and becomes payable. Disputes and refunds during the window come out of the reserve before they hit the seller's payout.

The seller can see their reserved balance separately from their payable balance in their portal.

## On-demand payouts

For platforms where seller cash flow really matters — gig-economy apps, instant-pay marketplaces — you can offer **on-demand payouts**: a button the seller taps when they want their money now, before the next scheduled payout.

On-demand payouts cost an extra 1% of the payout amount, charged to the seller (or absorbed by the platform — your call). They land in the seller's bank within minutes if the bank supports RTP/FedNow, otherwise within hours.

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="success" icon="bolt" %}
**Enterprise customers** can configure on-demand payouts and decide whether the fee is paid by the seller, the platform, or split. Configure in **Connect → Settings → Instant payouts**.
{% endhint %}

{% endif %}

## Holds

Three reasons a seller's payout might be held:

<details>

<summary>Risk hold</summary>

Evolve's risk system flagged something — unusually high transaction volume, dispute pattern, or specific signals from the network. The seller's payouts pause for up to 14 days while the case is reviewed. The seller and platform both get notified.

</details>

<details>

<summary>Platform hold</summary>

Your platform has held the seller manually — usually because of a complaint, a TOS violation, or a pending investigation. You set the duration; the dashboard shows your team is responsible for releasing it.

</details>

<details>

<summary>Compliance hold</summary>

A re-verification is required (e.g. document expired, address change pending). Payouts pause until verification completes. Usually resolved within 1–2 days.

</details>

In all three cases, charges keep running normally — the seller can still take payments. Only the payout to their bank is paused.

## Failed payouts

A scheduled payout can fail if the seller's bank account becomes invalid (closed, frozen, or wrong details). When this happens:

1. The payout is marked **Failed** with the bank's reason code.
2. The seller and platform get an email.
3. The amount returns to the seller's balance.
4. The seller updates their bank account in their portal; the next scheduled payout includes the failed amount.

Repeated failures (three in a row) auto-pause the seller's payouts and require platform intervention.

## What you see as the platform

The platform dashboard shows aggregate payout activity:

* **Today's payouts** — total amount across all sellers, by currency.
* **Pending payouts** — what's queued for the next schedule run.
* **Held payouts** — broken down by hold type, with the action item to clear each.
* **Failed payouts** — recent failures, with one-click resend.

For the per-seller view, click into the seller and see their payout history alongside their charges and balance.

## Reporting

Two payout reports under **Reports** when Connect is enabled:

* **Platform payout summary** — daily/weekly/monthly aggregates of total payouts.
* **Per-seller payout history** — drill-down per seller for support purposes.

Both export to CSV and can be [scheduled](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reporting/sharing-exports).

## Related

* [Splitting payments](splitting-payments.md) — how each transfer's amount is determined.
* [Refunds and disputes](refunds-and-disputes.md) — how reversals affect payouts.
* [Money movement (Payments)](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/money-movement) — the underlying settlement engine.
