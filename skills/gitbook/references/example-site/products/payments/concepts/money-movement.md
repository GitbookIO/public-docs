---
icon: money-bill-transfer
description: How captured funds become a payout in your bank account.
---

# Money movement and settlement

A captured charge isn't yet money in your bank — it's a balance on your Evolve account. Evolve groups captured charges into daily settlements and pushes the net amount to your linked bank account on a payout schedule that depends on your plan.

## The flow

```mermaid
flowchart LR
    A[Captured] --> B[Available balance]
    B --> C[Daily settlement]
    C --> D[Payout to bank]
```

* **Available balance** updates in real time. You can see it in the dashboard or query `GET /v1/balance`.
* **Settlement** runs once a day at <code class="expression">space.vars.settlement_time_utc</code>. It bundles all captures, refunds, fees, and dispute deductions into a single net amount and produces a [settlement file](../reconciliation/settlement-files.md).
* **Payouts** are initiated from the settlement file on your plan's schedule.

## Payout schedule by plan

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="info" icon="clock" %}
**Starter:** Payouts arrive **T+3 business days** after capture. There's no faster option on this plan.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "growth" %}

{% hint style="info" icon="clock" %}
**Growth:** Payouts arrive **T+2 business days** after capture. Same-day payouts are available as an Enterprise add-on.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="success" icon="clock" %}
**Enterprise:** Default schedule is **T+1 business day**. Same-day payouts are available for an additional 0.4% per transfer — turn it on under **Settings → Payouts**.
{% endhint %}

{% endif %}

| Plan | Default schedule | Faster option |
| --- | --- | --- |
| Starter | T+3 | — |
| Growth | T+2 | — |
| Enterprise | T+1 | Same-day (+0.4%) |

## What's deducted

Each settlement nets the following against your captures:

* **Processing fees** — per your plan's pricing.
* **Refunds issued in that window**.
* **Dispute deductions** — both the disputed amount and the per-dispute fee ($15 USD).
* **Reserves**, if your account has a reserve policy in place.

The settlement file shows each line item by ID so you can match it back to the originating charge or refund. See [Settlement files](../reconciliation/settlement-files.md).

## Multi-currency

If you accept multiple currencies, Evolve maintains a separate balance and payout schedule per currency. You can hold balances and pay out to bank accounts denominated in the same currency, or convert at settlement time at the daily wholesale rate plus 0.5%.

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="info" %}
Enterprise customers can negotiate the FX margin and configure per-entity payout accounts. Contact your account team.
{% endhint %}

{% endif %}

## Holds and reserves

Two scenarios delay payout for individual charges:

<details>

<summary>Risk holds</summary>

If a charge triggers a risk rule, Evolve may hold the funds for up to 14 days while the transaction is reviewed. You'll see `held_for_review: true` on the charge object and a `payout_hold` line in the settlement file.

</details>

<details>

<summary>Account reserves</summary>

For new accounts or those processing high-risk verticals, Evolve may set a rolling reserve — typically 5% held for 90 days. Reserves release automatically as they age out and appear as positive line items on later settlements.

</details>

## Related

* [Settlement files](../reconciliation/settlement-files.md) — the daily CSV format.
* [Disputes and chargebacks](../reconciliation/disputes.md) — how disputes affect settlement.
* [Reporting](../reporting/README.md) — building finance reports on top of settlements.
