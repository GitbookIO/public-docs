# SUMMARY.md grammar

The `SUMMARY.md` file defines a space's table of contents and navigation structure. It's a markdown file with a specific format that mirrors the sidebar navigation in GitBook.

For the broader scaffolding context (folder layout, when SUMMARY is optional, etc.), see `repo-scaffolding.md`. For SUMMARY.md generation patterns when scaffolding from scratch, see `repo-scaffolding.md` § "Generating SUMMARY.md".

## Contents

- Basic structure
- Key rules
- Page link titles (optional)
- Indentation and nesting
- Special bullet types (external links, cross-space, OpenAPI)
- Important notes / common pitfalls

## Basic structure

```markdown
# Summary

## Use headings to create page groups like this one

* [First page's title](page1/README.md)
    * [Some child page](page1/page1-1.md)
    * [Some other child page](page1/page1-2.md)
* [Second page's title](page2/README.md)
    * [Some child page](page2/page2-1.md)
    * [Some other child page](page2/page2-2.md)

## A second page group

* [Another page](another-page.md)
```

## Key rules

- Use `#` for the main title (commonly "Table of contents" or "Summary")
- Use `##` headings to create page groups (section headers in the sidebar)
- Use `*` for unordered lists to define pages and subpages
- Indent with spaces (not tabs) to create nested/child pages
- Each list item should be a markdown link: `[Link text](path/to/file.md)`
- Paths are relative to the location specified in `.gitbook.yaml` (typically the root)
- **README.md is on its own line at the very top, as a sibling**, not a parent
- **One bullet per page, no extra formatting** — no bold, no descriptions in the SUMMARY (those live in the page frontmatter)

## Page link titles (optional)

You can define a different title for the sidebar navigation versus the page itself:

```markdown
# Summary

* [Page main title](page.md "Page link title")
```

The text in quotes ("Page link title") will be used in:

- The table of contents sidebar
- Pagination buttons at the bottom of pages
- Any relative links to that page

## Indentation and nesting

Two-space (or four-space) indentation under a bullet creates a child page. Don't mix tabs and spaces. Keep nesting shallow — 1–2 levels is best. Deeper nesting tends to make the sidebar unreadable.

## Special bullet types

### External links

```markdown
* [GitHub repo](https://github.com/example/repo)
```

Renders as an outbound link in the nav.

### Cross-space links

```markdown
* [API Reference](https://app.gitbook.com/s/<spaceId>/)
```

Path has no `.md` suffix. During scaffolding write the sentinel form (`XSPACE_<KEY>`); resolve after space creation. See `cross-space-links.md`.

### OpenAPI auto-generated endpoint pages

Use a fenced YAML block as the bullet content (`type: builtin:openapi`):

```markdown
## Feedback API

* [Overview](feedback/README.md)
* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: true
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: my-api-v1
  ```
```

See `custom-blocks.md` § "OpenAPI specifications" for the full pattern.

## Important notes / common pitfalls

- **SUMMARY.md is optional.** If not provided, GitBook infers structure from your folder hierarchy.
- **You cannot reference the same markdown file twice in SUMMARY.md** (each page has only one URL).
- **GitBook updates SUMMARY.md automatically when you edit through the GitBook UI.** Be aware of this if you're also editing it via Git Sync.
- **The file structure reflects exactly what users see in the navigation sidebar.**
- **Don't mix tab/space indentation in SUMMARY.md** — the parser is strict.
- **Group names come from the user, not the folder names.** "concepts/" can be the folder slug, but the group heading might be "How it works" if that's clearer.
- **Avoid the "* README.md" + nested-everything-under-it antipattern.** That collapses the entire nav into one tree under the homepage and makes every page look like a sub-page of the homepage in the sidebar. Top-level pages should be siblings of README.md, not children.
