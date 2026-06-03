---
description: Spot gaps in your documentation, and fix them automatically with GitBook Agent
hidden: true
icon: wrench
tags:
  - early-access
  - add-on
---

# Agent audit

{% hint style="warning" %}
**Agent audit is currently in early access**

We’re slowly rolling out access to agent audit. Stay tuned for more progress on the features below.
{% endhint %}

Agent audit helps you review documentation gaps the [GitBook Agent](what-is-gitbook-agent.md) identifies.

It highlights issues in your docs, explains why they matter, and helps you fix them through change requests.

To request access, open your site's **Settings**.

<figure><img src="../.gitbook/assets/25_03_30_site_findings@2x.png" alt=""><figcaption></figcaption></figure>

### How agent audit works

{% stepper %}
{% step %}
#### Review findings

Agent audit collects issues [GitBook Agent](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/gitbook-agent) has identified across your docs. The findings list helps you review these issues by topic, type, and severity.
{% endstep %}

{% step %}
#### Inspect a finding

Open any finding to review its details. Each finding includes a summary of the issue, the topic it belongs to, and supporting evidence from the pages GitBook used to detect it.
{% endstep %}

{% step %}
#### Fix or archive

Some findings can be fixed automatically by GitBook Agent. When that option is available, you can create [change requests](../collaboration/change-requests/) directly from the finding. You can also archive findings you don't want to keep in your active list.
{% endstep %}
{% endstepper %}

### **Findings list**

The **Findings** view shows the issues GitBook Agent has detected for your site. You can filter the list by **Type**, **Topic**, and **Severity** to focus on the findings you want to review first.

Each row shows the finding title and when GitBook identified it. Clicking a finding opens its full detail view.

### Findings details

When you open a finding, you can review its details and summary. This includes **Status**, **Severity**, **Type**, and **Topic**, followed by a description of the issue and why GitBook flagged it.

Some findings also include linked evidence pages so you can review the source material behind the finding. Each row shows the finding title and when GitBook identified it. Selecting a finding opens its full detail view.

### Automatic fixes

When a finding supports automatic fixes, GitBook shows a **Create change request** action so the GitBook Agent can generate a proposed fix for your team to review. To skip the suggestion, archive the finding instead.

### Scans

The **Scans** tab gives you a separate view of scan activity for your site. Use it to review the scans GitBook runs as part of agent audit.
