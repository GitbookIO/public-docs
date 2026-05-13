---
icon: sliders
description: Build your own views on top of Evolve's data — without writing SQL.
---

# Custom reports

Custom reports let you build views beyond the [standard reports](standard-reports.md) — different breakdowns, different filters, different chart types — and save them for your team. They run against the same underlying data, so they're always consistent with what shows up in finance reports.

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="warning" icon="lock" %}
**Custom reports are a Growth and Enterprise feature.** Starter accounts get full access to standard reports and can save filtered views, but can't build new chart types from scratch.
{% endhint %}

{% endif %}

## What you can build

Three kinds of report, each backed by a different builder:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-chart-line" style="color:$primary;">:chart-line:</i></h3></td><td><strong>Time series</strong></td><td>A metric over time, optionally split by a dimension.</td><td></td></tr><tr><td><h3><i class="fa-users-line" style="color:$primary;">:users-line:</i></h3></td><td><strong>Cohort</strong></td><td>Customer groups followed forward in time.</td><td></td></tr><tr><td><h3><i class="fa-table-cells" style="color:$primary;">:table-cells:</i></h3></td><td><strong>Pivot</strong></td><td>Two-dimensional table, one metric per cell.</td><td></td></tr></tbody></table>

## Building a time-series report

The most common kind. An example: "monthly net revenue, split by payment method, last 12 months."

{% stepper %}
{% step %}

### Pick a metric

In **Reports → New report**, choose **Time series** and pick a metric — net revenue, payment count, refund rate, dispute count, approval rate, fee total.

{% endstep %}

{% step %}

### Pick a time grain

Day, week, or month. The grain locks the start of each bucket — daily uses your account timezone, weekly buckets start on Monday, monthly buckets on the 1st.

{% endstep %}

{% step %}

### Add a split (optional)

Split the metric by a dimension — payment method, currency, region, customer cohort, acquirer, or a metadata field you've attached at payment creation. The chart turns into stacked bars or a multi-line chart.

{% endstep %}

{% step %}

### Add filters

Restrict the dataset before charting — for example, "only payments above $100" or "only customers tagged `enterprise`."

{% endstep %}

{% step %}

### Save and share

Click **Save**. Name it, give it an emoji icon, optionally pin it to your account dashboard. From here you can also schedule it (see [Sharing and scheduled exports](sharing-exports.md)).

{% endstep %}
{% endstepper %}

## Building a cohort report

Cohort reports answer questions like "what fraction of customers acquired in March were still paying us in June?" — useful for subscription businesses and any product where return purchases matter.

* **Cohort definition:** the event that puts a customer into a cohort (first payment, first subscription, sign-up).
* **Cohort grain:** weekly or monthly.
* **Forward metric:** what you're measuring over time — retention, cumulative revenue, refund rate.

The result is the classic triangular cohort chart, with each cohort as a row and time-since-cohort as columns.

## Building a pivot report

Pivot reports give you a two-dimensional grid — one dimension per axis, one metric per cell. An example: "decline rate by issuer country and card brand, last 30 days."

The builder is similar to a spreadsheet pivot table:

* **Rows** — one dimension.
* **Columns** — another dimension.
* **Cell value** — the metric, e.g. count, sum, average, percentile.

Pivot reports are great for spotting outliers — a single bad row often jumps out.

## Available metrics

| Metric | Description |
| --- | --- |
| `payment_count` | Number of payments |
| `payment_volume_gross` | Sum of payment amounts before fees |
| `payment_volume_net` | After fees and refunds |
| `approval_rate` | Approved / (approved + declined) |
| `decline_rate` | Declined / total |
| `refund_count` | Number of refunds |
| `refund_volume` | Sum of refund amounts |
| `dispute_count` | Number of disputes opened |
| `dispute_rate` | Disputes / payments |
| `dispute_win_rate` | Won / (won + lost) |
| `fee_total` | Total processing fees paid |
| `customer_count` | Distinct customers in the period |

## Available dimensions

| Dimension | Examples |
| --- | --- |
| `payment_method` | `card`, `ach_debit`, `wire`, `sepa`, ... |
| `card_brand` | `visa`, `mastercard`, `amex`, ... |
| `currency` | `usd`, `eur`, `gbp`, ... |
| `region` | `us`, `eu`, `apac`, ... |
| `acquirer` | The processor used |
| `customer_cohort` | A cohort tag you've defined |
| `metadata.<key>` | Any metadata field on the underlying payment |

## Saving and sharing

Custom reports live in your workspace and respect your team's permissions. You can:

* **Pin** a report to your account dashboard so it loads on first sign-in.
* **Share** a read-only link with anyone in your workspace.
* **Schedule** it to email or push to a destination — see [Sharing and scheduled exports](sharing-exports.md).
* **Export** the underlying data to CSV.

## Limits

* Up to **50 saved custom reports** per workspace included; **$50/month per additional 50** beyond that.
* Reports run over the last **24 months** of data by default. For older data, see [Exporting to BI tools](exporting.md).
* Reports refresh on demand. A scheduled refresh runs as part of the schedule itself.

## Related

* [Standard reports](standard-reports.md) — the pre-built starting points.
* [Exporting to BI tools](exporting.md) — for anything that doesn't fit the report builder.
