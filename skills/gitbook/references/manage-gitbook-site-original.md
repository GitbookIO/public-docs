---
name: manage-gitbook-site
description: "Create and maintain entire GitBook documentation sites end-to-end — design the site structure from source content, scaffold a Git repository in monorepo layout, set up the GitHub/GitLab remote, drive the GitBook REST API to create the site/sections/spaces, apply branded customization, and hand the user clean instructions for the one UI step (Git Sync wiring) that GitBook does not expose via API. Trigger this skill whenever the user wants to spin up a new GitBook docs site, restructure or extend an existing one, link spaces to a Git repo for sync, change a site's branding (logo, colors, fonts, header/footer), or programmatically manage spaces, sections, or site-spaces. This skill is the orchestration layer; for authoring the markdown content of any individual page it defers to the companion `write-gitbook` skill."
---

# Manage GitBook Site

A skill for creating and maintaining entire GitBook documentation sites. Where `write-gitbook` covers what goes inside a single page, this skill covers everything around the pages: structure design, repo scaffolding, the GitBook REST API, and branding. Use the two skills together — this one calls into `write-gitbook` whenever it needs to generate or edit page content.

## The fundamental constraint

The most important thing to internalize before doing anything: **GitBook's REST API can do almost everything except set up Git Sync**. Authorizing GitHub/GitLab, picking the repository, choosing the branch, setting the project directory for monorepo layouts, and choosing the initial sync direction are all UI-only operations. The API only lets you *read* the resulting Git Sync state (`GET /v1/spaces/{spaceId}/git/info`).

That means the cleanest end-to-end flow is always:

1. Claude scaffolds a Git repo locally (and, when tooling permits, the remote)
2. Claude creates the site, sections, and any empty spaces it can via the API
3. **The user does a short, well-scripted UI step in GitBook to wire each space to its directory in the repo**
4. Claude applies branding/customization via the API

The user's role in step 3 is unavoidable but should never be a surprise — generate clear, copy-paste-ready instructions for them. Reference: `references/git-sync-handoff.md`.

If the user explicitly does not want Git Sync, fall back to the API content path (the Imports API and template application) — covered briefly below and in `references/api-cheatsheet.md`.

## Inputs you should gather up front

Don't start scaffolding until these are known. If something is missing, ask once with a focused question rather than guessing.

- **GitBook PAT** — required for all API calls. The user keeps this in 1Password and we fetch it at the start of each session via the `op` CLI:

  ```bash
  export GITBOOK_TOKEN=$(op read "<secret-reference>")
  ```

  The skill remembers the user's secret reference across sessions via Claude's memory feature. On first use:

  1. Check user memories for a line like `User's GitBook PAT 1Password reference: op://...`. If present, use that reference directly.
  2. If absent, ask the user once for their `op` secret reference (they can find it via "Copy Secret Reference" in the 1Password UI, or by running `op item get <item-name> --format=json`). After they share it, save it via `memory_user_edits add` so future sessions don't have to ask again.
  3. If `op read` fails (not signed in, wrong reference, item moved), surface the exact error and stop. Don't fall back to asking the user to paste the token directly into the conversation — keeping it in `op` is the whole point.

  Never write the token to a file, never echo it back in a response, never commit it.

- **Organization** — list the user's orgs with `GET /v1/orgs` and **show the list to the user, then ask them to confirm which one is the target by name**. Do this even if they have only one org — confirming once up front is cheap insurance against creating sites in the wrong place. Save the chosen `organizationId` for the rest of the session and refer to the org by its title (not its UUID) when narrating subsequent steps.
- **Site plan and visibility** — **default to `type: site` on the Ultimate plan**, public visibility, unless the user explicitly says otherwise. Most real customers want the Ultimate feature set (custom domain, AI Assistant, advanced customization, hidden GitBook trademark, custom fonts, custom logos). The free tier (`type: basic`) is appropriate only for clearly low-stakes use cases like solo open-source side projects. If you're unsure, ask: *"I'll set this up on the Ultimate plan unless you'd prefer the free tier — should I downgrade?"* — Ultimate features that are silently absent on `basic` (no AI assistant, no custom fonts, no custom domain) are a much bigger user surprise than briefly confirming the plan.
- **The content seed** — what's the site being built from? Common shapes:
  - A folder of existing markdown — the cleanest starting point
  - A handful of notes plus a competitor's site as a reference
  - Just a description of what they want to document
  - An existing site they want to restructure (in which case fetch `GET /v1/orgs/{orgId}/sites/{siteId}/structure` first)
  - **A migration** from another docs platform (Mintlify, Docusaurus, ReadTheDocs, GitBook v1) — see `references/migration-from-other-platforms.md` for the workflow. Migration is its own discipline; don't treat it as a glorified file copy.
- **OpenAPI spec for the API reference** — if the site has any API reference content, **ask up front whether they have an OpenAPI spec** (or whether one can be generated from their codebase). If yes, the API reference space is one `builtin:openapi` SUMMARY entry plus a one-paragraph overview README per resource — dramatically less work than hand-authored endpoint pages, and never drifts. See `references/block-ecosystem.md` and `references/api-cheatsheet.md` for the workflow. **Don't default to hand-authored endpoint pages** — they're almost always the wrong call.
- **Branding** — at minimum, primary color (hex). Optionally: logo URLs (light + dark), favicon, font choice (or one of GitBook's defaults), header links, footer text/links, theme preset (`clean`, `muted`, `bold`, `gradient`). For Ultimate sites, also consider AI-assistant starter prompts (3-5 short questions visitors are likely to ask).
- **Site structure** — sections, not site-spaces. If the site has more than one space, plan the **section list** with the user explicitly: each section has a title, a Font Awesome icon name, and a description. Section icons and descriptions are first-class navigation furniture — visitors see them — and gathering them up front saves a PATCH-per-section later. Example: `[{title: "Guides", icon: "book-open", description: "Concepts and tutorials"}, {title: "API Reference", icon: "code", description: "REST API and SDKs"}, {title: "Changelog", icon: "clock-rotate-left", description: "Updates and release notes"}]`.
- **Git remote preference** — GitHub, GitLab, or local-only. Check whether `gh` or `glab` are installed *before* asking. If neither tool is available, **say so explicitly** and offer two paths: (1) commit locally and put the "create the remote and push" step at the top of the user's handoff, or (2) ask the user to install the tool. Don't quietly default to local-only without telling them — they'll have a repo with no remote and no instructions.
- **Site shape** — single space or multi-space. Multi-space sites use **sections** to group spaces in the navigation; this is the right choice when content has clearly distinct audiences (e.g. user docs + API reference + changelog). Use site-spaces directly only for translation variants — see `references/api-cheatsheet.md`.

## Confirmation gates for state-changing API calls

Site creation, space creation, adding sections, attaching site-spaces, and customization PUTs all create or modify objects that are **immediately visible to everyone in the org** and that take real effort to clean up. Treat them as heavy operations.

The rule: **never call a state-changing endpoint without first showing the user a one-screen preview of exactly what's about to happen and getting an explicit "yes".**

A good preview is short and concrete:

> About to run, in org **Acme Inc** (`org_abc123`):
> - Create site **"Acme Platform Docs"** (type: site, plan: ultimate, visibility: public)
> - Create 3 empty spaces: **Guides**, **API Reference**, **Changelog**
> - Add Guides as the default section; create sections for API Reference and Changelog
>
> Proceed? (yes/no)

Bad previews are vague ("I'll create the site now") or buried in a wall of explanation. Keep it scannable.

The same rule applies to destructive calls — DELETE on a site, space, section, or customization override — only with even less ambiguity ("This will delete site **Acme Platform Docs** along with its 3 spaces. Spaces and sites are recoverable for 7 days, then permanent. Confirm?").

When the user has already confirmed a multi-step plan in the structure-design step, you don't need to ask again for each individual API call inside that plan — but if anything in the plan changes (an extra space, a different visibility), re-confirm.

For read-only calls (GET endpoints), no confirmation is needed.

## Designing the site structure

Before writing any files or making any API calls, decide on the structure and run it past the user. A weak structure is the single biggest reason docs sites fail to land.

The output of this step is a small plan, ideally three pieces:

1. **The space list** — one space per coherent body of content. Keep it small (1–4 spaces is typical). A space is a unit of navigation and Git Sync, so don't split a single audience's content across spaces.
2. **The section grouping** (if multi-space) — sections are top-level partitions in the site nav, e.g. "Product" / "Developers" / "Resources". A section can hold one or more spaces.
3. **The page tree per space** — folders and pages, with one or two sentence summaries of each page. The depth should match the content; shallow trees (1–2 levels) are usually best.

The full set of heuristics for going from raw inputs to a structure plan is in `references/site-structure-design.md` — read it the first time you do this for a non-trivial site. **Always show the plan to the user and get explicit sign-off before scaffolding files.** Restructuring later is cheap inside Git but expensive once a site is published and indexed.

A note on confirmation when the user gives one collapsed instruction: prompts like *"plan the structure and then scaffold it"* tempt you to skip the gate. Don't. Present the plan as a clear, scannable block, then either wait for a "yes" or — if you've already started scaffolding because the prompt was that explicit — surface what you decided in the plan and offer one easy chance to redirect ("if any of this is off, tell me and I'll redo before going further"). The point is that the user sees the plan **before** they're staring at twenty generated files, while a redo is still cheap.

## Scaffolding the repository

Once the structure is agreed, lay out the repo as a monorepo — even for single-space sites, this is consistent and future-proof. Each space is a directory containing its own `README.md` (homepage) and `SUMMARY.md` (table of contents). Optionally a `.gitbook/` folder for per-space variables and reusable content blocks, and optionally a `.gitbook.yaml` for advanced sync configuration.

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

A few notes about this layout that often trip people up:

- **`.gitbook.yaml` is optional.** GitBook works fine on the default convention of `README.md` + `SUMMARY.md` per space. Only add a `.gitbook.yaml` when you need to override the root, define redirects, or do something else non-default. The bundled example site (`references/example-site/`) has zero `.gitbook.yaml` files and works perfectly.
- **`.gitbook/vars.yaml`** holds space-scoped variables that pages can reference inline (e.g. `support_email: support@evolve.com` referenced as `{% vars.support_email %}`). Useful for any value that appears on many pages.
- **`.gitbook/includes/<name>.md`** holds reusable content blocks — a snippet you embed in many pages with `{% include "...persona-switcher" %}`. Use these instead of copy-pasting boilerplate.
- The space directory name (e.g. `guides/`) is what the user enters into the "Project directory" field when wiring up Git Sync.

A minimal `.gitbook.yaml`, when you do need one, looks like:

```yaml
root: ./
structure:
  readme: README.md
  summary: SUMMARY.md
```

### The repo-level README and .gitignore

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

### Generating SUMMARY.md — gather the nav, don't infer it from folders

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
   - **OpenAPI auto-generated endpoint pages** use a fenced YAML block as the bullet content (`type: builtin:openapi` — see `references/api-cheatsheet.md`).
   - **External links** are `* [Title](https://...)` and render as outbound links in the nav.
   - **Cross-space links** in SUMMARY.md use the same `https://app.gitbook.com/s/<spaceId>/<path>` form as in body content. Path has no `.md` suffix. During scaffolding write the sentinel form (`XSPACE_<KEY>`); resolve after space creation. See `references/cross-space-links.md`.

If your scaffolding helper auto-generates a SUMMARY.md by walking folders, **make it idempotent and skip files that already exist**. A user-edited SUMMARY.md should never be silently clobbered — that's how hand-tuned navigation gets lost.

### Per-page markdown — defer to write-gitbook, but reach for the rich blocks

**For all markdown files** — `README.md`, `SUMMARY.md`, every page — follow the `write-gitbook` skill. It is the authoritative reference for:

- **Frontmatter** including the `icon:` field. Icons are Font Awesome names without the `fa-` prefix (e.g. `book-open`, `bolt`, `house`, `code`, `puzzle-piece`, `id-card`, `circle-dollar-to-slot`). Don't invent names — pick from the Font Awesome catalogue. The example site uses these in nearly every page's frontmatter.
- **Layout flags** including `layout: width: wide` (use selectively — on marketing-style landing pages, on changelog pages with the Updates timeline, on pages with multi-column blocks or genuinely wide tables. **Don't default to wide for every space homepage** — the GitBook default width is right for documentation, including documentation landing pages with card-tables. Wide is for hero-style marketing layouts, not normal docs.), `cover:` images, and per-page visibility flags (`title.visible`, `tableOfContents.visible`, etc.).
- **`SUMMARY.md` grammar.** Strict format — one bullet per page, optional `## Group name` headings, no extra formatting. Plus the special `type: builtin:openapi` syntax for auto-generating endpoint pages from a spec.
- **Rich blocks** — tabs, hints, steppers, columns, card-tables, expandables, embeds, conditional content with `{% if visitor.claims... %}`, the OpenAPI block, the **Updates** block (changelog), reusable content includes.
- **GitBook-flavoured markdown differences** from CommonMark.

Don't reinvent any of that here. The bundled `references/example-site/` is the best practical reference for what idiomatic content looks like.

### Choosing the right block — actively, not by default

A common failure mode: Claude generates docs that *work* but use plain markdown for everything, missing the rich blocks that make GitBook sites feel like a real product. **The skill should actively reach for specialized blocks**, not fall back to bare prose-and-bullets. Concrete patterns to internalize:

- **Changelogs** → `{% updates %}` block with `{% update date="..." tags="..." %}` entries. Auto-generates RSS, supports tags (defined in `.gitbook/tags.yaml`). Don't write `## YYYY-MM-DD` headings — that's the wrong shape.
- **API endpoint references** → OpenAPI spec uploaded once, auto-generated pages via `type: builtin:openapi` in SUMMARY.md. Don't hand-author endpoint pages — they drift, and the spec is canonical anyway. If the user doesn't have a spec, offer to draft a minimal one rather than going prose-y.
- **State machines, flows, sequences, simple architecture** → ` ```mermaid ` fenced blocks. Don't draw boxes-and-arrows in ASCII; Mermaid is supported, renders cleanly, and is screen-reader friendly.
- **Space homepages** → use the GitBook default layout for normal docs landings (TOC visible, default width). Reach for `layout: width: wide` only when the page is genuinely marketing-style — a hero image, an unusually large card grid, a multi-column dashboard layout. The default is right for docs.
- **"Choose your path" content** → card-tables (`<table data-view="cards">`). The HTML is verbose but the visual result beats any markdown alternative.
- **Side-by-side intro patterns** → `{% columns %}` block. Two columns at 50/50 is the standard.
- **Repeated boilerplate (3+ places)** → `.gitbook/includes/<name>.md` + `{% include "..." %}`.
- **Repeated literals (env URLs, support email, version pin)** → `.gitbook/vars.yaml` + `<code class="expression">space.vars.<name></code>`.
- **Multi-language code samples** → `{% tabs %}` block.
- **Walkthroughs of 3+ ordered steps** → `{% stepper %}` block.

The full block-by-block guide, with example invocations and a smell-vs-fix decision table, is in `references/block-ecosystem.md`. **Read it before generating any non-trivial page**, and walk the decision table for each content area being scaffolded — ask "is there a specialized block for this?" before defaulting to plain markdown.

### Cross-space links

Multi-space sites *want* cross-space links — they're how a site feels like one connected product, not a bunch of separate manuals. **Don't duplicate content to avoid them, and don't drop them.** They're a first-class GitBook feature; the only twist is that they need real space IDs to render correctly, and IDs only exist after the site is created via the API.

The pattern in markdown is just a regular link to the GitBook URL of the target space:

```markdown
For the conceptual side, see the [Authentication concept page](https://app.gitbook.com/s/<spaceId>/concepts/authentication).
```

GitBook resolves `https://app.gitbook.com/s/<spaceId>/<path>` at render time, regardless of your custom domain. Internally these are `ContentRefPage` or `ContentRefSpace` content references with the space ID set; in markdown they just appear as URLs.

**The scaffolding flow:**

1. **During scaffolding**, write cross-space links using a sentinel space-ID prefixed with `XSPACE_`, one per planned space. Use the space slug from your structure plan as the suffix:

   ```markdown
   See the [Authentication concept page](https://app.gitbook.com/s/XSPACE_GUIDES/concepts/authentication).
   For the full reference, see the [API Reference](https://app.gitbook.com/s/XSPACE_API/).
   ```

   These are valid markdown links to non-existent GitBook spaces — they don't break the parser, they're easy to grep for, and they round-trip cleanly through Git.

2. **After space creation**, when the API returns each new space's real ID, walk every markdown file and substitute `XSPACE_<KEY>` with the real space ID:

   ```bash
   sed -i \
     -e "s|XSPACE_GUIDES|${GUIDES_SPACE_ID}|g" \
     -e "s|XSPACE_API|${API_SPACE_ID}|g" \
     -e "s|XSPACE_CHANGELOG|${CHANGELOG_SPACE_ID}|g" \
     $(find . -name '*.md' -not -path './.git/*')
   ```

3. **Commit and push** the resolution. GitBook will pick it up via Git Sync and the links will resolve on the next render.

For a clean implementation, keep a `cross-space-links.yaml` in the repo root mapping sentinel keys to space IDs, generated after creation. That makes the resolution script reproducible if anyone re-runs it. The full pattern, including anchor links, page-specific links, and a sample resolution script, is in `references/cross-space-links.md`.

**Where this gets written into:** the scaffold (with sentinels), the markdown content as you generate it across spaces, and the post-creation step in the API workflow. Don't try to write real `app.gitbook.com/s/<id>/...` links during scaffolding — IDs don't exist yet, and any guess will be a broken link.

### Where to look for example content

`references/example-site/` is a **pruned snapshot** of a production-style GitBook site bundled with this skill. The original is a 12-space site (home, three product spaces, three versions of a developer API, three guides spaces, partners, changelog, plus an external-content `connections/` tree) with ~200 content files; the bundled snapshot keeps ~150 to stay within file-count limits.

**Read `references/example-site/PRUNE-NOTES.md` first** — it explains exactly what was kept and dropped, and lists the highest-signal files to read for specific patterns. The TL;DR:

- The full structural backbone of every space is intact — `README.md`, `SUMMARY.md`, `.gitbook/vars.yaml`, `.gitbook/includes/`.
- `developers/v2/` is kept in full as the canonical example. `developers/v1/` (legacy) and `developers/v3/` (beta) were dropped — they were structurally identical to v2 with version-specific content variations. The pattern of multi-version API docs is documented in PRUNE-NOTES.md and visible in `structure.json`.
- `connections/` — each subfolder (`blog/`, `community/`, `youtube/`) keeps its `index.html` plus one representative article so the metadata patterns stay learnable.
- `customization.json` and `structure.json` are the complete API exports describing the entire original site, including spaces and pages that were pruned. SUMMARY.md files inside each space also describe the original tree — some links in them point to pruned pages, which is expected.

Notable files to study, **organized by pattern you're trying to demonstrate**:

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

When you need a pattern not represented in the bundled snapshot (e.g. legacy/beta versioned API spaces side-by-side, the full external-content article catalogue), `structure.json` is the authoritative source for shape, and PRUNE-NOTES.md describes the patterns those omissions represented.


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

## Migration and content quality

Most real builds aren't greenfield — they're migrations from another docs platform (Mintlify, Docusaurus, ReadTheDocs, an older GitBook), or restructurings of existing markdown. These have their own discipline that's distinct from "make a new site." Get this wrong and you produce something that *looks* like a docs site but reads like a machine output.

The full workflow is in `references/migration-from-other-platforms.md`. The headlines:

**Mirror the source before reimagining it.** When the user has an existing live docs site, fetch the rendered landing pages and look at them before generating any homepage content. The current IA is the spec; the user's reasons for it usually aren't visible from a folder of markdown alone. Inventing card grids, hero blocks, and "what's new" sections from scratch when the source already had a working answer is the most common content-quality failure mode.

**A bulk export is rarely a complete content source.** Mintlify's `llms-full.txt`, ReadTheDocs HTML scrapes, and similar AI-friendly exports often strip visible content (custom components rendered to raw markup, AI-prompt blocks unrolled inline, parameter names dropped from API tables). After bulk conversion, sample-check the rendered pages against the original site and flag where content is missing — don't pretend the export is the whole story.

**Anchor pages, not all pages.** Migrating 280 pages doesn't mean hand-crafting 280 pages with GitBook idioms. The right move is to bulk-convert the long tail, then deliberately rebuild 4–6 anchor pages — homepage, top-level landing per space, the marquee how-to — using the full block ecosystem. The rest can be brought up to standard iteratively.

**Format-pass is a documented step.** Naive markdown conversion leaves artifacts (foreign component tags, malformed code fences, broken internal links). After bulk conversion, run a clean-up pass before the first commit — remove unsupported components, normalize fences, rewrite `/docs/...` paths to GitBook URLs or relative paths. Skipping this produces a repo that *almost* renders.

**Don't auto-generate frontmatter you don't have.** When the source had no icons, don't auto-pick icons from URL slugs — you'll produce a sea of mismatched cog icons. When the source had no description, leave the field blank; don't stub it with `Source: <url>` (that text leaks into sidebar previews and search).

**OpenAPI-first for API references.** If the migrated site has API reference content and you can get an OpenAPI spec (or generate one from their codebase), route the entire reference space through `builtin:openapi`. A 70-page hand-converted reference is almost always worse than a 3-file auto-generated one.

**Internal-link conversion is a sweep, not a per-page concern.** After the structure is known, walk every markdown file and rewrite `/docs/...` links to either relative `.md` paths (within a space) or `https://app.gitbook.com/s/<spaceId>/<path>` URLs (across spaces). Doing this per-page-as-you-go produces inconsistent links; doing it as one sweep with a slug-to-path manifest is much more reliable.

**Be careful with helper scripts that regenerate content.** If you're using a converter or SUMMARY-generator, make it idempotent by default. Skip files that already exist. A second run that clobbers hand-tuned homepages is a footgun. Never run `rm -rf <space>/` on a directory that might contain hand-edited content; if you must regenerate, write to `<space>/_generated/` and merge or diff.

## Driving the GitBook API

All endpoints are at `https://api.gitbook.com/v1`. Auth is `Authorization: Bearer $GITBOOK_TOKEN`. The full set of calls used by this skill, with curl-friendly request bodies, is in `references/api-cheatsheet.md`. Read it before making API calls — the schemas are nuanced (especially customization).

### The standard sequence for a new site

1. **Verify the token and find the org**: `GET /v1/user`, then `GET /v1/orgs`.
2. **Create the site**: `POST /v1/orgs/{organizationId}/sites` with `{title, type, visibility, spaces?}`. **Default to Ultimate** (`type: "site"` is the API value; the plan tier is set on the site after creation or via the org's billing). Use `type: "basic"` (free) only when the user explicitly opts in. Don't include `spaces` if no spaces exist yet — you can add them later.
3. **Decide how spaces will come into being.** Two paths:
   - **Git-Sync-first (recommended)**: tell the user to create each space in the GitBook UI by clicking "Add new space" → "Sync to a GitHub or GitLab repository", picking the repo and the per-space project directory. This creates the space, sets up sync, and links it to the site in one action. The skill's job is to give exact, copyable instructions (one block per space). See `references/git-sync-handoff.md`.
   - **API-first**: create empty spaces via the API (the skill's API cheatsheet covers this), add them to the site with `POST /v1/orgs/{orgId}/sites/{siteId}/site-spaces`, and use the Imports API or template application to load content. The user will still need to wire Git Sync in the UI later if they want bidirectional sync.
4. **Add sections** (multi-space sites with grouped navigation): `POST /v1/orgs/{orgId}/sites/{siteId}/sections`. A section is created by associating a space with a title and optional icon.
5. **Resolve cross-space link sentinels**: if the scaffolded markdown contains `XSPACE_<KEY>` placeholders (which it should, for any link that crosses a space boundary), now is when you substitute them for the real space IDs returned by step 3 or 4. See `references/cross-space-links.md` for the substitution script. Commit and push the changes — the next Git Sync run picks them up.
6. **Apply customization** (branding): `PUT` the `SiteCustomizationSettings` for the site or for individual site-spaces. The full schema is broad — theme preset, colors (each as a `{light, dark}` themed pair), favicon, header (logo, primaryLink, links), footer (groups of links, copyright), themes (default light/dark, toggleable), AI mode, PDF export, and more. Recipes for common branding scenarios are in `references/customization-recipes.md`.
7. **Verify**: `GET /v1/orgs/{orgId}/sites/{siteId}/structure` to see the final tree and `GET .../customization` to confirm settings.

### Multi-language sites and auto-translated spaces

GitBook supports **auto-translated site-spaces**: a single English space (synced from Git) can be paired with computed translations in other languages. The translations are not separate spaces in the Git repo — they live entirely in GitBook and are configured through the UI under each section's settings. The API exposes them as additional `site-space` objects under the same section, each with a different `language` and no `gitSync` field.

What this means in practice:

- **Don't scaffold per-language directories in the repo.** The Git repo has one space per topic, in English. The skill writes one set of markdown files per content area, full stop.
- **Each section can hold many site-spaces.** A "Payments" section might contain `Payments` (en, git-synced), `Payments (FR)` (fr, computed), `Payments (DE)` (de, computed), etc. The structure response will list all of them; only the English ones need a Git Sync handoff.
- **`localizedTitle` shows up everywhere.** Sections, section-groups, header links, footer links, and the site title itself all carry a `localizedTitle: {de: "...", fr: "...", ...}` map. When reading the customization, expect to see translations even for fields the user only set in English. Don't strip these out unless asked.
- Auto-translation is a UI-only feature today. If the user wants it enabled on a section, surface that as part of the Git Sync handoff: "After Git Sync is configured, go to **Site → Sections → Payments → Translations** and enable the languages you want."

When the user asks for "a docs site in five languages", the answer is one English content tree in Git plus auto-translation enabled per section in the UI — not five copies of the markdown.

### Section groups

A site's structure has three possible levels of nesting in the navigation:

1. **Site-spaces** at the root (a flat site, no sections)
2. **Sections** containing site-spaces (the typical multi-space site)
3. **Section groups** containing sections containing site-spaces (used to bucket related sections, e.g. "Products" group containing Payments / Identity / Connect sections)

The `GET /v1/orgs/{orgId}/sites/{siteId}/structure` response is recursive — a section-group's `sections` array can hold both sections and other section-groups. When designing the structure, use section-groups only when there are 3+ closely related sections that benefit from being visually grouped in the top nav. For a 2-section site, sections at the root level are clearer.

### Updating an existing site

When asked to modify a site that already exists, *always* fetch the current state first:

- `GET /v1/orgs/{orgId}/sites/{siteId}` for site metadata
- `GET /v1/orgs/{orgId}/sites/{siteId}/structure` for sections + spaces
- `GET /v1/orgs/{orgId}/sites/{siteId}/customization` (or the per-site-space variant) for branding

Then make targeted PATCH/PUT/POST/DELETE calls. Don't replace whole customization payloads if you only mean to change one field — get the current settings, modify in memory, and PUT the result back.

### When to use Imports vs. Git Sync

- **Imports API** (`POST /v1/org/{orgId}/imports`) is for ingesting external content (a website URL, a set of files) into a space. It's good for one-shot migrations from another doc tool.
- **Git Sync** is for ongoing two-way sync between a Git repo and a space. This is what we're optimizing for in the standard flow.
- If the user has already-good content sitting outside both Git and GitBook (e.g. a Notion export), use Imports to get it in, then optionally turn on Git Sync afterward.

## Branding and customization

The `SiteCustomizationSettings` schema is large. The bundled `references/example-site/customization.json` is a real export from a production-style demo and is the most useful reference — read it before composing any customization payload. It shows how all the nested fields fit together, how `localizedTitle` maps work, and how conditional header links are structured.

Fields that matter most for "make this site look like our brand":

- **`title`** — site title (the one shown in the header). Plus `localizedTitle: {en: ..., fr: ..., ...}` for translations.
- **`styling.theme`** — preset: `clean` (default-modern), `muted` (low-contrast), `bold` (high-contrast), or `gradient` (colorful)
- **`styling.primaryColor`** — `{light: "#xxxxxx", dark: "#xxxxxx"}` — the brand color, used for links, buttons, accents
- **`styling.tint`** — `{color: {light, dark}}` — a subtle tint applied across text, icons, and UI elements (search bar, etc.). Does **not** affect link/button colour (those keep `primaryColor`). This is the field most brand guides mean when they say "background tint" or "secondary surface colour".
- **`styling.infoColor` / `successColor` / `warningColor` / `dangerColor`** — semantic colors, each a themed pair
- **`styling.font` / `styling.monospaceFont`** — pick a preset (`Inter`, `IBMPlexMono`, etc.) or supply a custom font definition with hosted woff2 files
- **`styling.corners`** — `straight | rounded | circular`
- **`styling.depth`** — `subtle | flat`
- **`styling.icons`** — `regular | solid | duotone | light | thin`
- **`styling.sidebar.background`** — `default | filled`
- **`styling.sidebar.list`** — `default | pill | line`
- **`styling.codeTheme.default` / `styling.codeTheme.openapi`** — themed code-block colors
- **`styling.search`** — `prominent | subtle`
- **`favicon`** — `{icon: {light, dark}}` (themed URLs) or `{emoji: "📘"}`
- **`header.logo`** — `{light: <url-shown-in-light-mode>, dark: <url-shown-in-dark-mode>}` (Premium feature). The schema field name is the *mode the URL is shown in*, not the colour of the file. Brand guides often use ambiguous file names like `logo-dark.svg` (which can mean "the dark-coloured logo" — for light backgrounds — or "the logo for dark mode" — a light-coloured file). When in doubt, ask the user explicitly.
- **`header.links`** — top-nav items. Each item has `title`, `style` (`link | button-primary | button-secondary`), `to` (a `ContentRef` — see below), `links: []` (for sub-menus), and an optional `condition` for conditional visibility.
- **`footer.logo`** — same shape as header.logo (Premium)
- **`footer.groups`** — grouped link lists for the footer. Each group has `title` (with optional `localizedTitle`) and `links`.
- **`footer.copyright`** — string up to 300 chars
- **`themes.default`** — `light | dark | system`; `themes.toggeable` controls whether visitors can switch
- **`ai.mode`** — `none | search | assistant`; `ai.suggestions` for canned questions
- **`pageActions`** — booleans: `externalAI` (open-in-ChatGPT), `markdown` (copy as markdown), `mcp` (connect via MCP)
- **`pagination.enabled`** — prev/next page links at the bottom of pages
- **`feedback.enabled`** — page feedback widget
- **`pdf.enabled`** — PDF export button
- **`socialAccounts`** — list of `{handle, platform, display: {footer, header}}` for icons in header/footer
- **`git.showEditLink`** — whether the "Edit on GitHub" link appears on git-synced pages
- **`externalLinks.target`** — `self | blank` for outbound links
- **`insights.trackingCookie`** — whether GitBook places its analytics cookie
- **`advancedCustomization.enabled`** — whether advanced CSS/JS is allowed (Enterprise)
- **`announcement`** — site-wide banner: `{enabled, message, link?, style: info|warning|danger|success}`

A handful of fields are present in responses but **deprecated** and should not be set on new sites: `internationalization.locale`, `header.preset` (use `styling.theme`), `header.backgroundColor`, `header.linkColor`. Leave existing values alone when round-tripping a GET; just don't introduce them.

One quirk: `styling.background` reads as deprecated in some docs, but the API rejects POST/PUT without it (`422 expected "background" to be defined`). Treat it as required-but-vestigial — set to `"plain"` on new sites, or echo whatever GET returns on round-trip updates. Modern theming runs through `styling.tint` instead.

Similarly, every entry in `header.links[]` requires a `links: []` array even when there's no sub-menu. The API rejects link items without it.

### Content references (the `to` field)

Header links, footer links, and `header.primaryLink` all use a `ContentRef` to specify destination. Three forms:

- **External URL**: `{kind: "url", url: "https://..."}`
- **Whole space**: `{kind: "space", space: "<spaceId>"}`
- **Specific page**: `{kind: "page", page: "<pageId>", space: "<spaceId>"}` (use this to deep-link to e.g. the latest changelog entry)

### Conditional links

Header links can carry a `condition` field — a JS-like expression evaluated against `visitor.claims`. Pattern from the example site:

```json
{ "title": "Sign in",  "condition": "visitor.claims.unsigned.persona !== \"partner\"", ... }
{ "title": "Sign out", "condition": "visitor.claims.unsigned.persona === \"partner\"",  ... }
```

This is how the same site shows different navigation to logged-in vs. logged-out visitors. The conditions reference visitor claims that GitBook resolves at render time.

A few features (custom logos, custom fonts, semantic colors, footer logo, advanced customization, disabling the GitBook trademark) require Premium or Ultimate site plans. The API will reject these on free sites with 400/403 — handle the error gracefully and tell the user.

`references/customization-recipes.md` has worked examples for: minimal brand pass (just colors + favicon), full brand with logos and fonts, dark-mode-only with toggle, and AI-assistant enabled with suggested prompts.

For a complete real-world payload to learn from, `references/example-site/customization.json` is the customization export of a production site bundled with this skill. Reading it is the fastest way to see how all the fields fit together in practice — much more useful than the abstract schema. Don't paste it wholesale into a new site; use it as a model for shape and field selection.

For a real example of the structure response (sections, section-groups, multi-language site-spaces), see `references/example-site/structure.json` alongside it.

## The Git Sync handoff

This is the part that has to feel polished. Once the repo is pushed and the site exists, generate a clear set of per-space instructions. For each space, the user needs:

1. The repo URL
2. The branch name (usually `main`)
3. The **project directory** for that space (e.g. `guides`, `api-reference`)
4. The initial sync direction — almost always **GitHub → GitBook** (or GitLab → GitBook), since the repo is the source of truth at this point

`references/git-sync-handoff.md` has a template you can fill in and present to the user. Render it as a numbered list per space, not as one big wall of prose. After they finish, ask them to confirm — at that point you can fetch `GET /v1/spaces/{spaceId}/git/info` to verify each space's sync state programmatically.

## Common mistakes to avoid

- **Don't put the PAT in any file Claude writes.** Always read it from the environment.
- **Don't try to set up Git Sync via the API.** It will fail; the API is read-only for this. Always route through the UI handoff.
- **Don't paste an entire customization payload from memory.** GET the current state, modify, PUT it back. Schemas evolve and you'll write fewer bugs this way.
- **Don't create a space for every section of content.** A space is a heavy unit (it has its own URL slug, sync, settings). Pages and folders within a space are the right tool for sub-grouping.
- **Don't skip the structure-plan-and-confirm step**, even when the user is in a hurry. Restructuring a published site is painful.
- **Don't over-format the SUMMARY.md.** GitBook's parser is strict about it. Defer to the rules in `write-gitbook`.

## Reference files

- `references/api-cheatsheet.md` — the complete set of API calls used by this skill, with curl-style request bodies and expected responses
- `references/site-structure-design.md` — heuristics and worked examples for going from raw inputs to a space/section/page plan
- `references/migration-from-other-platforms.md` — pre-flight, source-platform mappings (Mintlify, Docusaurus, GitBook v1, RTD), anchor-pages strategy, format-pass, internal-link sweep. **Read this before any migration build, not after.**
- `references/block-ecosystem.md` — which GitBook block to reach for in which content situation, with a decision table and worked examples (Updates, Mermaid, OpenAPI auto-gen, layout flags, card-tables, conditional content, includes, vars). **Read this before generating any non-trivial page.**
- `references/cross-space-links.md` — the sentinel-and-resolve workflow for cross-space links in markdown, with a working substitution script
- `references/git-sync-handoff.md` — the template for the user-facing Git Sync setup instructions
- `references/customization-recipes.md` — worked branding payloads for common scenarios
- `references/example-site/` — a pruned snapshot (~150 files) of a real production-style GitBook site repo (markdown, `SUMMARY.md`s, `.gitbook/` configs). Read `PRUNE-NOTES.md` inside it first — it explains what's kept, what's dropped, and lists high-signal files for specific patterns.
- `references/example-site/customization.json` — the customization export from that site, illustrating a complete real-world branding payload
- `references/example-site/structure.json` — the structure export, showing sections, section-groups, and multi-language site-spaces (English git-synced + auto-translated)
