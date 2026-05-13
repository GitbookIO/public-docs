---
icon: file-csv
description: The daily CSV that explains every cent moving in and out of your account.
---

# Settlement files

Every business day at <code class="expression">space.vars.settlement_time_utc</code>, Evolve produces a CSV that lists every payment, refund, fee, dispute deduction, and adjustment that affected your balance during the previous day. The file is the source of truth — what's on it equals exactly what shows up in your bank account on payout day.

## Where to find it

Three ways, in order of decreasing effort:

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Dashboard</strong></td><td>Manual download. Best for occasional use.</td><td></td></tr><tr><td><strong>Email</strong></td><td>Daily attachment to your finance distribution list.</td><td></td></tr><tr><td><strong>Scheduled export</strong></td><td>Automatic push to SFTP, S3, or GCS.</td><td><a href="../reporting/sharing-exports.md">sharing-exports.md</a></td></tr></tbody></table>

## File structure

A single file per settlement day. The filename contains the settlement date and your account ID:

```
evolve-settlement-2026-04-29-acct_8L2pK9q.csv
```

Each row is one line item. Multiple rows can belong to the same payment — for example, a captured payment and the fee for it appear on separate rows.

## Columns

| Column | Description | Example |
| --- | --- | --- |
| `settlement_date` | The settlement date this row belongs to | `2026-04-29` |
| `id` | Unique line item ID | `stl_li_3KsM12pL9qXa7` |
| `type` | The line type — see below | `payment` |
| `source_id` | The originating object | `pay_3KsM12pL9qXa7` |
| `description` | Free-text description from the original payment | `Order #1042` |
| `gross_amount` | Amount before fees | `42.00` |
| `fee` | Evolve fee for this line | `-1.52` |
| `net_amount` | What hit your balance | `40.48` |
| `currency` | ISO 4217 code | `USD` |
| `customer_id` | If applicable | `cus_4n2P3qR5sT6uV` |
| `metadata.*` | Custom metadata you attached at payment creation | varies |

The full column reference, including all `type` values, lives at the top of every file as a comment row — no need to memorize anything.

## Line types

| Type | When you'll see it |
| --- | --- |
| `payment` | A captured payment on the settlement day |
| `refund` | A refund issued on the settlement day |
| `dispute_lost` | The disputed amount + dispute fee, deducted |
| `dispute_won` | The disputed amount returned, fee not refunded |
| `payout` | The net amount sent to your bank (one row per file) |
| `adjustment` | A manual adjustment made by Evolve (rare) |
| `reserve_release` | A previously held amount released to your balance |

## A small example

A day with one payment, one refund, and a payout looks like this:

```csv
settlement_date,id,type,source_id,gross_amount,fee,net_amount,currency
2026-04-29,stl_li_a1,payment,pay_3KsM12pL9qXa7,42.00,-1.52,40.48,USD
2026-04-29,stl_li_a2,payment,pay_5n8R4qT2bX9c1,128.00,-3.78,124.22,USD
2026-04-29,stl_li_a3,refund,re_2pK9qL3sM4tN5,-42.00,0.00,-42.00,USD
2026-04-29,stl_li_a4,payout,po_7vY3wZ8aB2cD9,0.00,0.00,-122.70,USD
```

The payout row's `net_amount` is the negative of the sum of the other rows — it's what leaves your Evolve balance and lands in your bank.

## Reconciling against your bank

A simple daily process:

{% stepper %}
{% step %}

### Match the payout to the bank deposit

The `payout` row's `net_amount` (as a positive number) should equal exactly one credit on your bank statement, dated per your plan's payout schedule.

{% endstep %}

{% step %}

### Book each payment as revenue

Sum the `payment` rows' `gross_amount` — that's your revenue for the day. The corresponding `fee` rows are processing-fee expenses.

{% endstep %}

{% step %}

### Book refunds and disputes

`refund` rows reduce revenue. `dispute_lost` rows reduce revenue and add a dispute-fee expense.

{% endstep %}

{% step %}

### Verify the file balances

Sum the `net_amount` column. It should equal zero — every cent that came in either left in the payout, was netted by a refund/dispute, or moved into reserves.

{% endstep %}
{% endstepper %}

If the file doesn't balance to zero, something is off — open a support ticket with the file attached and we'll trace it.

## Going further

* Push files automatically to your data warehouse — see [Sharing and scheduled exports](../reporting/sharing-exports.md).
* Build reconciliation into QuickBooks or NetSuite — see [Guides / Integrations](https://app.gitbook.com/s/MBT3EDUK7DzXmR0k9cje/).
* For deeper analysis, the same data is available as queryable [Reports](../reporting/standard-reports.md).
