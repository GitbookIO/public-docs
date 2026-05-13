---
icon: slack
description: Real-time alerts for disputes, refunds, and platform events. Slash commands for lookups.
---

# Slack

The Evolve Slack app sends real-time alerts to channels you pick and exposes slash commands for looking up customers, charges, and verification sessions without leaving Slack. Most teams install it once at platform launch and tweak the alert routing as needs evolve.

## What you can do

* **Get alerted** on disputes, large refunds, failed payouts, and account requirements changes.
* **Look up** a customer or charge by ID, email, or amount with `/evolve` slash commands.
* **Approve** Connect actions (manual reviews, payout releases) directly from Slack.
* **Schedule** daily and weekly digest summaries to a channel.

## Install

{% stepper %}
{% step %}

### Install the Slack app

In your Evolve dashboard, **Settings → Integrations → Slack → Install**. You'll be redirected to Slack to authorize the app for your workspace. Pick the workspace and click **Allow**.

{% endstep %}

{% step %}

### Pick the default channel

Pick a channel for general Evolve notifications. Most teams create a dedicated `#evolve-alerts` channel for this. The bot needs to be invited to any channel you want to send notifications to — the install flow does this automatically for the default channel; for additional channels, run `/invite @evolve` in the channel.

{% endstep %}

{% step %}

### Configure alerts

The default install enables the most common alerts (disputes, failed payouts). To customize which events go where, see [Configuring alerts](configuring-alerts.md).

{% endstep %}
{% endstepper %}

## Slash commands

Once installed, anyone in your workspace with access to the channel can use:

| Command | What it does |
| --- | --- |
| `/evolve customer cus_123` | Show a customer's record, recent charges, balance |
| `/evolve charge ch_123` | Show a charge with its full timeline |
| `/evolve search jordan@acme.com` | Search across customers, charges, verifications |
| `/evolve dispute dp_123` | Show a dispute and let you upload evidence |
| `/evolve verify vs_123` | Show a verification session and its check results |
| `/evolve help` | Full list of commands |

Slash command results are visible only to the user who ran them — they're not posted to the channel.

## Permissions

The Slack app uses scoped permissions:

* **Read** — anyone in a channel where Evolve is installed can see incoming alerts and run lookup slash commands.
* **Approve** — only members of your **#evolve-approvers** group (configurable) can approve manual reviews or release held payouts.

The mapping between Slack users and Evolve dashboard users is automatic when the email matches. For Slack users without matching dashboard accounts, slash commands return a "no access" message rather than data.

## Last reviewed

This page was last reviewed in early 2026. Doc updates flow through change requests in the [evolve-pay/docs repo](https://github.com/GitbookIO/evolve-demo) — open one if anything here is out of date.

## Related

* [Configuring alerts](configuring-alerts.md) — picking which events go where.
* [Webhooks](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/) — the underlying event source.
* [Disputes at scale](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/marketplace/disputes-at-scale) — the most-common dispute-routing pattern.
