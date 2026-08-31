---
hidden: true
name: write-docs
metadata:
  version: "1.0"
description: "Write, author, edit, and format GitBook documentation pages in Git-synced repos, IDEs, or any text editor. Use whenever a task involves creating or editing a GitBook markdown page, writing or updating a README.md or SUMMARY.md, inserting a hint, tab, stepper, card, or other GitBook block, configuring page frontmatter or layout options, setting up variables or expressions, or formatting content for GitBook outside the GitBook UI."
---

### When to Use This Skill

Use this skill when working with GitBook documentation through:

* Git-synced repositories (GitHub, GitLab)
* Local markdown editors
* IDE integrations
* Any environment where you're editing GitBook content as files rather than through the GitBook UI

### Quick Reference

#### GitBook Content Structure

GitBook organizes content through pages, spaces, and collections:

* **Pages** are individual markdown files that make up your documentation
* **Spaces** are collections of pages organized into a documentation site
* **Collections** are groups of spaces

**File structure:**

```
/
  .gitbook/
    assets/              # GitBook-managed images and files
    includes/            # Reusable content blocks
    vars.yaml            # Space-level variables
  .gitbook.yaml          # Configuration
  README.md              # Homepage
  SUMMARY.md             # Table of contents
  getting-started/
    installation.md
    quickstart.md
  api-reference/
    authentication.md
    endpoints.md
```

**Frontmatter fields (quick form):**

```markdown
---
description: "Page description for SEO"
icon: book-open
hidden: true
vars:
  page_variable: value
layout:
  width: default  # or 'wide'
  tableOfContents:
    visible: true
  pagination:
    visible: true
---
```

**Variables and expressions:**

* Space variables: `/.gitbook/vars.yaml`
* Page variables: Frontmatter `vars:`
* Expression syntax: `<code class="expression">space.vars.variableName</code>`

**Most common custom blocks:**

* `{% tabs %}...{% endtabs %}` — for alternatives
* `{% hint style="..." %}...{% endhint %}` — callouts (info/warning/danger/success)
* `{% stepper %}...{% endstepper %}` — sequential steps
* `<details>...<summary>...</details>` — expandable content

**Links:**

* External: `[text](https://example.com)`
* Relative (same space): `[text](page.md)`, `[text](../folder/page.md)`
* Cross-space (different space): `[text](https://app.gitbook.com/s/<spaceId>/<path>)` — relative paths never cross space boundaries, and this is the only correct URL form (not `/spaces/<id>/pages/<id>`). Get `<spaceId>` from `GET /orgs/{orgId}/spaces` and `<path>` from a page's `path` field in `GET /spaces/{spaceId}/content/pages`. Scaffolding a new site where the target space doesn't exist yet? Use `XSPACE_<KEY>` sentinels; `configure-site` resolves them after creation. Full examples: `references/markdown.md`.
* Moved/renamed pages keep working — GitBook auto-creates a redirect from the old path.

**Key reminders:**

* Read SUMMARY.md first when working with existing content
* Test in GitBook after editing locally
* Keep SUMMARY.md synchronized with your file structure
* OpenAPI specs must be uploaded via the UI, API, MCP, or CLI, not embedded in markdown

### When to Use Which Block

| Need | Use | Why |
|---|---|---|
| Sequential, ordered instructions | `{% stepper %}` | Clear step progression |
| Alternative options (languages, platforms) | `{% tabs %}` | User chooses without page clutter |
| Optional or detailed information | `<details>` | Keeps page scannable |
| Important warnings or tips | `{% hint %}` | Colored callout (info/warning/danger/success) |
| Side-by-side comparisons | `{% columns %}` | Parallel layout (max 2 columns) |
| Timeline or changelog | `{% updates %}` | Dated entries with tag filtering |
| Visual navigation cards | `<table data-view="cards">` | Clickable card grid |
| Downloadable files | `{% file %}` | File with caption |
| Call-to-action links | `<a class="button">` | Primary or secondary button |
| Reusable content across pages | `{% include %}` | Single source of truth |
| Dynamic content | `<code class="expression">` | Renders variable values |

**Variable scope:**

| If variable is... | Define in... | Access with... |
|---|---|---|
| Used across multiple pages | `/.gitbook/vars.yaml` | `space.vars.variableName` |
| Specific to one page | Frontmatter `vars:` | `page.vars.variableName` |

### Working with Existing Content

1. **Read SUMMARY.md first** — complete table of contents and file hierarchy
2. **If no SUMMARY.md** — browse the directory structure directly
3. **Check .gitbook.yaml** — root path, custom README/SUMMARY locations, redirects
4. **Check .gitbook/assets/** — uploaded images and files
5. **Check .gitbook/vars.yaml** — space-level variables

### Common Pitfalls

**Cross-space links:**

* Don't use relative paths to link to a page in a different space — they won't resolve.
* Don't use `/spaces/<spaceId>/pages/<pageId>` — that's not a valid GitBook link form.
* Use `https://app.gitbook.com/s/<spaceId>/<path>` instead, where `<path>` is the target page's `path` field (from `GET /spaces/{spaceId}/content/pages`), not its page ID.
* Use `XSPACE_<KEY>` sentinels when space IDs aren't known yet (new space, not yet created).

**File organization:**

* Don't reference the same markdown file twice in SUMMARY.md
* Keep file paths consistent between SUMMARY.md and actual file locations

**Configuration:**

* When using Git Sync, manage README.md only through your repository
* Test redirects after moving or renaming files

**Custom blocks:**

* Always close blocks properly (`{% endtab %}`, `{% endhint %}`, etc.)
* Match opening and closing tags exactly

**Frontmatter:**

* Always quote `description:` values containing `:`, `#`, or other YAML-significant characters — unquoted special characters cause silent Git Sync failures with no error message
* Frontmatter must be at the very top of the file

### Working with Git Sync

When GitBook is synced with Git, changes flow in both directions — Git changes update GitBook, and GitBook UI changes commit back to Git. Merge conflicts are resolved in Git.

**Best practices:** make structural changes via SUMMARY.md in Git; use branch-based workflows for significant updates; review auto-generated commits from GitBook.

#### Previewing a pushed branch

The two-link rule below covers content pushed through a change request. When you push
through **Git** instead, the equivalent is the commit status: opening a pull/merge request —
or pushing to a branch that already has one — makes GitBook import that branch and post a
status linking a preview of the rendered site. **Give the user that link whenever you push
docs changes, without being asked.** Read it off the commit status rather than building a
URL: the revision id is minted at import time and can't be derived from the branch or the PR,
and every push mints a new one, so an earlier link goes stale. See
`references/git-sync-previews.md` for the GitHub and GitLab commands and what to do while the
import is still running.

#### Choosing Git Sync vs. a change-request content push

When a space has Git Sync configured and you have (or can get) a local checkout of the synced repo, **prefer editing the files directly and committing/pushing** — Git Sync propagates the change to GitBook. This holds even in an MCP session where a change-request content-push tool (e.g. `updateChangeRequestContent`) is available and connected: the tool being one call away isn't a reason to bypass Git as the source of truth. An agent that discovers it *can* push straight into a CR should still check whether Git Sync is set up and reachable before doing so.

Reach for the change-request content-push path instead (MCP's `updateChangeRequestContent` or similar, or the REST `POST .../change-requests/<cr>/content` endpoint — see the `cr-create` skill) when:

- the space has no Git Sync configured yet (e.g. a brand-new space still mid-setup),
- there's no local Git checkout available in the current environment (no filesystem access to the synced repo), or
- the change is small and targeted (a typo, one paragraph, one field) — opening a CR is proportionate, and a full clone/commit/push cycle isn't worth it for that.

For anything larger — a new page tree, a multi-page rewrite, a migration — prefer Git Sync, even if that means pausing to confirm the repo is cloned locally first. Don't default to the change-request tool just because it's the first one that worked.

#### Two links are mandatory whenever a change request is involved

If any part of this edit went through a change request (`create_change_request` / `updateChangeRequestContent`, or the REST equivalents), **the edit is not done until both of the following have been reported back, every single time — this is a hard rule, not a reminder to skim past:**

1. **The CR diff/editor link** — `urls.app` on the change-request object, returned by `create_change_request`, `updateChangeRequestContent`, or `getChangeRequestById`.
2. **The site preview link** — the site URL from the **Site** object (`urls.published` when the site is public, else `urls.preview`) with **`/~/changes/<number>/` appended**. This is never part of the change-request response — it requires a separate lookup — which is exactly why it's the one that gets forgotten. Resolve it every time, not just when it comes to mind. **Without the `~/changes/` segment the link is not a preview of the change request** — it renders the site's current content, so it will look plausible and be wrong.

This applies no matter which skill pushed the content (this skill or `configure-site`) and no matter the transport (MCP or REST). See the `cr-create` skill's "Surfacing the preview link" for the full write-up and the REST resolution steps. **MCP equivalent** (GitBook MCP has no single ready-made "give me the preview link" call):

1. Resolve the space's organization — `invoke_operation("getSpaceById", {path:{spaceId}})` → `.organization` (skip if you already have the org ID).
2. Find which site the space belongs to — `list_sites` / `get_site_structure`, or check each site's site-spaces for a match on `.space.id`.
3. `invoke_operation("getSiteById", {path:{organizationId, siteId}})` → `.urls.published` (once the site is live), else `.urls.preview`. Append `/~/changes/<number>/`, stripping the trailing slash the API returns.

If the space isn't attached to any published site, say so plainly and give only the diff link — don't quietly drop the preview line without explanation.

This has already failed silently in practice: an edit was pushed and merged with only the diff link reported, and the preview link only surfaced when a person asked for it directly. Treat the two-link checklist above as literal.

### Reference files

Load these on demand when the task requires deeper detail:

- `references/blocks.md` — full syntax and worked examples for every GitBook block type: tabs, steppers, hints, expandable, columns, updates, cards, embeds, files, buttons, icons, reusable content, and OpenAPI blocks. **Load when authoring non-trivial pages or when the quick-reference above isn't enough.**
- `references/frontmatter.md` — all frontmatter fields with descriptions, YAML quoting rules, cover images, adaptive content (`if:`), and the variables/expressions deep-dive. **Load when configuring page layout, covers, conditional visibility, or variables.**
- `references/markdown.md` — standard markdown, code blocks with titles, math/TeX, Mermaid diagram types and examples, and SVG handling quirks. **Load when working with diagrams, math, or SVG assets.**
- `references/configuration.md` — `.gitbook.yaml` options, the `.gitbook/` directory structure (assets, includes, vars, tags), and SUMMARY.md grammar rules in full. **Load when setting up a space, adding redirects, or authoring/editing SUMMARY.md.**
- `references/git-sync-previews.md` — getting a preview link for a branch pushed through Git Sync: reading the GitBook commit status on GitHub and GitLab, telling the site preview from the editor diff, and handling an import that's still running. **Load whenever you push docs changes to a branch with a pull/merge request open.**
