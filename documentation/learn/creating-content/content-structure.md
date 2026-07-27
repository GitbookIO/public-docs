---
description: How pages, page groups, spaces, and collections organize your content.
---

# Content structure: pages, spaces, collections

Content in GitBook is organized around your docs sites. Your organization contains sites, and each site is made up of **sections** — the pages you write and edit live inside a section. Related sections can be organized into **groups** to shape your site's navigation. The structure you see while editing is the same structure your visitors see on your published site.

## Sections

A section is where you work on a set of related pages — write content, organize pages, add integrations, and more. Every section belongs to a site, and related sections can be organized into groups.

{% hint style="info" %}
The GitBook API represents sections as `space` objects. This doesn't affect API integrations or Git Sync.
{% endhint %}

**Create a section** — in your site, click **Add…**, then **New section**. Create it at the top level of your site or inside a group. New sections start as **drafts**: part of your site and editable by your team, but not visible to visitors until published. Rename a section by hovering over its name in the section header.

**Publish a draft section** — open the section's Actions menu and click **Publish** (or publish several drafts at once from the structure editor). Preview drafts by switching the site preview between **Live** and **Live + Drafts**.

**Duplicate a section** — open its Actions menu and click **Duplicate**, creating a copy in the same location.

{% hint style="warning" %}
Duplicating copies the section's content, but not its revisions or version history.
{% endhint %}

**Move or reorder a section** — the sidebar's content tree is read-only. Open the structure editor and drag the section to its new position — changes reflect in the sidebar and published site immediately.

**Delete a section** — open its Actions menu and click **Delete**.

{% hint style="warning" %}
Restore deleted sections from the Trash for up to 7 days — after that, GitBook deletes them permanently.
{% endhint %}

## Groups

Groups organize related sections within your site, making its structure easier for visitors to navigate.

**Create a group** — click **Add…** → **New group**, and choose a title and icon. New groups start as drafts, invisible on your published site until published.

**Add sections to a group** — open the structure editor and drag a section into or out of the group, or create a new section directly inside it.

**Publish a group** — open its Actions menu and click **Publish** (or publish several drafts at once from the structure editor).

**Rename a group** — open its Actions menu, click **Rename**, and change the title or icon.

**Delete a group** — open its Actions menu and click **Delete**.

## Pages

A page is where you add, edit, and embed content — always inside a section, letting you group related content by topic or area. When you publish your site, each section appears in navigation, with its pages underneath.

### Table of contents

Create as many pages as you need in a section — they all appear in the table of contents on the left, in the same place on your published site (unless you [hide it](#page-options)).

{% hint style="info" %}
**Section landing page.** The first page in your table of contents is always the section's landing page, even if it's hidden from the table of contents.
{% endhint %}

**Create a new page** — enter live edit mode or open a change request, then click **Add new...** at the bottom of the table of contents and click **Page**. Or hover between existing pages and click the **+** icon that appears.

{% hint style="warning" %}
**New page option missing?** If live edits are disabled, create or edit a change request instead — the **New page** button (for pages, page groups, and links) lives in the table of contents there. You might also lack permission to edit.
{% endhint %}

### Organizing your content

Three ways to organize content in the table of contents:

**Pages.** A page has a title, an optional description, and content. Nest a page by dragging it below another in the table of contents — this creates a **subpage**. Adding subpages to an empty parent page auto-generates a "contents" page linking to them in the published docs.

{% hint style="info" %}
There's no limit to page nesting, but avoid more than three levels to keep navigation simple.
{% endhint %}

Changing a page's title also changes its slug (the final part of its URL) unless you've set the slug manually. To change a page's title, link title, or slug: open its Actions menu and click **Edit title & slug**.

**Page link title.** Give a page a longer, SEO-friendly title while keeping a shorter one for navigation and links — open the page's Actions menu, click **Edit title & slug**, and enable/define a link title in the dialog. With Git Sync, set it directly in `SUMMARY.md`:

```markdown
# Table of contents

* [Page main title](page.md "Page link title")
```

Link titles appear in the table of contents, pagination buttons, and relative links to that page. They're optional — without one, the page uses its standard title.

**Page groups.** Bring related pages together within a section's table of contents.

{% hint style="info" %}
Page groups organize pages within a single section. To organize the sections of a site, use [groups](#groups) instead.
{% endhint %}

Create one via **Add new...** → **Group**. Page groups live only at the top level of the table of contents — you can't nest them inside each other. To rename one, open its Actions menu and click **Rename**.

**External links.** Add a link straight to external content via **Add new...** → **External link**.

### Page icons and emojis

Add an optional icon or emoji to a page so it's easier to spot when skimming the table of contents — it also appears next to the title at the top of the page. Click **Add icon** when hovering the page title, or the emoji button to its left.

### Page options

Customize a page's look and visibility from the **Page options** menu (hover the page title, or open its Actions menu).

**Layout.** Choose one of three layout presets, or build a custom layout, toggling: page title, page description, table of contents, page outline, next/previous links, page metadata, and tags. Tag a page from **Library → Tags**; toggle **Show tags on page** to display them in the header, and pick one as the page's primary tag to show in the table of contents. Set the page's width here too — **Wide** gives blocks like tables, cards, and code blocks more room, useful for landing pages.

**Visibility.** Choose which pages show in your published docs and whether each appears in site search and search engines. To hide a page: open its Actions menu and toggle **Hide page**. Hidden pages are only hidden from the published table of contents — they remain available through the site's MCP server and in `llms-full.txt`. With Git Sync, hidden pages carry `hidden: true` in their frontmatter.

{% hint style="warning" %}
Hiding **Page title** or **Page description** only hides the page header in published content — it doesn't remove headings inside the page body.
{% endhint %}

**Metadata (SEO).** Use **Page options → Metadata** to tell search engines how similar pages relate (e.g. documentation versions or variants):

* **Canonical URL** — the preferred, authoritative URL for this page, used when multiple URLs show the same content.
* **Alternate URLs** — other URLs for the same content in another variant (a different version or language), so search engines group them instead of treating them as duplicates.

Both fields accept another GitBook page (recommended) or an external URL. A common pattern for versioned docs: set older pages canonical to their latest equivalent, and list older versions as alternates on the latest page.

### Page covers

Click the **Page cover** option to add a default cover immediately, then:

* **Change the image** — hover the cover, click **Change cover**, and choose or upload an image (ideal size: 1990×480px).
* **Reposition it** — hover, open the Actions menu, click **Reposition**, drag into place, and **Save**.
* **Remove it** — hover, open the Actions menu, and click **Remove**.
* **Set full width or hero width** — hover, open the Actions menu, and choose your preferred style.
