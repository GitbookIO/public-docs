---
description: >-
  Define your team's writing rules in a dedicated style guide and keep every
  contributor, human or GitBook Agent, consistent.
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
tags:
  - tag: new
    primary: true
---

# Style guide

A style guide holds your team's writing rules: voice and tone, terminology, formatting, and structure. It serves two audiences:

* **Your team:** writers and reviewers share one reference, so documentation stays consistent no matter who edits it.
* **GitBook Agent:** the Agent follows your style guide whenever it writes, edits, or reviews content. Your rules override its own defaults.

GitBook Agent enforces rules that have a numbered ID or are definite and checkable, and treats the rest as guidance. For details, see [How GitBook Agent enforces your style guide](how-gitbook-agent-enforces-your-style-guide.md).

## Get started

To set up a style guide, you need admin permissions on the site.

{% stepper %}
{% step %}
**Set up a style guide**

Click **Style guide** in your site's sidebar, then click **Set up**. Start from a template, reuse a style guide your organization already has, or import your own. See [Choose a starting point](build-your-style-guide.md#choose-a-starting-point).
{% endstep %}

{% step %}
**Fill in the template**

Work through each section marked **Needs your input**, such as your product name, audience, and word list, and give every rule you want enforced an ID. See [Build your style guide](build-your-style-guide.md).
{% endstep %}

{% step %}
**Run your first check**

Open your style guide, go to the **Checks** tab, and click **Run a check** to review existing content. You can also request a style guide review on your next change request. See [Check content against your style guide](check-content-against-your-style-guide.md).
{% endstep %}
{% endstepper %}

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Build your style guide</strong></td><td>Choose a starting point, fill in the template, and write rules the Agent can enforce</td><td><a href="build-your-style-guide.md">build-your-style-guide.md</a></td></tr><tr><td><strong>Check content against your style guide</strong></td><td>Review a page, a change request, or whole spaces</td><td><a href="check-content-against-your-style-guide.md">check-content-against-your-style-guide.md</a></td></tr><tr><td><strong>How GitBook Agent enforces your style guide</strong></td><td>What the Agent reads, flags, and changes</td><td><a href="how-gitbook-agent-enforces-your-style-guide.md">how-gitbook-agent-enforces-your-style-guide.md</a></td></tr></tbody></table>

## Edit your style guide

Click **Style guide** in your site's sidebar to open your style guide. You edit it like the rest of your documentation: make your changes in a change request, then merge them.

## Share a style guide across sites

A style guide belongs to your organization, so several sites can use the same one and follow the same rules.

After you create a style guide, GitBook offers to link it to any other sites in your organization that don't have one yet. You can also choose an existing style guide, shared or forked, when you set one up for a site.

To see every style guide in your organization and the sites that use each one, open **Style guides** in your organization sidebar.

### Detach a style guide

To stop a site from using its style guide, open the actions menu next to **Style guide** in your site's sidebar and click **Detach style guide**. Detaching keeps the style guide, since other sites may still use it. If no other site uses it, GitBook offers to delete it permanently.
