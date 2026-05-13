---
icon: file-invoice
description: Map every Evolve settlement line item to the right QuickBooks account.
---

# Reconciliation mapping

The default account mapping covers most teams. For more nuanced setups — multi-class tracking, location-based accounting, project codes — the **Advanced mapping** view in **Settings → Integrations → QuickBooks → Mapping** has finer controls.

## Default mapping

Out of the box, Evolve maps settlement-file line types to QuickBooks accounts:

| Evolve line type | Default QuickBooks account | Account category |
| --- | --- | --- |
| `payment` (gross) | Sales Income | Income |
| `payment.fee` | Bank Charges | Expense |
| `refund` | Returns and Allowances | Income (contra) |
| `refund.fee_unrecovered` | Bank Charges | Expense |
| `dispute_lost` | Bad Debt Expense | Expense |
| `dispute_lost.fee` | Bank Charges | Expense |
| `dispute_won` | Other Income | Income |
| `payout` | Bank Account | Asset |
| `reserve_held` | Restricted Cash | Asset |
| `reserve_released` | Bank Account | Asset |

You override any of these in the mapping view.

## Per-class mapping

QuickBooks Online (Plus and above) supports **classes** — a tagging system for tracking revenue across product lines, regions, or projects. Evolve can tag each journal entry with a class derived from the charge's metadata:

```
Charge metadata: { product_line: "subscriptions" }
   ↓
QB journal entry class: "subscriptions"
```

In **Settings → Integrations → QuickBooks → Classes**, set which metadata key drives the class assignment. Multi-line businesses (commerce + subscriptions, US + EU, etc.) almost always want this enabled.

## Per-location mapping

QuickBooks Online's **locations** feature works similarly to classes, but for physical locations or business units. Map a metadata key to a QB location to track revenue per restaurant, per store, etc.

## Connect platforms

For Connect platforms, the mapping has an extra layer:

* **Application fees** earned by the platform → your platform's revenue account.
* **Transfers to sellers** → typically a clearing account, since the money isn't your revenue (it's the seller's).
* **Per-seller tracking** → optional, via class mapping per `connected_account_id`.

Most platforms with under 50 sellers track per-seller in QB; larger platforms track aggregated by tier or category.

## Reconciling against your bank

Each daily settlement creates one **payout** journal entry that should match exactly one credit on your bank statement. The Evolve dashboard shows a per-day match report:

* Posted to QB ✓
* Bank credit posted ✓
* Match status: matched / mismatched / pending

For mismatches, the report shows the difference (usually a timing issue between Evolve's posting and the bank's posting). Most discrepancies clear within a business day.

## Backfilling historical data

When you first connect QuickBooks, you can backfill journal entries for past settlements. Three options:

* **No backfill** — start with today's settlement going forward.
* **30 days back** — most common; matches the typical month-end-close timing.
* **Custom range** — useful for migrating from another accounting integration mid-year.

Backfills run in the background; you'll get an email when complete.

## Closing the books

For month-end close:

1. Confirm the last settlement of the month has posted to QB (usually the morning of the 1st).
2. Run the **Reconciliation summary** report from Evolve and compare to QB's balance.
3. Sign off on any flagged mismatches.
4. Close the period in QuickBooks.

The whole process for a typical month is 15–30 minutes for an accountant familiar with the integration.

## Last reviewed

Reviewed in early 2026. Mapping options expand occasionally with new QuickBooks features; suggest changes via [the docs repo](https://github.com/GitbookIO/evolve-demo).

## Related

* [QuickBooks overview](README.md) — install and concepts.
* [Settlement files](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reconciliation/settlement-files) — the source data this writes against.
* [NetSuite custom field mapping](../netsuite/custom-field-mapping.md) — equivalent for NetSuite customers.
