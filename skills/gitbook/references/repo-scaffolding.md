# Repo scaffolding

How to lay out a GitBook docs repo as a monorepo, including the per-space directory shape, the optional `.gitbook.yaml`, repo-level `README.md` and `.gitignore`, and the rules for generating `SUMMARY.md` files.

## Contents

- Monorepo layout
- Optional vs required configuration
- Repo-level README and .gitignore
- Generating SUMMARY.md — gather the nav, don't infer it from folders
- Per-page markdown — defer to authoring references
- Cross-space links (sentinel-and-resolve)
- Example content (where to look)
- Committing and remote setup

## Monorepo layout

Lay out the repo as a monorepo — even for single-space sites, this is consistent and future-proof. Each space is a directory containing its own `README.md` (homepage) and `SUMMARY.md` (table of contents). Optionally a `.gitbook/` folder for per-space variables and reusable content blocks, and optionally a `.gitbook.yaml` for advanced sync configuration.

Example layout for a three-space site:

```
my-docs/
├── .gitignore
├── README.md                    # repo-level readme (not a space homepage)
├── guides/                      # space 1
│   ├── README.md                # space homepage
│   ├── SUMMARY.md
│   ├── .gitbook/
│   │   └── vars.yaml            # optional: space-level variables
│   ├── getting-started/
│   │   ├── installation.md
│   │   └── quickstart.md
│   └── concepts/
│       └── ...
├── api-reference/               # space 2
│   ├── README.md
│   ├── SUMMARY.md
│   └── endpoints/
│       └── ...
└── changelog/                   # space 3
    ├── README.md
    └── SUMMARY.md
```

## Optional vs required configuration

- **`.gitbook.yaml` is optional.** GitBook works fine on the default convention of `README.md` + `SUMMARY.md` per space. Only add a `.gitbook.yaml` when you need to override the root, define redirects, or do something else non-default. The bundled `example-site/` has zero `.gitbook.yaml` files and works perfectly.
- **`.gitbook/vars.yaml`** holds space-scoped variables that pages can reference inline (e.g. `support_email: support@evolve.com`). Useful for any value that appears on many pages. See `variables-and-expressions.md`.
- **`.gitbook/includes/<name>.md`** holds reusable content blocks — a snippet you embed in many pages with `{% include "..." %}`. Use these instead of copy-pasting boilerplate.
- The space directory name (e.g. `guides/`) is what the user enters into the "Project directory" field when wiring up Git Sync.

A minimal `.gitbook.yaml`, when you do need one, looks like:

```yaml
root: ./
structure:
  readme: README.md
  summary: SUMMARY.md
```

For the full `.gitbook.yaml` and `.gitbook/` directory reference, see `configuration-files.md`.

## Repo-level README and .gitignore

The repo-level `README.md` (top of the repo, not inside a space) should explain what the folder is and how it relates to the published site — not duplicate the docs themselves. A short paragraph is enough:

```markdown
# my-docs

Source for the [My Product docs site](https://docs.example.com). Each top-level folder
is a separate GitBook space; edits flow in both directions via Git Sync once configured.
```

A `.gitignore` should keep OS junk and editor settings out of the repo. Reasonable default:

```
.DS_Store
Thumbs.db
*.swp
*.swo
.idea/
.vscode/
```

If the team has additional generated artifacts (e.g. an OpenAPI spec built from source elsewhere), add those.

## Generating SUMMARY.md — gather the nav, don't infer it from folders

The most common scaffolding mistake is to walk the file tree and emit a SUMMARY.md from it: README at the top, every other file as a child indented under the README. This produces dispiriting nav — every page is a "child of the homepage", folder names become group titles whether or not they're meaningful to a reader, and the IA mirrors the file system instead of the user's mental model.

**The right pattern, in order:**

1. **Gather the desired navigation from the user during structure design.** Ask them — explicitly — to enumerate the top-level pages and the named groups for each space. This is the place where you make folder names match nav reality, and where the user can tell you "actually I want Authentication as a top-level page, not under Concepts."

2. **Lay out folders to match the agreed nav, not the other way around.** If the user wants three groups in a space — "Getting started", "Concepts", "Tutorials" — the space directory has three subfolders by those names (slugified), each with its own pages. Don't auto-extract a fourth group from a stray subfolder.

3. **Write SUMMARY.md to the explicit shape the user agreed.** The grammar that GitBook honors:

   ```markdown
   # Table of contents

   * [Space homepage](README.md)
   * [Top-level page A](top-level-a.md)
   * [Top-level page B](top-level-b.md)

   ## First group

   * [Page in group](first-group/page.md)
   * [Another page](first-group/another.md)

   ## Second group

   * [Page](second-group/page.md)
   ```

   Key shape rules:
   - **README.md is on its own line at the very top, as a sibling**, not a parent. Other top-level pages follow as siblings.
   - **`## Group name` headings introduce groups.** Pages in a group are flat bullets directly under the heading — *not* indented under the README.
   - **Avoid mechanical "* README.md" + nested-everything-under-it.** That collapses the entire nav into one tree under the homepage and makes every page look like a sub-page of the homepage in the sidebar.
   - **Group names come from the user, not the folder names.** "concepts/" can be the folder slug, but the group heading might be "How it works" if that's clearer.
   - **One bullet per page, no extra formatting.** No bold, no descriptions in the SUMMARY — those live in the page frontmatter.

4. **Special-case patterns** that aren't plain bullets:
   - **OpenAPI auto-generated endpoint pages** use a fenced YAML block as the bullet content (`type: builtin:openapi` — see `api-cheatsheet.md` and `custom-blocks.md`).
   - **External links** are `* [Title](https://...)` and render as outbound links in the nav.
   - **Cross-space links** in SUMMARY.md use the same `https://app.gitbook.com/s/<spaceId>/<path>` form as in body content. Path has no `.md` suffix. During scaffolding write the sentinel form (`XSPACE_<KEY>`); resolve after space creation.

If your scaffolding helper auto-generates a SUMMARY.md by walking folders, **make it idempotent and skip files that already exist**. A user-edited SUMMARY.md should never be silently clobbered — that's how hand-tuned navigation gets lost.

For the full SUMMARY.md grammar and pitfalls, see `summary-md-grammar.md`.

## Per-page markdown — defer to authoring references

**For all markdown files** — `README.md`, `SUMMARY.md`, every page — follow the page-authoring rules. See:

- `page-frontmatter.md` for frontmatter fields (`icon:`, `layout:`, `cover:`, etc.)
- `markdown-syntax.md` for markdown extensions, Mermaid, SVG handling
- `custom-blocks.md` for tabs, hints, steppers, columns, cards, updates, OpenAPI, etc.
- `variables-and-expressions.md` for `space.vars` / `page.vars`
- `block-ecosystem.md` for the decision table — which block to reach for in which situation
- `write-gitbook-syntax.md` for the complete original authoring reference, preserved verbatim

**Don't reinvent any of that here.** The bundled `references/example-site/` is the best practical reference for what idiomatic content looks like.

## Cross-space links (sentinel-and-resolve)

Multi-space sites *want* cross-space links — they're how a site feels like one connected product, not a bunch of separate manuals. **Don't duplicate content to avoid them, and don't drop them.** They're a first-class GitBook feature; the only twist is that they need real space IDs to render correctly, and IDs only exist after the site is created via the API.

**The flow during scaffolding:**

1. **Write cross-space links using a sentinel space-ID prefixed with `XSPACE_`**, one per planned space. Use the space slug from your structure plan as the suffix:

   ```markdown
   See the [Authentication concept page](https://app.gitbook.com/s/XSPACE_GUIDES/concepts/authentication).
   For the full reference, see the [API Reference](https://app.gitbook.com/s/XSPACE_API/).
   ```

   These are valid markdown links to non-existent GitBook spaces — they don't break the parser, they're easy to grep for, and they round-trip cleanly through Git.

2. **After space creation**, walk every markdown file and substitute `XSPACE_<KEY>` with the real space ID.

3. **Commit and push** the resolution. GitBook will pick it up via Git Sync.

Full script and gotchas: `cross-space-links.md`.

## Example content (where to look)

`references/example-site/` is a pruned snapshot of a production-style GitBook site (~150 files). **Read `references/example-site/PRUNE-NOTES.md` first** — it explains what's kept, what's dropped, and lists high-signal files for specific patterns.

Notable files to study, organized by pattern:

| Pattern | File to read |
|---|---|
| Updates block + tags | `changelog/README.md` + `changelog/.gitbook/tags.yaml` |
| `builtin:openapi` SUMMARY pattern | `developers/v2/SUMMARY.md` (look at the fenced YAML bullets) |
| Mermaid diagrams (flowchart, sequence) | `products/payments/concepts/payment-lifecycle.md`, `developers/v2/identity-api/README.md` |
| Layout `width: wide` + cover image | `home/README.md`, `developers/v2/README.md` |
| Card-tables for navigation | `home/README.md`, `partners/README.md` |
| Conditional content via `{% if visitor.claims... %}` | `products/payments/accept-payments/take-a-payment.md` |
| Tabs and steppers used together | `developers/v2/getting-started/quickstart.md`, `developers/v2/getting-started/authentication.md` |
| Webhook docs with code samples | `developers/v2/webhooks/verifying-signatures.md` |
| Reusable content includes | `home/.gitbook/includes/persona-switcher.md` |
| `.gitbook/vars.yaml` variables | Any space's `.gitbook/vars.yaml` |
| Grouped SUMMARY.md (sections via `## Heading`) | Any of the per-space `SUMMARY.md` files |

`customization.json` and `structure.json` at the example-site root are the complete API exports — the authoritative source for shape when you need a pattern not represented in the pruned snapshot.

## Committing and remote setup

After scaffolding:

```bash
cd my-docs
git init
git add .
git commit -m "Initial scaffold"
```

If the user wants a remote and `gh`/`glab` is available:

```bash
# GitHub
gh repo create <name> --private --source=. --push

# GitLab
glab repo create <name> --private && git push -u origin main
```

If neither tool is available, **say so explicitly** before scaffolding finishes. Two valid paths:

- **Local-only repo + manual remote step in handoff.** Commit locally, leave the user a "Step 0" in their handoff that says: *"On your machine, create a private GitHub or GitLab repo named `<name>`, then `git remote add origin <url> && git push -u origin main` from this directory."* Put this above the GitBook UI steps — they need the repo pushed before Git Sync can connect to it.
- **Ask the user to install `gh` or `glab`.** If they're going to be doing more sites, the tool is worth having.

Don't quietly default to local-only — a repo with no remote and no instructions about how to add one is a footgun the user will discover when they try to wire up Git Sync.
