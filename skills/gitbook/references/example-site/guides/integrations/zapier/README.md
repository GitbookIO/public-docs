---
icon: bolt-lightning
description: Wire Evolve events to 6,000+ apps without writing code.
---

# Zapier

The Evolve Zapier integration lets you connect Evolve to anything Zapier supports — Google Sheets, Mailchimp, Notion, Airtable, Salesforce, you name it. Triggers fire when Evolve events happen; actions let you create Evolve records from other apps.

This is the right path when:

* You don't have engineering bandwidth to build a webhook integration.
* The tool you want to connect to is already in Zapier's catalog.
* The volume is reasonable (Zapier's free tier covers 100 tasks/month; paid plans go up from there).

For high-volume integrations, build directly against [webhooks](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/) — Zapier's per-task pricing adds up fast.

## Connect Evolve in Zapier

{% stepper %}
{% step %}

### Authenticate

In Zapier, search for "Evolve" and click **Connect**. You'll be asked for your Evolve API key — paste a [restricted key](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/authentication#restricted-keys) scoped to read-only or to the specific operations the Zap will perform.

For most Zaps, **Read-only** is enough. For Zaps that create or refund charges, scope to the specific resources.

{% endstep %}

{% step %}

### Pick a trigger

Zaps start with a trigger — an event in Evolve that kicks the Zap off. The full list is on [Triggers and actions](triggers-and-actions.md). Common starting points:

* **New charge succeeded** — for tracking sales in a spreadsheet.
* **New dispute opened** — for routing to a support tool like Intercom.
* **New customer created** — for syncing to a CRM.

{% endstep %}

{% step %}

### Add downstream actions

After the trigger, chain whatever Zapier supports. Examples:

* New charge → append to Google Sheets.
* New dispute → create a Notion task.
* New customer → add to Mailchimp.
* Failed payout → send Slack DM to the finance team.

{% endstep %}

{% step %}

### Test and turn on

Zapier's **Test** step pulls a real recent event from your Evolve test mode and runs the Zap. Verify the downstream action looks right. When you turn the Zap on, it starts processing live events.

{% endstep %}
{% endstepper %}

## Live mode vs test mode

The API key you connect determines which mode the Zap reads from. Use a `sk_test_*` key during build-out; swap to `sk_live_*` when ready. Most teams keep two Zaps in parallel — one against test for development, one against live for production.

## Common Zap recipes

A handful of patterns worth copying:

| Recipe | Trigger | Action |
| --- | --- | --- |
| **Sales tracker** | Charge succeeded | Append row to Google Sheets |
| **Dispute alerter** | Dispute opened | Create Linear issue |
| **CRM sync** | Customer created | Create HubSpot contact |
| **Refund logger** | Refund created | Post to Slack #refunds |
| **Onboarding email** | Connect account verified | Send Mailchimp welcome email |

## Limits

* Zapier's free tier: 100 tasks/month, 5 Zaps active at once. Fine for prototyping; you'll outgrow it.
* Zapier's paid tiers handle 10,000+ tasks/month if you need them.
* Zapier polls our API every 1–15 minutes depending on plan, so triggers aren't real-time. For sub-second reactivity, use webhooks.

## Last reviewed

Last reviewed in early 2026. Zapier's catalog of supported triggers and actions is occasionally updated; suggest additions via [change request](https://github.com/GitbookIO/evolve-demo).

## Related

* [Triggers and actions](triggers-and-actions.md) — the full catalog.
* [Webhooks](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/) — for the engineering-driven path.
* [Authentication → Restricted keys](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/authentication#restricted-keys) — the right key shape for Zapier.
