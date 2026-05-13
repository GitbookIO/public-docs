---
icon: bell
description: Decide which Evolve events fire alerts, where they go, and at what threshold.
---

# Configuring alerts

In **Settings → Integrations → Slack → Alerts**, you'll find the alert configuration. The default install enables a sensible starter set; most teams tune it within the first two weeks.

## Alert types

| Alert | Default channel | Threshold |
| --- | --- | --- |
| **Dispute opened** | `#evolve-alerts` | Always |
| **Large refund** | `#evolve-alerts` | Over $1,000 |
| **Payout failed** | `#evolve-alerts` | Always |
| **Risk hold placed** | `#evolve-alerts` | Always |
| **Account verification required** | `#evolve-alerts` | Always |
| **Connect: seller restricted** | `#evolve-alerts` | Always |
| **Daily summary** | (off) | n/a |
| **Weekly summary** | (off) | n/a |

Each alert can be:

* **Enabled or disabled** entirely.
* **Routed** to a different channel (any channel `@evolve` is invited to).
* **Filtered** by amount, country, or seller (where applicable).

## Routing patterns

A few patterns most teams use:

{% columns %}
{% column width="50%" %}

### <i class="fa-bell" style="color:$primary;">:bell:</i> Single channel

All Evolve alerts to one channel. Simplest. Fine for teams under 10 people.

{% endcolumn %}

{% column width="50%" %}

### <i class="fa-route" style="color:$primary;">:route:</i> By function

`#finance-alerts` for payouts and disputes; `#support-alerts` for verifications and seller issues; `#eng-alerts` for webhook delivery failures.

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column width="50%" %}

### <i class="fa-globe" style="color:$primary;">:globe:</i> By region

Multi-region operations route alerts to per-region channels — `#evolve-us-alerts`, `#evolve-eu-alerts`, etc. Filter rules use the country on each event.

{% endcolumn %}

{% column width="50%" %}

### <i class="fa-circles-overlap" style="color:$primary;">:circles-overlap:</i> Per-seller (Connect)

For platforms running Connect, route per-seller alerts to a channel shared with that seller (via Slack Connect). The seller sees their own disputes and payouts; you see all of them.

{% endcolumn %}
{% endcolumns %}

## Threshold tuning

For teams getting too many alerts, raise the thresholds:

* **Large refund threshold** — default $1,000. Raise to $5,000 if you process high-value transactions; below this won't fire.
* **Volume-spike alert** — fires when daily volume exceeds the rolling 30-day average by 50%. Useful for catching account compromise but noisy during sales events.

For the inverse problem (missing important alerts), check that your channel has the bot invited and that the filters aren't excluding the events you care about.

## Daily and weekly summaries

In addition to per-event alerts, Evolve can post scheduled digests to a channel:

* **Daily summary** — yesterday's volume, top customers, dispute rate. Posts at 9am in your account timezone.
* **Weekly summary** — past 7 days of metrics, week-over-week deltas, anomalies. Posts Monday morning.

Most teams enable the weekly summary in `#all-hands` or similar. Daily summary is more for finance / ops.

## Customizing the message format

The default alert messages are designed to be readable at a glance. To customize per-alert format (add fields, change the layout, attach metadata), use the **Custom alert templates** feature under **Settings → Integrations → Slack → Templates**.

Templates use a [block-kit-style format](https://api.slack.com/block-kit) with Evolve event variables. Most teams don't need to customize, but it's there if you want to add internal context (order ID, account manager name) to each alert.

## Pausing alerts during incidents

In an incident, you may want to pause Evolve alerts to avoid noise. Run `/evolve pause 1h` in any channel with the bot — that channel's alerts are paused for an hour. `/evolve resume` to bring them back.

The pause is per-channel and per-user; admins can also pause workspace-wide via the dashboard.

## Last reviewed

Reviewed in early 2026, with quarterly updates as new alert types ship. Suggest an alert type via [a change request on the docs repo](https://github.com/GitbookIO/evolve-demo).

## Related

* [Slack overview](README.md) — install and slash commands.
* [Webhooks event catalog](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/event-catalog) — the underlying event types these alerts surface.
