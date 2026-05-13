---
description: See what your business is doing — by day, by product, by customer, by acquirer.
icon: chart-line
---

# Reporting

Everything that happens in Evolve is queryable. Reports turn raw events into the views your team actually looks at — daily revenue, top customers, decline reasons, dispute rates, the lift from smart routing. They're available in the dashboard, exportable to CSV, and pushable to your data warehouse.

{% if visitor.claims.unsigned.persona === "partner" %}

{% hint style="info" icon="building" %}
**Setting up reporting at the enterprise level?** You'll likely want **scheduled exports** to your warehouse so your BI tool is the source of truth, not the dashboard. Skip ahead to [Sharing and scheduled exports](sharing-exports.md).
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}

{% hint style="info" icon="hand-wave" %}
**New to Evolve?** The fastest way to get a feel for what's possible is to open [Standard reports](standard-reports.md) — they're already populated with your test-mode activity.
{% endhint %}

{% endif %}

## What reports give you

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-chart-bar" style="color:$primary;">:chart-bar:</i></h3></td><td><strong>Standard reports</strong></td><td>Pre-built views finance and ops use every day.</td><td><a href="standard-reports.md">standard-reports.md</a></td></tr><tr><td><h3><i class="fa-sliders" style="color:$primary;">:sliders:</i></h3></td><td><strong>Custom reports</strong></td><td>Build your own views on top of the same data.</td><td><a href="custom-reports.md">custom-reports.md</a></td></tr><tr><td><h3><i class="fa-file-export" style="color:$primary;">:file-export:</i></h3></td><td><strong>Exporting to BI tools</strong></td><td>Push to Looker, Tableau, your warehouse.</td><td><a href="exporting.md">exporting.md</a></td></tr><tr><td><h3><i class="fa-share-nodes" style="color:$primary;">:share-nodes:</i></h3></td><td><strong>Sharing and scheduled exports</strong></td><td>Email distributions, SFTP and S3 pushes.</td><td><a href="sharing-exports.md">sharing-exports.md</a></td></tr></tbody></table>

## What you can answer

A few examples of what falls out of the standard reports:

| Question | Report |
| --- | --- |
| What did we make yesterday, after fees? | Daily revenue |
| Which payment methods are growing? | Methods over time |
| What's our approval rate, and is smart routing helping? | Routing report |
| Which customers are top of the LTV chart? | Top customers |
| What's our dispute rate this quarter? | Dispute report |
| Why did this batch of payments fail? | Decline reasons |
| Did we collect enough to cover the upcoming payouts? | Cash position |

## How reports stay fresh

* **Dashboard charts** update in near-real-time — typically a few seconds behind the underlying event.
* **Daily reports** (revenue, methods, declines) cut over at midnight in your account's timezone, set in **Settings → Account → Timezone**.
* **Settlement-anchored reports** (anything tied to a specific payout) close at the daily settlement cut-off, <code class="expression">space.vars.settlement_time_utc</code>.
* **Custom reports** run on demand; saved views can be scheduled to refresh and email/post to a destination.

## Permissions

Reports respect your role's data scope:

| Role | Can see |
| --- | --- |
| Viewer | Aggregate reports, no per-customer data |
| Finance | Everything in this section, plus settlement files |
| Ops | Aggregate reports + per-customer history needed to support |
| Admin | Everything, plus permission to schedule and share |

Configure in **Settings → Team → Roles**.

## Related

* [Settlement files](../reconciliation/settlement-files.md) — the source data for all finance reports.
* [Smart routing](../accept-payments/smart-routing.md) — what the Routing report measures.
* [Guides / Integrations](https://app.gitbook.com/s/MBT3EDUK7DzXmR0k9cje/) — pre-built connectors to QuickBooks, NetSuite, Looker, and more.
