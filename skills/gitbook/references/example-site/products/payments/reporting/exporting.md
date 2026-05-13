---
icon: file-export
description: Pipe Evolve data into your data warehouse, BI tool, or accounting system.
---

# Exporting to BI tools

For most businesses, the dashboard is enough — you build reports, save the views you care about, and check them daily. But if your data team is the source of truth for finance reporting, or you want to combine Evolve data with marketing, product, and ops data in one place, you'll want it pushed into your warehouse.

## What's available

Three categories of pre-built integration:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-warehouse" style="color:$primary;">:warehouse:</i></h3></td><td><strong>Data warehouses</strong></td><td>Snowflake, BigQuery, Redshift, Databricks.</td><td></td></tr><tr><td><h3><i class="fa-chart-pie" style="color:$primary;">:chart-pie:</i></h3></td><td><strong>BI tools</strong></td><td>Looker, Tableau, Mode, Metabase.</td><td></td></tr><tr><td><h3><i class="fa-calculator" style="color:$primary;">:calculator:</i></h3></td><td><strong>Accounting</strong></td><td>QuickBooks, NetSuite, Xero.</td><td><a href="https://app.gitbook.com/s/MBT3EDUK7DzXmR0k9cje/">README.md</a></td></tr></tbody></table>

If your tool isn't listed, you can also:

* Pull data via the [reporting API](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api/reports) (requires engineering effort).
* Use [scheduled CSV exports](sharing-exports.md) to SFTP or S3 and pick them up from there.

## Data warehouses

Evolve's warehouse connectors push a defined schema of tables on a schedule — typically every hour. The tables include:

| Table | Contents |
| --- | --- |
| `payments` | One row per payment, current state |
| `payment_events` | One row per state change, full history |
| `refunds` | One row per refund |
| `disputes` | One row per dispute, including evidence and outcome |
| `customers` | One row per customer |
| `payment_methods` | Saved methods linked to customers |
| `settlements` | Daily settlement summaries |
| `settlement_line_items` | One row per settlement line — equivalent to the [CSV file](../reconciliation/settlement-files.md) |
| `acquirer_routes` | Per-payment routing decisions and outcomes |

Joining these is straightforward — every table has a `payment_id` or `customer_id` column where applicable.

### Setting up a warehouse connector

{% stepper %}
{% step %}

### Pick the warehouse

In **Settings → Data → Warehouse connectors**, click the warehouse you want and follow the auth flow. We support OAuth where the warehouse offers it, otherwise it's a service-account credential.

{% endstep %}

{% step %}

### Pick the dataset

Choose which database and schema Evolve should write to. We strongly recommend a dedicated schema — `evolve_raw` is a common choice — so the connector can manage its own tables without touching anything else.

{% endstep %}

{% step %}

### Pick the schedule

Hourly is the default. You can go to every 15 minutes on Enterprise. Daily is fine if your reporting cadence is daily.

{% endstep %}

{% step %}

### Trigger the first sync

Click **Sync now** to backfill. The first sync pulls the last 24 months of data and can take a few hours for large accounts; we'll email you when it's done.

{% endstep %}
{% endstepper %}

## BI tool integrations

The BI integrations are mostly thin wrappers around the warehouse connectors — they're a convenience for teams that want a curated set of reports out of the box.

When you connect Looker, Tableau, Mode, or Metabase, you get:

* A **starter dashboard** mirroring our [standard reports](standard-reports.md).
* A **semantic model / explore** so non-technical users can build queries by dragging fields.
* **Drill-through links** from charts back to the Evolve dashboard for the underlying payment.

You're not locked in — once data is in the warehouse, you can build whatever you want.

## Accounting integrations

QuickBooks, NetSuite, and Xero integrations work differently — they push **journal entries**, not raw data. Each settlement file produces one journal entry per accounting period, with the right account codes for revenue, fees, refunds, and disputes.

See [Guides / Integrations](https://app.gitbook.com/s/MBT3EDUK7DzXmR0k9cje/) for the per-tool setup.

## Related

* [Sharing and scheduled exports](sharing-exports.md) — CSV-based pushes, and email distributions.
* [Reporting API](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api/reports) — pull data programmatically.
* [Settlement files](../reconciliation/settlement-files.md) — the daily CSV that finance imports.
