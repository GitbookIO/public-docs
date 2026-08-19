---
hidden: true
name: gitbook
description: >-
  Work with GitBook end-to-end: author and format GitBook-flavored Markdown pages and blocks (hints,
  tabs, steppers); design, scaffold, and configure documentation sites via the GitBook REST API and
  Git Sync; generate and troubleshoot OpenAPI/Swagger API reference docs; create, push content to, and
  manage change requests and reviews over the REST API; and build GitBook integrations (custom blocks,
  ContentKit UI, events, OAuth). Use whenever a task involves GitBook: writing or editing docs,
  SUMMARY.md/.gitbook.yaml, site structure, OpenAPI references, change-request review flows, or
  building a GitBook app/integration.
---

{% hint style="info" %}
This page is generated automatically from [GitbookIO/gitbook-skills](https://github.com/GitbookIO/gitbook-skills). Don't edit it directly — edit the source skills there instead.
{% endhint %}

# GitBook

GitBook's skill for AI coding agents, covering six areas of GitBook work. Each section below is one of the six skills in [gitbook-skills](https://github.com/GitbookIO/gitbook-skills) — read its description to see if it matches your task, then fetch its linked page for full instructions before acting. Each skill's instructions link out to further reference material (full block syntax, API payloads, troubleshooting) in [gitbook-skills](https://github.com/GitbookIO/gitbook-skills) under `skills/<name>/references/` when you need more depth than the top-level instructions.

### Write & Edit Docs

Write, author, edit, and format GitBook documentation pages in Git-synced repos, IDEs, or any text editor. Use whenever a task involves creating or editing a GitBook markdown page, writing or updating a README.md or SUMMARY.md, inserting a hint, tab, stepper, card, or other GitBook block, configuring page frontmatter or layout options, setting up variables or expressions, or formatting content for GitBook outside the GitBook UI.

Full instructions: [https://gitbook.com/docs/skill/write-docs.md](https://gitbook.com/docs/skill/write-docs.md)

### Configure a Site

Create and maintain entire GitBook documentation sites end-to-end — design the site structure from source content, scaffold a Git repository in monorepo layout, set up the GitHub/GitLab remote, drive the GitBook API (via its REST API or MCP server) to create the site/sections/spaces, apply branded customization, and hand the user clean instructions for the one UI step (Git Sync wiring) that GitBook does not expose programmatically. Trigger this skill whenever the user wants to spin up a new GitBook docs site, restructure or extend an existing one, link spaces to a Git repo for sync, change a site's branding (logo, colors, fonts, header/footer), or programmatically manage spaces, sections, or site-spaces. This skill is the orchestration layer; for authoring the markdown content of any individual page it defers to the companion `write-docs` skill.

Full instructions: [https://gitbook.com/docs/skill/configure-site.md](https://gitbook.com/docs/skill/configure-site.md)

### Write OpenAPI Reference Docs

Author, configure, structure, and troubleshoot OpenAPI/Swagger API reference documentation in GitBook. Use this whenever a task involves a GitBook OpenAPI block or `{% openapi %}` block, adding or updating an OpenAPI/Swagger spec in GitBook (by file or URL, via the API, MCP, CLI, or app UI), generating API reference pages from a spec, configuring the interactive "Test it" runner (auth, servers, CORS, proxy), customizing pages with GitBook `x-*` extensions (icons, titles, navigation hierarchy, code samples, enum descriptions), marking operations experimental/deprecated/hidden, or automating spec updates in CI/CD. Trigger even when the user only mentions GitBook plus OpenAPI, puts an `x-` extension on a spec destined for GitBook, or asks "why isn't my spec loading" or "why doesn't Test it work", without naming this skill.

Full instructions: [https://gitbook.com/docs/skill/write-openapi.md](https://gitbook.com/docs/skill/write-openapi.md)

### Create & Manage Change Requests

Drive an end-to-end GitBook docs review flow from Claude Code by calling the GitBook REST API directly with curl (no CLI) — create a change request, push content (update an existing page AND create a new page), request reviewers, notify Slack, then pull review comments back in, fix them, re-push, and resolve. This is the authoring-side companion to cr-review (the reviewer side over the same API). Use this whenever someone wants to run a "docs review in GitBook" loop from the terminal/agent against the raw API (curl/HTTP), mentions creating a change request via the API, pushing content into a CR, "pull in the latest comments and fix them," requesting review on docs, or showing engineers how to collaborate on GitBook docs from Claude + Slack without a CLI.

Full instructions: [https://gitbook.com/docs/skill/cr-create.md](https://gitbook.com/docs/skill/cr-create.md)

### Review Change Requests

Review GitBook change requests from Claude Code by calling the GitBook REST API directly with curl (no CLI) — the reviewer-side companion to cr-create (the authoring side over the same API). Discover the change requests that need review (filter by who opened them, by space, or across a whole org), get the GitBook app link to review the diff, summarize what actually changed in a CR, then leave comments and optionally submit a review verdict (approve / request changes). Use this whenever someone wants to review docs change requests over the raw API (curl/HTTP), asks "what CRs are open / waiting on me / opened by <person>", "show me the change requests in <space>/<org>", "summarize what changed in this CR", "review this change request", "leave a comment on a CR", or "approve / request changes on a CR". For the authoring side (create a CR, push content, request reviewers, fix comments) over the API, use cr-create instead.

Full instructions: [https://gitbook.com/docs/skill/cr-review.md](https://gitbook.com/docs/skill/cr-review.md)

### Build an Integration

Build, develop, and publish GitBook integrations — apps that run inside GitBook to add custom blocks, react to events, connect external services via OAuth, and extend the editor. Use this skill whenever a task involves the GitBook integrations platform: scaffolding an integration with the GitBook CLI (`gitbook new`), writing or editing an integration's code (`createIntegration`, `createComponent`, ContentKit TSX), configuring `gitbook-manifest.yaml` (scopes, blocks, configurations, secrets), building custom editor blocks or link unfurlers, handling GitBook events like `space_content_updated`, setting up an integration's OAuth flow, running `gitbook dev`, or publishing an integration (private/unlisted/public, marketplace submission). Trigger this even if the user just says they want to 'build an app for GitBook', 'add a custom block', or 'connect <some tool> to GitBook' without saying the word 'integration'.

Full instructions: [https://gitbook.com/docs/skill/build-integration.md](https://gitbook.com/docs/skill/build-integration.md)
