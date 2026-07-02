---
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
* Internal (same space): `[text](page.md)`, `[text](../folder/page.md)`
* Cross-space: use `https://app.gitbook.com/s/<spaceId>/<path>` — relative paths don't cross space boundaries. Use `XSPACE_<KEY>` sentinels during scaffolding; `configure-site` resolves them after creation.

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
* Use `https://app.gitbook.com/s/<spaceId>/<path>` instead.
* Use `XSPACE_<KEY>` sentinels when space IDs aren't known yet.

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

### Reference files

Load these on demand when the task requires deeper detail:

- `references/blocks.md` — full syntax and worked examples for every GitBook block type: tabs, steppers, hints, expandable, columns, updates, cards, embeds, files, buttons, icons, reusable content, and OpenAPI blocks. **Load when authoring non-trivial pages or when the quick-reference above isn't enough.**
- `references/frontmatter.md` — all frontmatter fields with descriptions, YAML quoting rules, cover images, adaptive content (`if:`), and the variables/expressions deep-dive. **Load when configuring page layout, covers, conditional visibility, or variables.**
- `references/markdown.md` — standard markdown, code blocks with titles, math/TeX, Mermaid diagram types and examples, and SVG handling quirks. **Load when working with diagrams, math, or SVG assets.**
- `references/configuration.md` — `.gitbook.yaml` options, the `.gitbook/` directory structure (assets, includes, vars, tags), and SUMMARY.md grammar rules in full. **Load when setting up a space, adding redirects, or authoring/editing SUMMARY.md.**
