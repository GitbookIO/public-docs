---
icon: puzzle-piece
description: Connect Evolve to the tools you already use — Slack, Zapier, Segment, QuickBooks, NetSuite.
cover: .gitbook/assets/integrations-cover.png
coverY: 0
layout:
  width: wide
  tableOfContents:
    visible: false
---

# Integrations

{% columns %}
{% column width="50%" %}
Evolve plugs into the tools your team already uses. Five officially-supported integrations cover the four jobs most teams need first — alerts, automation, customer-data routing, and accounting.
{% endcolumn %}

{% column width="50%" %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

Each integration is its own **page group** (Slack, Zapier, Segment, QuickBooks, NetSuite). Doc updates flow through **change requests** on GitHub — see the [evolve-pay/docs repo](https://github.com/GitbookIO/evolve-demo) for open PRs and the "Coming soon" section below for integrations being designed in the open right now.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

## Featured: Slack

The most-installed integration on Evolve. Real-time alerts for disputes, refunds, and platform events; slash commands for looking up customers and charges without leaving Slack; per-channel routing rules so finance, ops, and engineering only see what they care about.

Most teams install Slack on day one and then add others as needs grow.

<p><a href="slack/README.md" class="button primary">Set up Slack</a> <a href="slack/configuring-alerts.md" class="button secondary">Configure alerts</a></p>

## Browse by job

### <i class="fa-bell" style="color:$primary;">:bell:</i> Real-time alerts and automation

Get notified when something happens, or trigger downstream actions in other tools.

* **[Slack](slack/README.md)** — channel-based alerts plus `/evolve` slash commands.
* **[Zapier](zapier/README.md)** — wire Evolve events to 6,000+ apps without writing code.

### <i class="fa-circle-nodes" style="color:$primary;">:circle-nodes:</i> Customer data

Stream Evolve activity into your data infrastructure.

* **[Segment](segment/README.md)** — Evolve as a source (event stream) or destination (customer-record updates).

### <i class="fa-calculator" style="color:$primary;">:calculator:</i> Accounting

Auto-create journal entries from settlements; sync customer records to your books.

* **[QuickBooks](quickbooks/README.md)** — Online and Desktop. Mapping per chart of accounts.
* **[NetSuite](netsuite/README.md)** — multi-subsidiary, custom segments, multi-currency.

## Coming soon

In active development. Each is being designed in the open via a GitHub pull request — comment to influence the design or sign up as a beta tester.

| Integration | What it does | Change request |
| --- | --- | --- |
| **HubSpot** | Sync Evolve customers to HubSpot contacts. | [PR #142](https://github.com/GitbookIO/evolve-demo) |
| **Pipedrive** | Evolve charges as Pipedrive deal events. | [PR #156](https://github.com/GitbookIO/evolve-demo) |
| **Xero** | Like QuickBooks, for Xero customers. | [PR #161](https://github.com/GitbookIO/evolve-demo) |

## Don't see what you need?

For tools not on this list, two paths:

* **Zapier**, if your tool integrates with it. [Our Zapier integration](zapier/README.md) is the fastest path — no engineering required.
* **Build your own**, against the [Webhooks API](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/). A few dozen lines of code wires Evolve to almost anything; the [tutorials](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/) cover common patterns.
