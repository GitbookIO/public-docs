---
name: gitbook
description: "Comprehensive skill for GitBook documentation work, combining two capabilities: (1) Site orchestration — design site structure, scaffold a Git monorepo, drive the GitBook REST API to create sites/sections/spaces, apply branded customization, and hand off Git Sync setup; and (2) Page authoring — write and edit GitBook content (markdown, frontmatter, custom blocks like tabs/hints/steppers/columns/updates/cards/openapi, variables, expressions, cross-space links) in Git-synced repos, IDEs, or any text editor. Use whenever the user wants to spin up, restructure, migrate, customize, or extend a GitBook docs site, link spaces to a Git repo for sync, change branding (logo/colors/fonts/header/footer), programmatically manage spaces/sections/site-spaces, or author/edit pages, README/SUMMARY files, reusable content blocks, or any GitBook-flavored markdown outside the GitBook UI."
---

# GitBook

A one-stop skill for teams working in GitBook. It covers two complementary jobs, with all the detail offloaded into topical reference files:

- **Site orchestration** — design structure, scaffold a Git monorepo, drive the GitBook REST API, apply branding, hand off Git Sync setup.
- **Page authoring** — write GitBook-flavored markdown: frontmatter, custom blocks, variables, expressions, OpenAPI, cross-space links.

Read this overview, then open the topical references below as the task requires. Each reference is one level deep from this file. The complete original SKILL.md files for both source skills are also preserved verbatim under `references/` as an integrity floor.

## When to use this skill

- Creating a new GitBook docs site end-to-end
- Restructuring or extending an existing site (add a space, regroup sections, change branding)
- Migrating to GitBook from another docs platform (Mintlify, Docusaurus, ReadTheDocs, GitBook v1)
- Authoring or editing GitBook content in Git-synced repos, IDEs, or any external text editor
- Working with GitBook-flavored markdown — frontmatter, custom blocks, variables, OpenAPI, cross-space links
- Managing spaces, sections, or site-spaces via the GitBook REST API
- Customizing branding (logo, colors, fonts, header/footer)

## Reference index

### Site orchestration

| Reference | When to read |
|---|---|
| `references/inputs-checklist.md` | Before starting any new build: PAT/auth, org, site plan, content seed, branding, structure, Git remote |
| `references/site-structure-design.md` | Designing the space/section/page tree for a non-trivial site |
| `references/repo-scaffolding.md` | Laying out the monorepo, generating SUMMARY.md, cross-space link sentinels, example-site index |
| `references/api-workflow.md` | The standard API call sequence; multi-language sites; section groups; updating existing sites; Imports vs Git Sync |
| `references/api-cheatsheet.md` | Exact request bodies and response shapes for every API call |
| `references/branding-schema.md` | The `SiteCustomizationSettings` field reference (theme, colors, fonts, header, footer, etc.) |
| `references/customization-recipes.md` | Worked branding payloads for common scenarios |
| `references/cross-space-links.md` | Sentinel-and-resolve workflow for `XSPACE_<KEY>` placeholders |
| `references/git-sync-handoff.md` | The user-facing instructions template for wiring up Git Sync in the UI |
| `references/migration-from-other-platforms.md` | Pre-flight, source-platform mappings, anchor-pages strategy, format-pass, link-sweep — read before any migration |

### Page authoring

| Reference | When to read |
|---|---|
| `references/page-frontmatter.md` | All frontmatter fields: `description`, `icon`, `hidden`, `vars`, `if`, `cover`, `coverY`, `layout` |
| `references/markdown-syntax.md` | Standard markdown, code blocks, links, math, Mermaid diagrams, SVG gotchas |
| `references/custom-blocks.md` | `{% tabs %}`, `{% hint %}`, `{% stepper %}`, `<details>`, `{% columns %}`, `{% updates %}`, cards, embeds, files, buttons, icons, includes, OpenAPI |
| `references/variables-and-expressions.md` | `space.vars` / `page.vars`, `<code class="expression">` |
| `references/summary-md-grammar.md` | SUMMARY.md format, indentation, special bullets (external, cross-space, `builtin:openapi`) |
| `references/configuration-files.md` | `.gitbook.yaml`, the `.gitbook/` directory, working with Git Sync |
| `references/block-ecosystem.md` | Decision guide: which block to reach for in which content situation |
| `references/example-page.md` | A complete worked example combining multiple blocks |

### Examples and originals

| Reference | What it is |
|---|---|
| `references/example-site/` | Pruned production-style GitBook site (~150 files). Read `PRUNE-NOTES.md` first |
| `references/example-site/customization.json` | Real-world branding payload export |
| `references/example-site/structure.json` | Real-world structure export (sections, section-groups, multi-language site-spaces) |
| `references/write-gitbook-syntax.md` | The original `write-gitbook` SKILL.md, verbatim — comprehensive authoring reference |
| `references/manage-gitbook-site-original.md` | The original `manage-gitbook-site` SKILL.md, verbatim — comprehensive orchestration reference |

## Critical concepts (must internalize before doing real work)

These five concepts shape everything else and are short enough to keep inline.

### 1. The Git Sync constraint

**GitBook's REST API can do almost everything except set up Git Sync.** Authorizing GitHub/GitLab, picking the repository, choosing the branch, setting the project directory for monorepos, and choosing the initial sync direction are all UI-only operations. The API only lets you *read* the resulting Git Sync state (`GET /v1/spaces/{spaceId}/git/info`).

That means the cleanest end-to-end flow is always:

1. Scaffold a Git repo locally (and, when `gh`/`glab` are available, the remote)
2. Create the site, sections, and any empty spaces via the API
3. **The user does a short, well-scripted UI step in GitBook to wire each space to its directory in the repo** — generate clean copy-paste instructions, see `references/git-sync-handoff.md`
4. Apply branding/customization via the API

If the user explicitly doesn't want Git Sync, fall back to the Imports API or template application (see `references/api-workflow.md`).

### 2. Confirmation gates for state-changing API calls

Site creation, space creation, adding sections, attaching site-spaces, customization PUTs, and any DELETE are **immediately visible to the whole org** and take real effort to clean up.

**The rule:** never call a state-changing endpoint without first showing the user a one-screen preview of exactly what's about to happen and getting an explicit "yes".

A good preview is short and concrete:

> About to run, in org **Acme Inc** (`org_abc123`):
>
> - Create site **"Acme Platform Docs"** (type: site, plan: ultimate, visibility: public)
> - Create 3 empty spaces: **Guides**, **API Reference**, **Changelog**
> - Add Guides as the default section; create sections for API Reference and Changelog
>
> Proceed? (yes/no)

Bad previews are vague ("I'll create the site now") or buried in a wall of explanation. For DELETEs, be even more explicit ("This will delete site X along with its 3 spaces. Spaces and sites are recoverable for 7 days, then permanent. Confirm?").

For read-only calls (GET endpoints), no confirmation is needed.

### 3. The auth pattern (never echo, never write the PAT)

The user keeps their GitBook PAT in 1Password. Fetch it via `op`:

```bash
export GITBOOK_TOKEN=$(op read "<secret-reference>")
```

The secret reference is remembered across sessions via Claude's memory feature. On first use, check memories first; only ask the user once if absent. Never write the token to a file, never echo it back in a response, never commit it. Full details in `references/inputs-checklist.md`.

### 4. Cross-space link sentinels (`XSPACE_<KEY>`)

Cross-space links need real space IDs, but IDs don't exist until the API has created the spaces. During scaffolding, write a sentinel:

```markdown
See the [Authentication concept page](https://app.gitbook.com/s/XSPACE_GUIDES/concepts/authentication).
```

After space creation, substitute every `XSPACE_<KEY>` for the real space ID using a sweep. Full pattern + substitution script: `references/cross-space-links.md`.

### 5. Actively reach for rich blocks — don't fall back to plain markdown

A common failure mode: generating docs that *work* but use plain markdown for everything, missing the rich blocks that make GitBook sites feel like a real product. Before writing any non-trivial page, walk the decision table in `references/block-ecosystem.md` and ask "is there a specialized block for this?" Concrete defaults:

- **Changelogs** → `{% updates %}` with `tags=""` + `.gitbook/tags.yaml` — not `## YYYY-MM-DD` headings
- **API endpoint references** → OpenAPI spec + `type: builtin:openapi` in SUMMARY.md — not hand-authored endpoint pages
- **State machines, flows, sequences** → ` ```mermaid ` fences — not ASCII art
- **"Choose your path" content** → card-tables (`<table data-view="cards">`)
- **Side-by-side intros** → `{% columns %}`
- **Repeated boilerplate (3+ places)** → `.gitbook/includes/<name>.md` + `{% include "..." %}`
- **Repeated literals** → `.gitbook/vars.yaml` + `<code class="expression">space.vars.<name></code>`
- **Multi-language code samples** → `{% tabs %}`
- **Walkthroughs of 3+ ordered steps** → `{% stepper %}`

## Quick-start workflows

### New site, end-to-end

1. Read `references/inputs-checklist.md` and gather all required inputs.
2. Design the structure with the user (see `references/site-structure-design.md`) and get explicit sign-off **before** scaffolding files.
3. Scaffold the repo as a monorepo (`references/repo-scaffolding.md`). Write cross-space link sentinels (`XSPACE_<KEY>`) wherever a link crosses a space boundary.
4. Author markdown content using the page-authoring references (`page-frontmatter.md`, `custom-blocks.md`, `block-ecosystem.md`, etc.). Look at `references/example-site/` for idiomatic patterns.
5. Commit and (if possible) push to a Git remote.
6. Run the API workflow (`references/api-workflow.md`) to create the site and sections. Apply customization (`references/branding-schema.md` + `references/customization-recipes.md`).
7. Resolve `XSPACE_<KEY>` sentinels with real space IDs (`references/cross-space-links.md`). Commit and push.
8. Generate per-space Git Sync handoff instructions (`references/git-sync-handoff.md`). Wait for user confirmation.
9. Verify with `GET .../structure` and `GET .../customization`.

### Editing existing content (Git-synced)

1. Read `SUMMARY.md` first to understand the navigation.
2. Check `.gitbook.yaml`, `.gitbook/vars.yaml`, `.gitbook/includes/` (see `references/configuration-files.md`).
3. Make changes using the page-authoring references. Test custom blocks in GitBook after editing locally.

### Migrating from another platform

Read `references/migration-from-other-platforms.md` **before** the build, not after. Headlines: mirror the source IA before reimagining it, treat bulk exports as incomplete, anchor 4–6 high-quality pages and bulk-convert the long tail, run a documented format-pass, don't auto-generate frontmatter you don't have, OpenAPI-first for API references, do internal-link conversion as one sweep.

### Branding-only changes on an existing site

1. `GET /v1/orgs/{orgId}/sites/{siteId}/customization` to fetch current settings.
2. Modify in memory using `references/branding-schema.md` as the field reference.
3. `PUT` the result back. Never paste a customization payload from memory — round-trip it.
4. Verify with another `GET`.

## Common mistakes to avoid

- **Don't put the PAT in any file Claude writes.** Always read it from the environment.
- **Don't try to set up Git Sync via the API.** It's UI-only; route through the handoff template.
- **Don't paste an entire customization payload from memory.** GET, modify, PUT.
- **Don't create a space for every section of content.** A space is a heavy unit (its own URL slug, sync, settings). Pages and folders within a space are the right tool for sub-grouping.
- **Don't skip the structure-plan-and-confirm step**, even when the user is in a hurry. Restructuring a published site is painful.
- **Don't auto-generate SUMMARY.md by walking folders.** Gather the desired nav from the user (see `references/repo-scaffolding.md` and `references/summary-md-grammar.md`).
- **Don't write real `app.gitbook.com/s/<id>/...` links during scaffolding.** IDs don't exist yet; use `XSPACE_<KEY>` sentinels.
- **Don't auto-generate frontmatter you don't have** during migrations (e.g. picking icons from URL slugs produces a sea of mismatched cog icons).
- **Don't default to plain markdown** when a specialized block fits the content shape (see `references/block-ecosystem.md`).
- **Don't over-format SUMMARY.md.** GitBook's parser is strict. See `references/summary-md-grammar.md`.

## Dynamic documentation lookup

If you need additional information that is not directly available in this skill or its references, you can query the GitBook documentation dynamically by asking a question:

```
GET https://gitbook.com/docs/skill.md?ask=<question>
```

The question should be specific, self-contained, and written in natural language. The response will contain a direct answer plus relevant excerpts and sources from the documentation. Use this for clarification or to retrieve related documentation sections beyond what this skill covers.
