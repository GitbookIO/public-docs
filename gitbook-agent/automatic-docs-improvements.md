---
description: >-
  Identify incorrect and outdated pages in your documentation, push them to a
  triage queue, and fix them automatically with GitBook Agent
icon: magnifying-glass-plus
tags:
  - early-access
---

# Automatic docs improvements

{% hint style="warning" %}
**This feature is currently in early access.**

We’re slowly rolling out access. Stay tuned for more progress on the features below.
{% endhint %}

GitBook Agent can identify issues in your documentation — such as content gaps, outdated pages, and incorrect information — and suggest and implement improvements.

## What can GitBook Agent detect?

* **Content gaps** occur when GitBook sees users asking questions about your product that the docs struggle to answer, such as:
  * a customer asking a question to your support team that they couldn’t find on the docs.
  * an API endpoint missing complete documentation.
* **Outdated content** is detected when the content on your page has been superseded by content found in an external source, such as:
  * an SDK update that changed the signature of a function.
  * a paid feature that moved to the free tier, where the docs haven’t been updated.
* **Incorrect content** is flagged when the content on the docs site is explicitly wrong, such as:
  * a guide pointing to APIs that do not exist anymore, or where the feature has been sunsetted.
  * external sources such as your marketing website disagreeing with the documentation.

## How identification works

{% stepper %}
{% step %}
#### Connect sources

GitBook Agent works best when it’s connected to external sources like your support ticketing system, public forums, or marketing website. Some sources require an additional API key or authentication before setup is complete. [Learn more about our connections.](../ai-and-search/connections/)
{% endstep %}

{% step %}
#### GitBook Agent generates findings

GitBook regularly reviews your sources and generates findings based on the results. These findings are automatically pushed into your triage queue. [Learn more about how we ingest data.](../ai-and-search/connections/)
{% endstep %}

{% step %}
#### Review your triage queue

Open the **Triage** queue to start fixing issues. Each finding includes a summary of the issue, the topic it belongs to, supporting evidence, and links to the pages GitBook used as context.
{% endstep %}

{% step %}
#### Fix or archive

Some findings can be fixed automatically by GitBook Agent. When that option is available, you can create [change requests](../collaboration/change-requests/) directly from the finding. You can also archive findings you don’t want to keep in your active list.
{% endstep %}
{% endstepper %}

To request access to GitBook Agent’s automatic documentation improvement features, open your site’s **Settings**.

<figure><img src="../.gitbook/assets/2026-07-13_connections@2x.png" alt=""><figcaption></figcaption></figure>

## Triage

The **Triage** view shows the **findings** GitBook Agent has detected for your site. You can filter the list by **Topic** and **Severity** to focus on the findings you want to review first.

Each row shows the finding title and when GitBook identified it. Clicking a finding opens its full detail view.

### Triage details

When you open an item in Triage, you can review its details and summary. This includes **Status**, **Severity**, **Type**, and **Topic**, followed by a description of the issue and why GitBook flagged it.

Some findings also include linked evidence pages so you can review the source material behind the finding. Each row shows the finding title and when GitBook identified it. Selecting a finding opens its full detail view.

### Automatic fixes

When a finding supports automatic fixes, GitBook shows a **Create change request** action so the GitBook Agent can generate a proposed fix for your team to review. To skip the suggestion, archive the finding instead. GitBook won’t re-open findings that you’ve archived.
