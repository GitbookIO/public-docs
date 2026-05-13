# Migration from other platforms

Migrating an existing docs site to GitBook isn't the same workflow as building from scratch — it has its own pitfalls and its own opportunities to do less work for a better outcome. This reference covers the platforms most commonly migrated *from* (Mintlify, Docusaurus, GitBook v1, raw ReadTheDocs/HTML scrapes), the pre-flight checks that catch missing content, the format-pass that catches conversion artifacts, and the anchor-pages strategy that produces a quality result without hand-crafting the long tail.

Read this **before** you start converting files. The biggest content-quality failures in migrations come from skipping the pre-flight, not from any specific bad conversion.

## Pre-flight: understand what you actually have

Before generating a single GitBook file, do these:

### 1. Fetch the rendered source

If the original site is live, fetch the rendered landing page for each section/space-equivalent. The user's IA is *visible* on the rendered site in ways that aren't visible in a folder of markdown — card layouts, callout densities, pinned sections, "what's new" blocks, persona switchers, navigation bar links.

```bash
# At minimum, save the rendered homepage and one representative deep page from each section
curl -sL "https://docs.example.com/" -o /tmp/source-home.html
curl -sL "https://docs.example.com/api-reference/" -o /tmp/source-api-home.html
```

These get used as the spec for what to mirror, in Step 5 below.

### 2. Catalog the source's information architecture

For each space-equivalent in the source (whatever the platform calls them — categories, sidebars, sections), write down:

- The **top-level pages** and the **named groups** they're organized into. Group names are user-visible and almost always carry meaning that's not encoded in folder names.
- The **landing-page structure** for each space — which cards/links/sections exist on the homepage, in what order, with what icons.
- The **navigation chrome** — header links, footer links, social icons, banner announcements.

This is the input to GitBook structure design. **It is not optional.** Skipping this and inferring structure from folders gives you a docs site that looks like a file tree, not a product.

### 3. Sample-check the bulk export against the rendered site

If the user's migration source is a bulk export (Mintlify's `llms-full.txt`, ReadTheDocs `.zip`, GitBook v1 export), pick three pages — homepage, a marquee how-to, and an API reference page — and **compare the export to the rendered original**. Things that often go missing:

- Custom components (Mintlify's `<Card>`, `<CardGroup>`, `<Tabs>`, `<Accordion>`) collapse to invalid GitBook tags
- AI-prompt blocks (`<Prompt>`, `<RequestExample>`) unroll inline and dominate the page
- API parameter tables strip the parameter names in AI-friendly exports
- Cover images, embedded videos, code-group package-manager labels — all routinely lost
- Internal links pointing to `/docs/...` paths that no longer exist after the move

If the export is missing material content, **flag this to the user immediately** and offer to either fall back to scraping the rendered HTML, or work from the original source repo (`.mdx` files) instead of the export. Don't silently produce a half-content site.

## Source-platform mappings

### Mintlify (`.mdx`)

The most common migration source. Mintlify uses `.mdx` with React components; GitBook uses extended markdown with custom block syntax.

| Mintlify component | GitBook equivalent |
|---|---|
| `<Card title="..." icon="...">` | A row in a `<table data-view="cards">` |
| `<CardGroup cols={3}>` | The full `<table data-view="cards">` |
| `<Tabs>` / `<Tab title="...">` | `{% tabs %}` / `{% tab title="..." %}` |
| `<Accordion title="...">` | `<details><summary>...</summary>...</details>` |
| `<Note>` | `{% hint style="info" %}` |
| `<Warning>` | `{% hint style="warning" %}` |
| `<Tip>` | `{% hint style="success" %}` |
| `<Info>` | `{% hint style="info" %}` |
| `<Steps>` / `<Step>` | `{% stepper %}` / `{% step %}` |
| `<CodeGroup>` with `\`\`\`sh npm` fences | `{% tabs %}` blocks — **the package-manager label after the language is the tab title**; converters that strip it lose the structure |
| `<Frame>` | Just an image; the frame chrome doesn't carry over |
| `<Prompt>` | `<details><summary>AI Prompt</summary>...</details>` — otherwise the prompt content unrolls inline and dominates the page |
| `<RequestExample>` / `<ResponseExample>` | A code block, optionally inside a tab |
| `<ParamField name="..." type="..." required>` | A row in an API params table — **note: in `llms-full.txt` exports, `name=` is often stripped; you'll need a re-pass from the original `.mdx`** |
| `<ResendParamField>`, `<YouTube />`, other custom components | Need case-by-case handling — there's no GitBook equivalent for a third-party-author custom component, so either inline a sensible substitute or note in a hint that the original had embedded content |
| `icon={<svg>...</svg>}` (inline SVG in a prop) | Convert the SVG into either a Font Awesome icon name (where one exists) or a separate file under `.gitbook/assets/` referenced via `<img>` — see write-gitbook for SVG handling |
| API reference pages (`api-reference/<endpoint>.mdx`) | **Don't convert these one by one.** Use `builtin:openapi` SUMMARY entries instead — see `block-ecosystem.md`. Mintlify API ref pages are auto-generated from the OpenAPI spec already, so the spec is the source of truth, not the `.mdx` files. |

### GitBook v1 (legacy)

Old GitBook sites export to a similar markdown shape but with different conventions:

- `SUMMARY.md` is at the repo root (not per-space) for single-book sites
- Cover images and rich-block syntax pre-date the current GitBook block ecosystem
- Internal links may use `path/to/page.md` directly (rather than `https://app.gitbook.com/s/...`)

For a v1→current migration, plan to lift content into the new monorepo layout (one folder per space), regenerate per-space `SUMMARY.md` files, and rewrite cross-space links to the resolved-ID pattern.

### Docusaurus

Docusaurus uses `.md` and `.mdx` with sidebars defined in JSON. The conversion is mostly straightforward:

- Sidebar JSON → `SUMMARY.md` (with `## Group name` headings derived from the JSON `category` entries)
- `:::note` / `:::warning` admonitions → `{% hint style="info|warning" %}`
- `<Tabs>` / `<TabItem>` (from `@theme/Tabs`) → `{% tabs %}` / `{% tab %}`
- Frontmatter mostly carries over directly, modulo some Docusaurus-specific keys (`sidebar_label`, `sidebar_position`) that map to SUMMARY ordering
- MDX with React components → case-by-case (most Docusaurus sites use these sparingly)

### ReadTheDocs / Sphinx

reStructuredText → markdown conversion (via `pandoc` or `rst2md`) is lossy. For RTD migrations:

- Run pandoc on each `.rst` to get markdown
- Walk the output for unconverted directives (`.. note::`, `.. code-block::`, `.. toctree::`) and convert them by hand
- The `toctree` is the IA spec — it maps to `SUMMARY.md`

### Generic HTML scrape

When all you have is a live site, scrape the rendered HTML, extract the article body (skip the chrome), and convert to markdown. This is the lowest-fidelity source — expect to do significant rework.

## Anchor-pages strategy

Migrating 200+ pages doesn't mean hand-crafting 200+ pages. The right approach is two-track:

1. **Bulk-convert the long tail** — `.mdx` → `.md` with mechanical component-to-block conversion. Acceptable level of polish: it renders, links work, hints are hints, code blocks are code blocks. Don't try to make every page beautiful.

2. **Hand-craft 4–6 anchor pages** — the homepage, the top-level landing of each space, the marquee how-to, the most-visited concept. These get the full GitBook treatment: card-tables for navigation, Mermaid diagrams instead of ASCII, Updates blocks for changelogs, OpenAPI auto-gen for API references, the right `width` and frontmatter for each.

The anchors set the standard for what the site can look like; the long tail gets brought up to that standard iteratively as the user touches each page in the future. Trying to anchor-quality every page in a single migration is how migrations stall.

When picking anchors, prefer:

- The site homepage (everyone sees it, it sets the visual tone)
- One landing per space (sets the per-space tone)
- The pages with the highest traffic in the source (where polish has the most impact)

## The format-pass

After bulk conversion, run a deliberate clean-up pass *before the first commit*. Naive conversion produces several classes of artifact that don't render well:

### Foreign component residue

Run a grep across the converted markdown for:

```bash
# Unconverted Mintlify components
grep -rn '<Card\|<CardGroup\|<Tabs\|<Tab\b\|<Note\|<Warning\|<Tip\|<Steps\|<Step\b\|<Accordion\|<Frame\|<Prompt\|<ParamField\|<ResendParamField\|<RequestExample\|<ResponseExample\|<YouTube' --include='*.md'
```

Each hit is either a missed mapping (apply the right GitBook block) or a custom component with no equivalent (leave a `<!-- TODO: original used <Foo> -->` marker and a hint asking the user to fill in the gap).

### Code fence metadata

Mintlify supports `\`\`\`bash {3-5}` (highlighted lines), `\`\`\`bash filename="install.sh"`, and other metadata after the fence language. GitBook ignores these and sometimes parses them as part of the language identifier. Strip everything after the language token unless you know the GitBook equivalent:

```bash
# Find code fences with extra metadata after the language
grep -rn '^```[a-z]\+ [^a-z]' --include='*.md'
```

### Broken internal links

Source-platform paths (`/docs/...`, `/getting-started/...`) usually don't survive the migration. After the GitBook structure is known, walk every markdown file and rewrite:

- Within-space links: relative `.md` paths (e.g. `[Authentication](concepts/authentication.md)`)
- Cross-space links: `https://app.gitbook.com/s/<spaceId>/<path>` (use `XSPACE_<KEY>` sentinels during scaffolding — see `cross-space-links.md`)
- External links: leave alone

The script for this is small but specific enough that it's worth writing per-migration:

```python
import re
from pathlib import Path

# Map of old paths (from the source platform) → new GitBook paths
LINK_MAP = {
    "/docs/getting-started/quickstart": "getting-started/quickstart.md",
    "/docs/api/authentication":         "https://app.gitbook.com/s/XSPACE_API/authentication",
    # ... one entry per old path
}

for md in Path(".").rglob("*.md"):
    text = md.read_text()
    new = text
    for old, new_path in LINK_MAP.items():
        new = re.sub(rf']\({re.escape(old)}([#?][^)]*)?\)', f']({new_path}\\1)', new)
    if new != text:
        md.write_text(new)
```

Build the LINK_MAP from the source platform's sitemap or sidebar JSON.

### YAML frontmatter quoting

Source titles with `:`, `#`, or other YAML-significant characters break Git Sync silently when copied verbatim into frontmatter. The format-pass should walk every page's frontmatter and quote `title:` and `description:` values that contain these characters. Cheap to do, expensive to debug if missed.

### Auto-generated icons and descriptions

The two most common bad-default migration patterns:

- **`icon: <something inferred from the URL slug>`** — produces a sea of mismatched cog/info/file icons that look wrong against an originally icon-less source. **If the source had no icons, leave the icon field blank.** Only carry icons forward when the source explicitly had them.
- **`description: "Source: https://old.example.com/page"`** — that string leaks into sidebar previews, search results, and social shares. **If you don't have a real description, leave the field out.** A blank description is much better than a stub one.

These are easy to enforce in the converter: only emit `icon:` and `description:` when the source frontmatter had them; never synthesize.

## Idempotency and homepage hazards

If you're using a custom converter or SUMMARY-generator that runs in steps, make every step idempotent by default:

- **Skip files that already exist.** A second run of the converter that clobbers a hand-edited homepage is the most common painful surprise.
- **Don't auto-promote `<space>/introduction.md` to `<space>/README.md` unconditionally.** Guard with `if not README.exists()`. Otherwise the user's hand-tuned README gets overwritten on every regenerate.
- **Never `rm -rf <space>/` to "regenerate cleanly".** If the converter genuinely needs to start from a clean slate, write into `<space>/_generated/` and let the user merge or diff into the live tree manually. Hand-edited content lives in the live tree; generated content lives next to it.

The general rule: **converters are append-only by default, destructive only on explicit opt-in.**

## Sequencing

A clean migration runs in this order:

1. Pre-flight: fetch source, catalog IA, sample-check the export
2. Plan structure with the user (sections, groups, page lists per space — agreed before any file is written)
3. Bulk-convert the long tail with the format-pass applied
4. Hand-craft the anchor pages
5. Internal-link sweep with the LINK_MAP
6. Resolve cross-space link sentinels (after spaces are created via the GitBook API)
7. Initial commit, push, Git Sync handoff

If you find yourself doing 4 before 3 (anchor pages while bulk content is still missing), or 5 before 2 (link sweeping before the structure is agreed), the migration is going to thrash. The order matters.
