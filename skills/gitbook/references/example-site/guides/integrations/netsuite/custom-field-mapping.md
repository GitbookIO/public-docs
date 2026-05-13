---
icon: arrows-up-down-left-right
description: Map Evolve metadata to NetSuite custom segments — departments, classes, locations, and custom-defined.
---

# Custom field mapping

NetSuite's custom segments are how multi-divisional, multi-region, and project-tracked accounting works. Evolve's bundle exposes a mapping screen where you bind Evolve metadata keys to NetSuite segments, so each journal entry posts to the right slice automatically.

## NetSuite segments supported

| NetSuite segment | What it represents | Common Evolve metadata source |
| --- | --- | --- |
| **Department** | Organizational unit (Sales, Engineering) | `metadata.department` |
| **Class** | Cross-cutting category (Subscriptions, Hardware) | `metadata.product_line` |
| **Location** | Physical site (Store 42, Warehouse East) | `metadata.location_id` or `metadata.store_id` |
| **Subsidiary** | Legal entity in a OneWorld account | Evolve account, or `metadata.subsidiary_id` |
| **Custom segments** | Anything you've defined (Project, Region, Cohort) | Per your mapping |

## Setting up a mapping

In NetSuite, the bundle's setup screen (under **Customization → SuiteApps → Evolve → Setup**) shows a row per custom segment. For each one:

1. Pick which segment values are available (NetSuite gives you a list).
2. Set the **default value** — what to post if the metadata key is missing.
3. Set the **metadata key** — which Evolve `metadata.X` field the bundle reads.
4. (Optional) Define a **mapping table** for translating Evolve values to NetSuite internal IDs.

Save. From the next sync onward, journal entries are tagged correctly.

## Mapping tables

When the Evolve metadata value doesn't match the NetSuite segment value verbatim, use a mapping table:

| Evolve metadata value | NetSuite segment internal ID |
| --- | --- |
| `subscriptions` | 12 (Class: Subscriptions) |
| `commerce` | 14 (Class: E-commerce) |
| `services` | 18 (Class: Professional Services) |

The bundle keeps the mapping table cached; updating it requires no resync — future entries just use the new mapping.

## Multi-subsidiary specifics

For Connect platforms with sellers in multiple legal entities, the typical setup:

* Tag each connected account with `metadata.subsidiary_id` during onboarding.
* Map `metadata.subsidiary_id` → NetSuite subsidiary in the bundle.
* Charges to that connected account post to the corresponding subsidiary's books.

For platforms charging multiple subsidiaries from a single Evolve account, the bundle handles inter-subsidiary eliminations on the FX side automatically — the elimination journal entries post nightly.

## Custom segment example

A common pattern: a SaaS company tracking revenue per product family AND per region:

```
Evolve metadata: { product_line: "subscriptions", region: "us" }
   ↓
NetSuite journal entry segments:
  - Class: "Subscriptions" (from product_line mapping)
  - Custom segment "Region": "United States" (from region mapping)
```

The reporting in NetSuite then slices on either or both — `Subscription revenue` × `US` = a single cell in your management report.

## Required vs optional segments

Some NetSuite installations require a value on every line item; others let lines have nulls. The bundle's setup tells you which:

* **Required segments** must have a default value or every journal entry needs a metadata value. The bundle errors out the day's sync if values are missing.
* **Optional segments** can be null; the bundle leaves them blank.

Most teams set sensible defaults (Region: "United States", Department: "Operations") to handle the cases where metadata is missing.

## Multi-currency and FX

For multi-currency Evolve accounts posting to multi-currency NetSuite, the bundle handles:

* Per-currency journal entries (one entry per currency per day).
* FX gain/loss postings on conversion (using NetSuite's exchange rate table).
* Currency-revaluation entries at month-end (configurable per subsidiary).

For complex setups (e.g., booking-currency vs reporting-currency mismatches), talk to your account team — there are several options depending on how your NetSuite is configured.

## Validating a mapping change

After changing a mapping:

1. Click **Sync test entry** in the bundle's setup screen. Posts a single test entry tagged with the new mapping.
2. Verify in NetSuite that the segments are correct.
3. If correct, click **Apply** to use the new mapping for future syncs.

The test entry is reversed automatically after 24 hours so it doesn't pollute your books.

## Last reviewed

Last reviewed in early 2026. Mapping options expand as NetSuite ships new custom-segment features. Suggest updates via [the docs repo](https://github.com/GitbookIO/evolve-demo).

## Related

* [NetSuite overview](README.md) — install and high-level setup.
* [QuickBooks reconciliation mapping](../quickbooks/reconciliation-mapping.md) — equivalent for QB customers.
* [Settlement files](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reconciliation/settlement-files) — the source data.
