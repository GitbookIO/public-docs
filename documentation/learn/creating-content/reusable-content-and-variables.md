---
description: Reuse blocks across pages and personalize content with variables and expressions.
---

# Reusable content and variables

## Reusable content

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Reusable content syncs a block (or blocks) across multiple pages and sections — edit any instance, and every instance updates.

### Fundamentals

Reusable content works like any other content: modify it via change requests, include it in review workflows, and it renders correctly on any published site. It can be referenced across multiple sections, but belongs to a single **parent section** — the only place it can be edited.

Even though updates appear instantly everywhere it's used, every change must originate from the parent section, as a direct edit or a change request. GitBook enforces permission-based editing, so reusable content can only change from its parent — editing rights are respected even when the content is reused across the organization.

**Known limitations:**

* **Integrations** — blocks from integrations aren't supported in reusable content. Integrations install per section, so limiting them this way keeps third-party integrations scoped to the permissions you grant — referencing reusable content across sections would break that boundary.
* **Search** — reusable content currently only appears in search results within its parent section (this limitation is being worked on).

### In the app

**Create reusable content** — select one or more blocks, open the Actions menu, choose **Turn into** → **Reusable content**, and optionally name it. Or select the blocks and press ⌘+C, which prompts you to create reusable content.

**Insert reusable content** — press `/` on an empty line, or click the `+` beside any block. The reusable-content picker lists blocks from your current section — use the section selector to browse content from another section you can access, then search by name and select it. Inserting from another section doesn't transfer ownership — only the parent section can edit it, and its updates keep syncing everywhere.

**Edit reusable content** — edit any instance directly (if live edits are enabled) or through a change request. Changes sync everywhere the content is used, taking effect once a change request merges.

**Detach reusable content** — open the Actions menu and select **Detach** to convert it back to regular blocks. Once detached, it no longer syncs with other instances, which remain synced together.

**Delete reusable content** — find it in the page's table of contents, open its Actions menu, and select **Delete**.

{% hint style="warning" %}
Deleting reusable content removes it from every page it's used in. This can't be undone.
{% endhint %}

### Syncing with GitHub & GitLab

Reusable content exports to a dedicated `includes` folder when Git Sync'd, one Markdown file per piece of content, referenced from other pages via the `include` directive:

```markdown
{% include "../../.gitbook/includes/reusable-block.md" %}
```

{% hint style="info" %}
The `.gitbook/includes` directory is created at the root of each synced section (which may not be the repository root). If it appears in your table of contents, hide it manually.
{% endhint %}

{% hint style="success" %}
Writing on the GitHub side? Make sure the path to the include is relative to the file containing the reference, not the repository root.
{% endhint %}

## Variables

Variables create reusable text you can reference conditionally in [expressions](#expressions) and in [conditions for adaptive content](../access/write-content-conditions.md#the-condition-editor). If you repeat the same name, phrase, or version number throughout your content, a variable keeps every instance in sync — useful for values you might update later, or that are easy to mistype.

Variables can be scoped to a single page or a single section.

### Create a new variable

Open **Library** in the table of contents while editing an open [change request](../collaboration/change-requests/README.md), then click **Variables**. Use the toggle to view or create variables scoped to the current page or the whole section, click **Create a variable**, name it, give it a value, and click **Add variable**.

{% hint style="info" %}
Variable names must start with a letter, and can contain letters, numbers, and underscores.
{% endhint %}

### Use variables in your content

Reference variables inside an [expression](#expressions), inserted inline. After inserting one, double-click to open the expression editor.

{% hint style="info" %}
Expressions only work in a document's page content — not in page titles or page metadata.
{% endhint %}

Page-scoped variables are accessible under `page.vars`; section-scoped variables under `space.vars`.

{% hint style="info" %}
In expressions, section-scoped variables live under `space.vars` — the GitBook API represents sections as `space` objects.
{% endhint %}

### Update a variable

Update a variable's value from within a change request — every expression referencing it updates too. The change goes live once the change request merges.

## Expressions

Expressions dynamically display content defined in a variable. Insert one from the `/` menu — clicking an inserted expression opens the expression editor, where you can reference a variable and [conditionally format](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator) it.

Expressions are also how you reference visitor [claims](../access/write-content-conditions.md) inline, for [adaptive content](../access/adaptive-content-concepts.md) — not just variables.
