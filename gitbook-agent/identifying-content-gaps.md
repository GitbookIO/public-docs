---
description: >-
  Spot gaps in your documentation, push them to a Triage queue, and fix them
  automatically with GitBook Agent
icon: magnifying-glass-plus
tags:
  - early-access
---

# Identify content gaps

{% hint style="warning" %}
**This feature is currently in early access:**

We’re slowly rolling out access. Stay tuned for more progress on the features below.
{% endhint %}

GitBook Agent can identify gaps in your documentation - pages where content could be improved to better respond to user questions.

To request access, open your site's **Settings**.

<figure><img src="../.gitbook/assets/25_03_30_site_findings@2x.png" alt=""><figcaption></figcaption></figure>

### How identification works

{% stepper %}
{% step %}
#### Connect sources

The Agent works best when it's connected to external sources. Most content gaps show up in conversations users have with your support team — so connecting to support ticketing systems like [Intercom](../ai-and-search/connections/intercom.md) or [Zendesk](../ai-and-search/connections/zendesk.md) and discussion forums gives the best results.
{% endstep %}

{% step %}
#### GitBook Agent generates findings

We regularly watch your sources and generate findings based on what we see. We push these findings into your Triage queue.
{% endstep %}

{% step %}
#### Go through your Triage queue

Open the Triage queue to start fixing issues. Each finding includes a summary of the issue, the topic it belongs to, and supporting evidence from the pages GitBook used to detect it.
{% endstep %}

{% step %}
#### Fix or archive

Some findings can be fixed automatically by GitBook Agent. When that option is available, you can create [change requests](../collaboration/change-requests/) directly from the finding. You can also archive findings you don't want to keep in your active list.
{% endstep %}
{% endstepper %}

### **Triage list**

The **Triage** view shows the **findings** GitBook Agent has detected for your site. You can filter the list by **Topic**, and **Severity** to focus on the findings you want to review first.

Each row shows the finding title and when GitBook identified it. Clicking a finding opens its full detail view.

### Triage details

When you open an item in Triage, you can review its details and summary. This includes **Status**, **Severity**, **Type**, and **Topic**, followed by a description of the issue and why GitBook flagged it.

Some findings also include linked evidence pages so you can review the source material behind the finding. Each row shows the finding title and when GitBook identified it. Selecting a finding opens its full detail view.

### Automatic fixes

When a finding supports automatic fixes, GitBook shows a **Create change request** action so the GitBook Agent can generate a proposed fix for your team to review. To skip the suggestion, archive the finding instead.
