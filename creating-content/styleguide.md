---
description: >-
  Define your team's writing rules in a dedicated styleguide space, and keep
  every contributor — human or GitBook Agent — consistent
icon: pen-ruler
---

# Styleguide

A styleguide is a dedicated space that holds your team's writing rules and conventions. It's the single source of truth for how content on your site should be written — tone, terminology, formatting, and structure.

A styleguide serves two audiences:

* **Your team** — writers and reviewers have one shared reference for how to write, so documentation stays consistent no matter who edits it.
* **GitBook Agent** — the Agent reads your styleguide and treats it as the source of truth it must follow whenever it generates or edits content. It overrides the Agent's own defaults and general writing conventions.

{% hint style="info" %}
**Styleguides are in early access**

The styleguide feature is rolling out gradually. If you don't see it yet in your site settings, it isn't enabled for your organization.
{% endhint %}

### Create a styleguide

Open your site's **Settings** and choose the **Styleguide** section. If your site doesn't have a styleguide yet, you can create one in a few ways:

{% tabs %}
{% tab title="Blank" %}
Start from an empty space and write your rules from scratch.
{% endtab %}

{% tab title="Starter template" %}
Start from a built-in template that already covers voice and tone, writing principles, formatting, and terminology. Adapt each section to your team — treat it as a starting point, not a rule book set in stone.
{% endtab %}

{% tab title="Import" %}
Import existing content — for example, a styleguide you already keep in another tool — into the new styleguide space.
{% endtab %}
{% endtabs %}

The first time you open a styleguide, GitBook shows a short intro explaining that you edit it like any other space.

### What to put in your styleguide

A styleguide is most useful when it captures the decisions that are easy to get wrong or inconsistent across a team. Common sections include:

* **Voice and tone** — how you address the reader, how formal or friendly you are.
* **Writing principles** — tense, active vs. passive voice, sentence and paragraph length.
* **Formatting** — heading case, when to use lists, steppers, hints, and other blocks.
* **Terminology** — product and feature names, preferred terms, how to handle acronyms.

{% hint style="warning" %}
**Put your main rules on the first page**

GitBook Agent loads your styleguide's **first page in full** into its context on every task, so that page always drives its work. It reads other pages only on demand, using the table of contents. Keep your most important rules on the first page, and use additional pages for detail the Agent can pull in when relevant.
{% endhint %}

### Edit a styleguide

A styleguide is a space, so you edit it the same way you edit the rest of your documentation:

* **In GitBook** — make your changes in a [change request](../collaboration/change-requests/), then merge them when you're ready.
* **With Git Sync** — if the styleguide space is [synced to GitHub or GitLab](../getting-started/git-sync/), edit it as markdown in your repository.

To open your styleguide, use the **Styleguide** entry in your site's sidebar, or the **Edit** action in **Site settings → Styleguide**.

### Share a styleguide across sites

A styleguide belongs to your organization, so several sites can rely on the same one. When you set up the styleguide for a site that doesn't have one yet, and your organization already has styleguides, you can:

* **Use an existing styleguide** — attach it as-is, shared with the other sites that use it. Edits apply everywhere it's used.
* **Fork it** — create a dedicated copy for this site (named `Styleguide - {site name}`) that you can evolve independently.

To see every styleguide in your organization and which sites use each one, open the **Styleguides** entry in your organization sidebar.

### Detach a styleguide

To stop a site from using its styleguide, open **Site settings → Styleguide** and choose **Detach**. Detaching keeps the styleguide space — it may still be used by other sites. If no other site references it, GitBook offers to delete it permanently.

### How GitBook Agent uses your styleguide

Whenever GitBook Agent writes or edits content on a site, it reads that site's styleguide and follows it as the source of truth. In practice:

* On every change request task, the Agent loads the styleguide's **first page** and its table of contents up front, then pulls in other sections as needed.
* You can ask the Agent to check a page against your styleguide directly, using **Check consistency against styleguide** in the [Improve menu](../gitbook-agent/write-and-edit-with-ai.md#improve-page-content-with-gitbook-agent).

{% hint style="info" %}
A styleguide complements the site-level [custom instructions](../gitbook-agent/what-is-gitbook-agent.md#add-a-style-guide-and-custom-instructions) you can give GitBook Agent. Custom instructions are short, site-specific directions; a styleguide is a full, shared document of your writing rules.
{% endhint %}
