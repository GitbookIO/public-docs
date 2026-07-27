---
description: Ask GitBook Agent to audit your docs for gaps and inconsistencies.
---

# Run an Agent audit

{% hint style="warning" %}
This feature is in early access, and access is rolling out gradually.
{% endhint %}

GitBook Agent can identify issues in your documentation — content gaps, outdated pages, and incorrect information — and suggest or implement fixes.

### What can GitBook Agent detect?

* **Content gaps** — users ask questions the docs struggle to answer. For example, a customer asking support a question that isn't in the docs, or an API endpoint with incomplete documentation.
* **Outdated content** — a page has been superseded by information from an external source. For example, an SDK update that changed a function's signature, or a paid feature that moved to the free tier without a docs update.
* **Incorrect content** — content that's explicitly wrong. For example, a guide pointing to APIs that no longer exist or have been sunset, or external sources (like your marketing site) disagreeing with the docs.

### How identification works

{% stepper %}
{% step %}
#### Connect sources

Agent works best connected to external sources — your support ticketing system, public forums, or marketing website. Some sources need an API key or additional authentication. See [Connect knowledge sources](../assistant/knowledge-sources.md).
{% endstep %}

{% step %}
#### Agent generates findings

GitBook regularly reviews your sources and generates findings, collected for your team to review.
{% endstep %}

{% step %}
#### Review your findings

Each finding includes a summary of the issue, the topic it belongs to, supporting evidence, and links to the pages Agent used as context.
{% endstep %}

{% step %}
#### Fix or archive

Some findings can be fixed automatically. When available, create a [change request](../../collaboration/change-requests/README.md) directly from the finding — or archive findings you don't want to act on. GitBook won't re-open an archived finding.
{% endstep %}
{% endstepper %}

To request access to Agent's automatic documentation improvement features, open your site's **Settings**.

### Automatic fixes

When a finding supports an automatic fix, GitBook shows a **Create change request** action, so Agent can generate a proposed fix for your team to review. To skip a suggestion, archive the finding instead.

You can also act on a single gap directly from the Insights dashboard — see [Fix gaps with GitBook Agent](../../analytics/insights/fix-gaps-with-agent.md).
