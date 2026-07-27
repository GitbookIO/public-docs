---
description: Definitions of GitBook terms.
---

# Glossary

### A

**Actions menu** — the menu that opens when you click the three dots next to a page or item in the GitBook interface. Its options can vary depending on your current view mode.

**Add new** — the button/menu at the bottom of a section's table of contents for adding new content to your section. Also refers to the **+** button next to **Docs sites** in the sidebar, for creating a new site.

**Ask or search** — GitBook's search tool. Open it from the top of the sidebar, or press ⌘ + K. Type a keyword for a standard search, or ask a question to get a GitBook AI summary based on your content.

**audience settings** — the settings that decide who can access a published docs site. See [Publishing your site](../learn/publishing/README.md).

**Authenticated access** — publishing a site so visitors must authenticate through your identity provider before viewing it. Ideal for private content or an internal knowledge base. See [Authenticated access](../learn/access/authenticated-access/README.md).

### B

**block** — every piece of content on a page exists in a block: text, images, tables, code, API references, embeds, and more. Move a block by dragging it, change its settings, and in some cases change its type, from the block's Options menu.

### C

**change request** — similar to a pull request in GitHub. Change requests let you work on a branch of a section in parallel while keeping the original intact — edit, then submit for review. Changes don't appear in the primary section until someone merges the change request.

**context menu** — the menu that appears above highlighted text in the editor, for formatting (bold, italic, code) or adding links and annotations.

**Comments** — a side panel for commenting on any block on a page. Reply to create a discussion, tag people with `@`, react with emojis, resolve comments that are no longer relevant, and filter to just the comments you need.

**cover** — an image at the top of a page, spanning the full page width or just the content width as a hero image.

**custom domain** — a customized URL for a docs site (e.g. `docs.yourcompany.com`), configured from a site's **Settings** panel. See [Set a custom domain](../learn/publishing/custom-domain/README.md).

### D

**diff view** — a toggle highlighting which pages and blocks were added, edited, or deleted in a change request. Toggle it with **View changes** in the section header.

**discussions** — replying to a comment creates a discussion: a threaded conversation in the Comments side panel.

**docs site** — a published site containing content written in the GitBook editor, accessible to users without a GitBook account.

**domain** — the base of a docs site's URL, customizable from a site's **Domains** settings. Setting a [custom domain](#custom-domain) overrides this.

### E

**editor** — the GitBook UI you see when logged into the app: a block-based editor with Markdown support and WYSIWYG tools for adding and moving blocks.

### F

**files** — images, videos, and other items uploaded to a section, viewable and manageable in the **Library** tab beside **Pages**.

### G

**Git Sync** — synchronizes a GitHub or GitLab repository with GitBook, turning Markdown files into documentation. It's bi-directional — GitBook edits appear in your repo, and repo commits update GitBook. See [Git Sync](../learn/git-sync/README.md).

**GitBook AI** — an AI assistant trained on your knowledge base, answering questions from the **Ask or search** menu, and able to help [write or edit content](../learn/gitbook-ai/agent/write-and-edit.md) in the editor.

**group** — a set of related sections, like a folder. Groups also let you manage content-level permissions at scale.

### I

**inline palette** — type `/` in the middle of a block to open it, for quickly adding inline content like images, emojis, or Math & TeX.

**insert palette** — type `/` in an empty block to open it, showing every available block, including plugins and reusable content.

**insights** — GitBook's built-in analytics for docs sites: page views, feedback, and popular searches. See [Analytics](../learn/analytics/README.md).

**integrations** — connect GitBook content to third-party services and platforms, installed per section from the Integrations menu. See [Custom components](../learn/custom-components/README.md).

### L

**live edits** — making changes directly to a live version of a document, without a change request. The default for unpublished sections.

**llms.txt** — files GitBook automatically generates for every published site (`llms.txt` and `llms-full.txt`), formatted for AI/LLM ingestion. See [Make your docs agent-ready](../learn/gitbook-ai/readers-ai/make-your-docs-agent-ready.md).

**locked live edits** — requires a change request to make changes, helping avoid mistakes on important documents. Available for any section, and automatic for published sites.

### M

**MCP server** — a Model Context Protocol server GitBook automatically exposes for every published site, giving AI tools a structured way to discover and retrieve your docs. See [MCP server for published docs](../learn/gitbook-ai/readers-ai/mcp-server-for-published-docs.md).

**member management** — tools for viewing and editing your organization's members, including admin rights and content access.

### O

**Options menu** — opens when you click the six dots next to a block, for changing its appearance. Drag the six dots to move the block.

**Organization** — contains all the content and docs sites for a company. You can belong to one or many organizations, switching between them from the organization menu at the top of the sidebar.

### P

**page** — where you add or write content using blocks. Pages live inside a section, with an optional icon or emoji.

**page group** — a way to group pages together, with an optional name and icon.

**page options** — layout and display options for a page — hide the title, description, table of contents, or page outline — set from the **Page options** side panel.

**Permissions** — decide organization members' access level via assigned roles, which can be overridden at a content level for specific spaces or collections. See [Roles, permissions, and inheritance](../learn/collaboration/roles-permissions-inheritance.md).

### R

**reusable content** — content synced across multiple locations in a section — edit one instance, and every instance updates. Manage it from the **Library** tab beside **Pages**. See [Reusable content and variables](../learn/creating-content/reusable-content-and-variables.md).

### S

**section** — an area for organizing related content: a single page, or multiple pages, subpages, and page groups. Sections belong to a docs site and appear in a tab bar on your published docs.

**section header** — the menu bar below the section overview, with the section's title and icon, plus buttons for comments, broken links, change requests, and **Edit**.

**section overview** — the menu bar at the top of the app when viewing a section: breadcrumbs, the Git Sync button, the Share button, the Actions button, and collaborator avatars if others are working there too.

**Share links** — a private link that gives access to a space or site without inviting someone to your organization — anyone with the link can view it.

**sidebar** — the area on the far left of the GitBook window: **Ask or search**, your docs sites and content, notifications, integrations, and settings.

**slug** — the customizable final part of a URL, after the domain — inferred from a site's title by default, customizable from **Site settings** → **Domains**.

**subpage** — a page nested within another page, typically holding related content.

### T

**table of contents** — the list of pages, links, and page groups making up a section, on the left of the page next to the sidebar. Also gives access to a section's reusable content and files.

### V

**variant** — a different version of your documentation — a translation, or docs for a different product version. Readers switch between variants using a dropdown on the published site. See [Site sections and variants](../learn/publishing/site-sections-and-variants/README.md).

**version** — a saved snapshot of a section at a specific time, accessible from **Version history**.

**Version history** — a menu showing a section's major events — creation, merged change requests, rollbacks. Click any version to see the section as it was then, and roll back if needed.
