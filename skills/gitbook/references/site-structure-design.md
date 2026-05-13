# Site structure design

A solid information architecture is the difference between docs people use and docs they bounce from. This file captures the heuristics for going from raw inputs to a structure plan that you'll show the user before scaffolding any files.

## The output of this step

By the end, you should have three things, all small and reviewable:

1. **The space list** — usually 1 to 4 spaces. Each space gets a one-sentence description and an emoji.
2. **The section grouping**, only if multi-space — sections are top-nav buckets that hold spaces.
3. **The page tree per space** — folders and pages. Each page gets a 1-line description.

That plan goes to the user before any files get written. Restructuring later is fine inside Git but expensive after publish.

## Heuristics for picking spaces

A space is a heavyweight unit: its own URL slug, its own Git Sync, its own customization overrides, its own visibility settings, and its own search scope. **Don't split content across spaces unless the audiences or lifecycles really differ.**

Useful prompts to decide:

- **Different audiences** — end users vs. developers vs. ops staff usually want their own space.
- **Different lifecycles** — a changelog updates daily; user docs update with releases; an architecture overview updates rarely. These benefit from being separate.
- **Different review processes** — if API reference is auto-generated from OpenAPI but user docs are hand-edited, splitting them makes the auto-update story cleaner.
- **Different visibility** — internal runbooks alongside public docs probably want separate spaces (and possibly separate sites).

When in doubt, **start with fewer spaces.** Splitting later is cheaper than merging.

### Common multi-space shapes for SaaS / API products

- **Two-space**: `Guides` (everything narrative) + `API Reference` (endpoint-by-endpoint). The simplest case.
- **Three-space**: `Guides` + `API Reference` + `Changelog`. Add this when release notes are frequent and substantial.
- **Four-space**: `Guides` + `API Reference` + `Changelog` + `SDKs`. Add SDKs as its own space when there are 3+ language bindings each with their own narrative.
- **Plus a separate internal space**: when there's an internal handbook or runbook content that shouldn't live alongside public docs, that's a different *site* (or a private space added to the same site with restricted visibility), not just another section.

## Heuristics for sections

Sections are top-level navigation groupings *within* a site. They show up as the top-nav row above each space's sidebar. Use sections when you have 3+ spaces and want them grouped — for example, "Product" (Guides + Tutorials) and "Developers" (API + SDKs).

If the site has only 1 or 2 spaces, skip sections — they add UI clutter without clarifying anything.

A section with a single space is fine as long as the section title clarifies the audience or topic in a way the space title alone wouldn't.

## Designing the page tree per space

The default rule of thumb: **shallow is better than deep.** A two-level tree (groups → pages) handles most spaces. Three levels is the upper limit before navigation gets disorienting.

### Patterns that tend to work

For a guides space:

```
README.md (overview, value prop, "what you can do here")
getting-started/
  installation.md
  quickstart.md
  first-project.md
core-concepts/
  <one page per concept, named with the noun>
how-to/
  <one page per task, named "Verb the Object">
reference/
  cli.md
  configuration.md
troubleshooting.md
```

For an API reference space (when not using OpenAPI auto-generation):

```
README.md (auth overview, base URL, conventions)
authentication.md
errors.md
rate-limits.md
endpoints/
  <one page per resource, with all its methods on the same page>
webhooks/
  <one page per webhook event>
```

For a changelog space:

```
README.md (subscribe links, deprecation policy)
2026/
  2026-04.md
  2026-03.md
  ...
2025/
  ...
```

### Anti-patterns to avoid

- **Mirroring an org chart.** Users don't care which team owns what; group by topic, not by reporting line.
- **One page per tiny topic.** If a page is going to be three sentences, fold it into a longer page.
- **Deep nesting "for organization".** Three folders deep usually means the second-level grouping is wrong.
- **Inconsistent naming.** Pick "verb the noun" or "Noun" for page titles and stick with it within a space.

## Going from raw inputs to a plan

### When the user has a folder of existing markdown

Start by listing all the files and reading the first ~100 lines of each. Look for:

- **Filenames as a signal** — `installation.md`, `auth.md`, `how-to-deploy.md` already suggest groupings.
- **Cross-references** — files that link to each other heavily belong in the same space.
- **Frontmatter** — if there's existing frontmatter with categories or tags, use it.
- **README files** — existing README.md or index.md files reveal the user's mental model.

Propose a structure that respects existing groupings where they're sensible, but call out reorganizations explicitly: "I'm proposing to move `legacy-api.md` from the top level into a `reference/` folder — does that work?"

### When the user has examples and content sketches

Read the examples (especially competitor docs the user pointed to) for structural ideas, but don't copy them blindly. Ask:

- What's the smallest set of pages that would make a v1 of this site useful?
- Which 3-5 questions will most readers arrive with? Make sure those have obvious entry points.
- What's the user journey from "first time visitor" to "power user"? The structure should support that journey.

A good v1 is usually 8–20 pages across 1–2 spaces. Don't pad with placeholders — empty pages hurt more than missing pages.

### When the user gives only a description

Ask one focused clarifying question to nail down audience and scope, then propose a minimal structure. Example questions:

- "Is this for end users of the product, developers integrating with it, or both?"
- "Should the docs site be public, or behind authentication?"
- "Are there any sections you absolutely need on day one — pricing, FAQ, status?"

Then propose, e.g., a single-space site with `README.md`, `getting-started/`, `how-to/`, and `reference/` — and iterate from there.

## Worked examples

### Example 1 — Open-source CLI tool, single contributor

**Inputs:** GitHub repo, README, CHANGELOG.md, a few notes in `docs/`.

**Plan:**
- Single-space site, name "Acme CLI Docs"
- Tree:
  ```
  README.md (overview + install one-liner)
  installation.md
  commands/
    <one page per top-level command>
  configuration.md
  troubleshooting.md
  changelog.md (linked from README.md, kept up to date manually)
  ```
- Branding: clean theme, primary color from the project's logo, GitHub footer link.

### Example 2 — Series-A SaaS with a public API

**Inputs:** Marketing site, internal Notion with scattered guides, an OpenAPI spec, a brand guide.

**Plan:**
- Three-space site, sections: "Product" (Guides), "Developers" (API Reference, Changelog)
- Spaces:
  - `guides/` — onboarding, how-tos, concepts, integrations
  - `api-reference/` — generated from the OpenAPI spec; pages organized by resource
  - `changelog/` — quarterly, with date-stamped entries
- Branding: brand color, custom logo, Inter font, footer with company links and a "Status" link

### Example 3 — Restructure an existing site

**Inputs:** An existing GitBook site with one over-stuffed space ("Documentation"), 80+ pages.

**Plan:**
- Don't reorganize without reading the current structure first (`GET .../structure`)
- Propose splitting into `Guides` + `API Reference`, with the API content moving wholesale
- Identify which pages are heavily linked and minimize their path changes (or set up redirects in `.gitbook.yaml`)
- Show the proposed before/after diff to the user before any moves

## Sign-off

After producing the plan, ask the user something like:

> Here's the proposed structure. Anything you'd change before I scaffold the repo and create the spaces? Specifically: (1) does the space split feel right, (2) are there any pages I've missed or grouped wrong, (3) any naming you'd tweak?

Wait for explicit confirmation. Then proceed.
