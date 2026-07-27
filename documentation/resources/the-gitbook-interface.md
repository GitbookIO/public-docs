---
description: A tour of the GitBook app interface.
---

# The GitBook interface

GitBook is organized around your docs sites. You start at your organization **Home**, open a site to work on its content, and edit pages inside sections. This page walks through each part of the interface.

### Home

When you open GitBook, you land on your organization **Home**: every docs site in your organization, in one place. From here you can open a site, create a new one, or adjust organization-wide settings. Home contains:

* **Switcher** — get back to Home from anywhere using the switcher at the top of the sidebar. If you're part of multiple organizations, switch between them here, or create a new one.
* **Notifications** — when you're tagged in a comment or conversation, or there's important activity in a section you're working in, you get a [notification](../account-and-billing/personal-and-organization-settings.md#notifications) showing what's new.
* **Ask or search** — press ⌘+K (or Ctrl+K) to open it from anywhere. Ask a question in natural language, powered by [GitBook AI](../learn/gitbook-ai/ai-search.md), or search by keyword. Results from your current section appear first, followed by the rest of your organization — switch organizations first to search a different one. Search respects your team's permissions, so you'll only see content you have access to. Content is indexed by grouping it into sections denoted by H1, H2, or H3 headings, with each result showing the first few lines below the section header.
* **Sites list** — every docs site in your organization. Click one to open it.
* **All content** — if your organization has content that isn't part of any site, it appears here alongside your sites, in a tree view; if everything belongs to a site, this section doesn't appear. Click **Content** in the sidebar to open it. Each row shows the content's name and when it was last updated — click a row to open it, use the **All sites** filter to narrow by site, or **Search content** to find something by name. Click **Create content** to start something new here — though it's best practice to create content inside a site whenever you can, so structure, permissions, and publishing stay in one place.
* **Settings** — [organization and account settings](../account-and-billing/personal-and-organization-settings.md) share one dedicated screen, grouped into **Account** and **Organization**. Click **Back to app** to return to your work.
* **Styleguides** — view every [style guide](../learn/gitbook-ai/agent/style-guide.md) in your organization and the sites that use it.
* **Trash** — deleted sections appear here. Restore them for up to seven days — after that, they're permanently deleted.

### Site sidebar

Opening a site replaces the sidebar with that site's content and tools — the same structure visitors see on your published site:

* **Site header** — your site's name and publish status, plus **Preview** and **Publish** buttons.
* **General** — Overview, Change requests, Site structure, and Settings.
* **Tools** — Styleguide, Customize, Analyze, and Extend. Each opens in the main view.
* **Content** — your site's [sections](../learn/publishing/site-sections-and-variants/README.md) and groups, in published order. Click a section to edit it. The tree here is read-only — reorganize it in the structure editor. Use the search, edit, and **+** icons on the Content header to find, rename, and add sections.

### Table of contents

By default, the table of contents lists [pages, links, and page groups](../learn/creating-content/content-structure.md) in your selected section, to the right of the sidebar. It also gives access to [reusable content](../learn/creating-content/reusable-content-and-variables.md) and [files](../learn/creating-content/blocks/files.md) for the section.

From the **Pages** tab, you can:

* Create new pages and subpages.
* Create page groups.
* Add external links.
* Open a page's Actions menu.

From the **Library** tab, you can:

* View and search reusable content, variables, images, and files in the section.
* View and insert reusable content from other sections.
* Create or import new Library items.
* Drag and drop Library items onto the page.
* Double-click a Library item to rename it.
* Preview images.
* Manage and download images and files.

To focus on page content, hover next to the table of contents and click **Hide** — hover near the page edge and click **Show** to bring it back.

### Section header

The section header sits at the top of the editor and shows information about the section you're viewing — comments, history, [Git Sync](../learn/git-sync/README.md) configuration, and more.

{% hint style="info" %}
The section header adapts to your current section and mode. Editing a [change request](../learn/collaboration/change-requests/README.md) shows an overview of the change request, plus options to open the editor, view changes, and merge. Viewing a read-only section means you need to open a new change request to edit, since live edits are locked.
{% endhint %}

It includes:

* **The section emoji or icon** — identifies the section in the sidebar.
* **The section name** — appears in the sidebar and on your published site.
* **The section's breadcrumbs** — the site, and group if any, the section lives in.
* **Actions menu** — actions for your section; available options differ by editing mode.
* **Overview** — in a change request, view its title, description, participants, reviewers, changes, and comments.
* **Editor view** — edit content with GitBook's block-based editor.
* **Changes view** — [highlights changes](../learn/collaboration/change-requests/README.md#review-changes-in-diff-view) in a change request using diff view, for review before merging.
* **Preview** — preview content before merging a change request.
* **Collaborators** — avatars for people reading pages in the section; click one to open the page they're viewing.
* **Git Sync configuration** — configure [GitHub or GitLab Sync](../learn/git-sync/README.md) for the section.
* **The Share menu** — publish and share your section, or invite others to collaborate.
* **Variables** — create reusable [variables](../learn/creating-content/reusable-content-and-variables.md) for the section.
* **GitBook Agent** — collaborate on section changes with [GitBook Agent](../learn/gitbook-ai/agent/README.md).
* **Comments** — view [comments and discussions](../learn/collaboration/comments-and-live-editing.md) about section content.
* **Change requests** — create, update, and delete [change requests](../learn/collaboration/change-requests/README.md).
* **Section history** — view [version history](../learn/creating-content/version-history-and-page-tags.md) for the section or change request.
* **The Edit button** — if a section is published or [live edits](../learn/collaboration/comments-and-live-editing.md#live-editing) are locked, **Edit** creates a change request.

### Site tools

Site tools open from the site sidebar in the main view. The site header keeps **Preview** and **Publish**.

Under **General**:

* **Overview** — essential site information: URL, publish status, audience, content, and top-level insights. Once your site is live, this links to it.
* **Change requests** — change requests across your site's sections.
* **Site structure** — the structure editor, for adding, reordering, publishing, and removing sections and groups.
* **Settings** — [site settings](../learn/customization/site-settings-reference.md), including General, Members, Agents, Audience, Domain and URL, Redirects, and Plan.

Under **Tools**:

* **Styleguide** — your site's [style guide](../learn/gitbook-ai/agent/style-guide.md) defines writing rules and conventions that GitBook Agent follows.
* **Customize** — [customize your site](../learn/customization/README.md) with Theme, Layout, AI Assistant, and Configure options.
* **Analyze** — AI Insights and Analytics provide [detailed analytics](../learn/analytics/README.md) about your site's performance.
* **Extend** — Connections, Channels, Docs Embed, MCP access, and [Integrations](../learn/custom-components/install-and-manage.md).

### Content editor

The editor is the main part of your section — write and insert content, then collaborate with your team in real time.

Insert [content blocks](../learn/creating-content/blocks/README.md), write [Markdown](../learn/creating-content/markdown-reference.md), [embed content](../learn/creating-content/blocks/embed-a-url.md), and collaborate with [GitBook Agent](../learn/gitbook-ai/agent/README.md). You can also comment on blocks and tag teammates.

### Page title and description

At the top of each page, set a title, add an optional emoji, and write a description. The title appears in the table of contents and forms the published URL slug. Descriptions can be up to 200 characters, and appear as preview text in search engines.

{% hint style="info" %}
To change a page's URL slug, open its Actions menu and click **Edit title & slug**.
{% endhint %}

### Page actions menu

A page's Actions menu lets you duplicate, rename, or delete it. In the table of contents, hover over a page and click the icon — or click the icon next to the page title.

{% hint style="info" %}
Available actions depend on whether you're using [live editing](../learn/collaboration/comments-and-live-editing.md#live-editing) or a [change request](../learn/collaboration/change-requests/README.md).
{% endhint %}

### Page options

Use page options to customize documentation layout and navigation — available only while editing. Open **Page options** from a page's Actions menu, or hover over the page title and click **Page options**.

{% hint style="info" %}
Some changes, like disabling the table of contents, only appear on published documentation.
{% endhint %}

### Page outline

The page outline sits on the editor's right side, listing the H1 and H2 [headings](../learn/creating-content/blocks/heading.md) on the page so you can jump to a section quickly. It also appears on your published site — toggle it from Page options.

{% hint style="info" %}
If the right-hand column isn't visible, your browser window might be under 1430 pixels wide.
{% endhint %}

## Toolbar on published sites and site previews

When viewing your live docs site, a toolbar can appear at the bottom of the browser window, giving quick access to:

* Open the editor to view and edit your site's content
* Open your site's settings in GitBook
* Open your site's customization settings
* Open site analytics

{% hint style="warning" %}
The toolbar is only visible to logged-in members of your GitBook organization — other site visitors won't see it.
{% endhint %}

You'll see a slightly different version when you [open a preview URL](../learn/collaboration/change-requests/create.md#previewing-a-change-request) for your site from the GitBook app, letting you jump back into the app to add feedback or continue editing.

### When does the toolbar appear?

* Viewing your live site while logged into GitBook.
* Previewing earlier versions of your site through [version history](../learn/creating-content/version-history-and-page-tags.md).
* Previewing links for proposed changes — a [change request](../learn/collaboration/change-requests/README.md) created in GitBook, or a pull request created through [Git Sync](../learn/git-sync/preview-pull-requests.md).

### Why isn't the toolbar displayed?

If you're logged into GitBook and still don't see it, your browser may be blocking third-party cookies — the toolbar uses them to recognize your GitBook session on your published docs site or preview URL. Enable third-party cookies for your docs domain in your browser settings, then reload. This is more common in browsers or extensions with stricter privacy settings.

### Can I hide the toolbar?

Yes — click the last button on the toolbar to choose:

1. **Minimize** — reduces it to a small orb; click to expand again.
2. **Close for one session** — removes it in the current tab until you close it.
3. **Don't show again** — hides it and remembers your choice. Restore it by clearing your browser's local storage.
