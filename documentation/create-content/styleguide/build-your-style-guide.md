---
description: >-
  Choose a starting point, fill in the template, and write rules that GitBook
  Agent can enforce.
---

# Build your style guide

Most teams start from a template and keep their style guide on a single page. This page covers choosing a starting point, filling in the template, and writing rules that GitBook Agent can enforce.

To set up a style guide, you need admin permissions on the site.

## Choose a starting point

To start, click **Style guide** in your site's sidebar, then click **Set up**. Then choose a starting point:

| Starting point              | Choose it when                                                                                                                                                     |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **A template**              | You don't have a style guide yet.                                                                                                                                  |
| **An existing style guide** | Another site in your organization already uses the style guide you want. See [Use an existing style guide](build-your-style-guide.md#use-an-existing-style-guide). |
| **An import**               | You keep a style guide in another tool or publish it online. See [Import a style guide](build-your-style-guide.md#import-a-style-guide).                           |

GitBook offers three templates:

<table><thead><tr><th width="204.75390625">Template</th><th>Best for</th></tr></thead><tbody><tr><td><strong>Starter template</strong></td><td>Defining your own voice and rules from scratch. Each section explains what belongs there, and you write the rules yourself.</td></tr><tr><td><strong>Google style guide</strong></td><td>Clear, precise, and professional writing for a developer audience. Generated from the Google developer documentation style guide.</td></tr><tr><td><strong>Microsoft style guide</strong></td><td>Warm, simple, and human writing for a broad audience, including readers who aren't technology experts. Generated from the Microsoft Writing Style Guide.</td></tr></tbody></table>

The Google and Microsoft templates come with enforceable rules from their source guides, covering voice, word lists, grammar, formatting, procedures, accessible writing, and inclusive language. Everything in a template is yours to edit.

{% hint style="info" %}
GitBook updates its templates when the source guides change. Updates apply to new style guides only. A style guide you've already created doesn't change.
{% endhint %}

## Fill in the template

Each template is a single page, organized into sections such as voice and tone, word list, grammar, formatting, and procedures. Each section explains what belongs in it. Delete any section you don't need.

Every template marks the parts you must customize with a **Needs your input** hint. Work through each one before you run your first check. They typically include:

* The snapshot date of the base guide version the template reflects (Google and Microsoft templates)
* Your product name and documentation mission
* Who reads and writes your documentation, and what the guide covers
* Your product names, feature names, and any terms your team debates, added to the word list
* An owner, a review cadence, and how to propose changes
* A first entry in the decision log, which records why your team settled on a rule or departed from the base guide

Everything without a hint is ready to use as-is. Rules that still contain placeholder text are inactive until you fill them in.

## Write rules the Agent can enforce

GitBook Agent enforces rules that have a numbered ID, and definite rules like "Never use semicolons". It treats everything else, such as a description of your voice, as guidance and offers it only as suggestions. For details, see [How GitBook Agent enforces your style guide](how-gitbook-agent-enforces-your-style-guide.md#which-rules-the-agent-enforces).

The templates write rules as a table, with an ID, the rule, an example of each side, and any exceptions:

| ID    | Rule              | Do                              | Don't                               | Exception                                                                                |
| ----- | ----------------- | ------------------------------- | ----------------------------------- | ---------------------------------------------------------------------------------------- |
| SG-12 | Use present tense | ✅ "The command creates a file." | ❌ "The command will create a file." | Future tense for events that are actually in the future ("Support for v2 ends in March") |

When you write or edit rules:

* **Give every rule you want enforced an ID.** Use the next number after the current highest, wherever the rule lives. Never renumber or reuse an ID, because past flags and your decision log refer to it.
* **Keep one rule per ID.** A rule that checks one thing produces flags that are easy to act on.
* **List exceptions.** The Agent doesn't flag text that falls under a rule's exception.
* **Turn checkable guidance into rules.** Keep your voice description as guidance, and write anything you can check, such as "No exclamation points in body text", as a numbered rule.
* **Replace every placeholder.** A rule that still contains bracketed text, like `[Product name]`, isn't enforced.

{% hint style="info" %}
The Starter template uses the `SG-` prefix for IDs. You can change it, but keep it the same once you start using the guide.
{% endhint %}

## Keep your main rules on the first page

One page is enough for most style guides. GitBook Agent loads the first page on every task, so the rules there always apply.

If your style guide grows long, move the detailed rules for one topic, such as a long word list or your content types, to their own page with a clear title. The Agent reads that page whenever a task touches its topic. Keep your core rules on the first page.

## Use an existing style guide

If your organization already uses style guides on other sites, they appear at the top of the setup screen, along with the sites that use them. When you choose one, you can:

* **Use it as-is:** share it with the other sites that use it. Edits apply everywhere it's used.
* **Fork it:** create a copy for this site, named `Style guide - {site name}`, that you can change independently.

## Import a style guide

To import a style guide you keep in another tool:

1. On the setup screen, click **Upload a file**.
2. Drop your Markdown, HTML, DOCX, or ZIP files, or browse to choose them.
3. Optionally, enable **Enhance import with AI** to clean up the imported content.
4. Click **Start import**.

To import a style guide that's published online:

1. On the setup screen, click **Import from a URL**.
2. Enter the link to the style guide.
3. Optionally, enable **Enhance import with AI** to clean up the imported content.

GitBook imports all public pages under the URL you enter, up to 200 pages. For example, importing `website.com/docs/` includes `website.com/docs/article` but not `website.com/other-parent/page`. For larger sites, import smaller sub-paths separately.

An imported style guide often spans many pages and has rules without IDs. Before you run your first check:

1. Move your core rules to the first page.
2. Give each rule you want enforced an ID, using one prefix for the whole guide.
3. Write down any rule you rely on from another guide. The Agent enforces only what's written in your style guide.

## Before your first check

Your style guide is ready when:

* Every **Needs your input** section is filled in, and no rule still contains placeholder text.
* Your product names and settled terms are in the word list.
* Every rule you want enforced has an ID.
* Your core rules are on the first page.

Then [check your content against your style guide](check-content-against-your-style-guide.md).
