---
icon: share-nodes
description: Push reports and settlement files to email, Slack, SFTP, or cloud storage on a schedule.
---

# Sharing and scheduled exports

Once you've built a report you check daily, the next step is to stop opening the dashboard to look at it. Evolve can push any standard or custom report — and any settlement file — to wherever your team already works.

## Destinations

| Destination | Format | Best for |
| --- | --- | --- |
| **Email** | CSV attachment + summary in body | Daily/weekly digest to a finance distribution list |
| **Slack** | Summary message + CSV attachment | Ops channel notifications |
| **SFTP** | CSV upload | Legacy finance systems and managed-service providers |
| **AWS S3** | CSV upload | Most data-engineering setups |
| **Google Cloud Storage** | CSV upload | GCP-first organizations |
| **Webhook** | JSON POST with summary + signed download URL | Custom downstream automation |

## Setting up a scheduled export

{% stepper %}
{% step %}

### Pick the report

From any standard or custom report, click **Schedule**. Or go to **Reports → Schedules → New** and pick a report from the list.

{% endstep %}

{% step %}

### Pick the cadence

Daily, weekly (pick a day), monthly (pick a date), or after each settlement (recommended for finance flows).

{% endstep %}

{% step %}

### Pick the destination

Choose one of the destinations above and authenticate. For SFTP, S3, and GCS, Evolve gives you a service account or set of static IPs to allow-list.

{% endstep %}

{% step %}

### Pick the format

CSV is the default. For some reports, JSON is also available. Choose whether to include a header row and which timezone date columns should use.

{% endstep %}

{% step %}

### Save

The first export runs on the next scheduled tick. You can also trigger an immediate test from the same screen.

{% endstep %}
{% endstepper %}

## Daily settlement push

The most common scheduled export setup:

* **Source:** the settlement file (one CSV per day).
* **Cadence:** every day after the <code class="expression">space.vars.settlement_time_utc</code> cut-off.
* **Destination:** SFTP or S3 in your finance environment.
* **Format:** CSV, UTF-8, with a header row.

This puts the file your accounting team imports each morning into a known location, named by date — `evolve-settlement-2026-04-29.csv` — and your existing import script can pick it up without any change to the dashboard workflow.

## Email distributions

Email is the right destination when:

* The recipients are humans, not systems.
* The cadence is weekly or monthly (daily emails get ignored).
* The data is summary-level, not row-by-row reconciliation.

You can configure up to 10 recipient addresses per scheduled email. Each email contains:

* A short summary in the body — "Daily revenue: $42,180. Up 5% from last week."
* A CSV attachment with the full data.
* A direct link back to the live dashboard view.

Emails are sent from `reports@evolve.com`. Make sure the recipients' mail servers don't filter it.

## Slack

The Slack integration posts a summary message to a channel you've connected, with a CSV attachment for the underlying data. The message format is configurable — you can include the headline metric, a chart preview (as an image), and a link back to the dashboard.

To connect Slack, install the [Evolve Slack app](https://app.gitbook.com/s/MBT3EDUK7DzXmR0k9cje/slack). The same app can also post real-time alerts for things like dispute openings and large refunds.

## Webhooks for finance automation

For more advanced automation — building a custom finance workflow, triggering a downstream pipeline, posting to a tool not in our destination list — use the webhook destination. Each scheduled run POSTs a JSON payload to your endpoint:

```json
{
  "schedule_id": "sched_3K2pL9q",
  "report_id": "rpt_8M2nF6m",
  "ran_at": "2026-04-30T06:01:14Z",
  "row_count": 412,
  "summary": { "net_revenue": 42180.55, "currency": "USD" },
  "download_url": "https://api.evolve.com/v1/reports/runs/rpt_8M2nF6m/download?token=...",
  "download_expires_at": "2026-05-01T06:01:14Z"
}
```

The download URL is signed and valid for 24 hours. Your code fetches the CSV when it's ready to process — no need to receive megabytes of data in the webhook itself.

## Auditing scheduled exports

Every scheduled run is logged in **Reports → Schedules → History**, with:

* When it ran.
* Whether it succeeded.
* Where it was delivered.
* The output file (downloadable for 30 days).

If a destination fails (SFTP timeout, S3 permission denied), you'll get an email and the failed run is retried up to 3 times over an hour.

## Permissions and security

Scheduled exports respect the role permissions of the user who created them. If that user's role changes — or they leave the team — the schedule pauses until an admin reassigns it.

For sensitive destinations, you can require a second admin to approve the schedule before it goes live. Toggle this in **Settings → Security → Approval policies**.

## Related

* [Standard reports](standard-reports.md) — what to schedule first.
* [Custom reports](custom-reports.md) — building reports worth scheduling.
* [Exporting to BI tools](exporting.md) — for warehouse-level integration.
* [Settlement files](../reconciliation/settlement-files.md) — the most-scheduled file.
