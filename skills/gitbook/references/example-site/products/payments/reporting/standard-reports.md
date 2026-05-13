---
icon: chart-bar
description: The pre-built reports finance and ops teams use every day.
---

# Standard reports

Standard reports cover the questions every payments team needs to answer regularly. They're available to every account, on every plan, and they're the right starting point before deciding whether you need a custom report.

Each report has the same structure:

* A **default view** that loads when you open it.
* **Filters** (date range, currency, payment method, customer cohort) at the top.
* An **export to CSV** button.
* A **save as custom report** button to lock in your filter set.

## The reports

### Daily revenue

How much you made each day, after processing fees and refunds. The default view shows the last 30 days.

* **Numerator:** sum of `payment.net_amount` − sum of `refund.net_amount` (both in your default currency).
* **Filters:** payment method, currency, customer cohort, region.
* **Common usage:** finance team's daily check; CFO's "are we trending?" question.

### Methods over time

The mix of payment methods used, by day or month, as a stacked area chart.

* **Useful for:** spotting growth in ACH or international rails; deciding whether to invest in a new method.
* **Filters:** date range, region.

### Routing report

Per-acquirer approval rate, in normal and degraded modes, plus the lift from [smart routing](../accept-payments/smart-routing.md) and any [failover](../accept-payments/failover.md) events.

* **Default view:** approval rate per acquirer, last 7 days.
* **Filters:** card brand, currency, BIN country.
* **Why it matters:** the headline number is "lift vs. baseline" — how many additional payments smart routing approved that wouldn't have approved on a single-acquirer setup.

### Decline reasons

Why declines happened, grouped by `decline_code`, with a sortable count column.

* **Default view:** last 30 days, sorted by count descending.
* **Useful for:** spotting `expired_card` clusters (set up account updater), `incorrect_zip` problems (review your AVS form), or sudden `do_not_honor` spikes (often an issuer-side incident).

### Top customers

Customers ranked by lifetime value, with a sortable column for refund rate, dispute rate, and last payment date.

* **Useful for:** support prioritization, churn analysis, and identifying the small slice of customers driving disputes.
* **Privacy note:** this report respects your retention policy — customers whose data has been auto-purged don't appear.

### Dispute report

Disputes opened, won, lost, and pending — per month, per reason code.

* **Default view:** last 6 months, all reason codes.
* **Useful for:** watching the dispute rate vs. the network's 1.0% threshold, and spotting reason-code patterns that indicate a systemic product or fulfillment issue.
* **Tied to:** [Disputes and chargebacks](../reconciliation/disputes.md).

### Cash position

Money in your Evolve balance now, money in your bank account from past payouts, money on the way (pending captures, in-flight payouts, held disputes).

* **Useful for:** "do we have enough to cover the upcoming payroll run?" type questions.
* **Filters:** currency.
* **Live updates:** balances refresh every 15 seconds.

### Reconciliation summary

A daily breakdown of payments, fees, refunds, and net to bank — designed to be the basis of your accounting close.

* **Output:** matches the structure of the [settlement file](../reconciliation/settlement-files.md), aggregated by day.
* **Useful for:** the daily reconciliation routine; finance team's first report of the day.

## Saving a customized view

If you load a standard report, change the filters or the date range to something you'll want again, click **Save as custom report**. It moves into your **Custom reports** tab and shows up at the top of the dashboard's report list.

See [Custom reports](custom-reports.md) for the full custom-report capabilities.

## Scheduling a report

Any standard or saved custom report can be scheduled to:

* Email a CSV to a list of recipients.
* Push a CSV to SFTP, S3, or GCS.
* Post a summary to Slack.

See [Sharing and scheduled exports](sharing-exports.md) for the configuration.

## Related

* [Custom reports](custom-reports.md) — building your own views.
* [Exporting to BI tools](exporting.md) — pushing the underlying data to your warehouse.
* [Settlement files](../reconciliation/settlement-files.md) — the source data for finance reports.
