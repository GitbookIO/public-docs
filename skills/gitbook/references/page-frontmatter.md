# Page frontmatter

GitBook supports YAML frontmatter at the top of markdown files to configure page-specific settings. Frontmatter must be placed at the very beginning of the file, before any content.

## Contents

- All available fields (cheat sheet)
- Field descriptions
- Layout options (width, visibility flags, cover)
- YAML quoting in frontmatter (gotcha)
- Complete example

## All available fields (cheat sheet)

```markdown
---
description: Page description used for SEO and page previews
icon: book-open
hidden: true
cover: .gitbook/assets/hero.png
coverY: 0
vars:
  page_variable: value
  another_var: another value
if: visitor.claims.unsigned.isPremium
layout:
  width: default            # or 'wide'
  cover:
    visible: true
    size: full              # or 'hero'
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---
```

## Field descriptions

- **`description:`** — Page description text. Supports multiline with `>-` syntax:

  ```yaml
  description: >-
    This is a longer description
    that spans multiple lines
  ```

- **`icon:`** — Icon name from Font Awesome (e.g., `book-open`, `bolt`, `stars`, `icons`, `brackets-curly`). Names without the `fa-` prefix.

- **`hidden: true`** — Hides the page from the table of contents in published documentation.

- **`vars:`** — Page-level variables (key-value pairs) that can be referenced in expressions. See `variables-and-expressions.md` for usage.

  ```yaml
  vars:
    version: v1.2.3
    api_key: example_key
  ```

- **`if:`** — Adaptive content visibility condition. Controls when the page is visible based on visitor attributes:

  ```yaml
  if: visitor.claims.unsigned.isPremium
  ```

  **Note:** While adaptive content conditions can be set in frontmatter, it's recommended to configure them through the GitBook UI for better maintainability and team visibility.

- **`cover:`** — Path to a hero/banner image displayed at the top of the page. Typically a `.gitbook/assets/` path:

  ```yaml
  cover: .gitbook/assets/home-cover.png
  ```

  Requires `layout.cover.visible: true` to render. Accepts external URLs too.

- **`coverY:`** — Vertical crop offset for the cover image (integer; `0` = centered, positive moves the focal point down, negative up). Useful when the image is taller than the cover band:

  ```yaml
  coverY: -72
  ```

## Layout options

`layout:` controls page layout and which elements are visible. This maps to the "Page Options" settings in the GitBook UI:

- **`width:`** — Page content width
  - `default` — Standard content width
  - `wide` — Wider content area (automatically widens full-width blocks like tables and code)
- **`cover.visible` / `cover.size`** — Control cover rendering. `size` is either `full` (full-bleed hero) or `hero` (smaller banner)
- **`title.visible`** — Show/hide the page title (boolean)
- **`description.visible`** — Show/hide the page description (boolean)
- **`tableOfContents.visible`** — Show/hide the left sidebar table of contents (boolean)
- **`outline.visible`** — Show/hide the right sidebar page outline/headings (boolean)
- **`pagination.visible`** — Show/hide next/previous page navigation links (boolean)
- **`metadata.visible`** — Show/hide page metadata section (boolean)

Example for a landing page with minimal chrome:

```yaml
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: false
  outline:
    visible: false
  pagination:
    visible: false
```

**Use `width: wide` selectively.** Don't default it for every space homepage — the GitBook default width is right for documentation, including documentation landing pages with card-tables. Wide is for hero-style marketing layouts, not normal docs.

## YAML quoting in frontmatter (gotcha)

Always quote `description:` and any other string values that contain YAML-significant characters. Characters that require quoting: `:` (most common), `#`, `[`, `]`, `{`, `}`, `&`, `*`, `!`, `|`, `>`, `'`, `"`, `%`, `@`, `` ` `` (especially at the start of a value). The safe default is to quote any value containing punctuation:

```yaml
# Wrong — breaks YAML silently
description: Authentication: how it works

# Right — quoted
description: "Authentication: how it works"
```

Unquoted special characters cause silent failures in Git Sync — the page imports without a title or description with no error message. When generating frontmatter programmatically from migrated content, quote all string values by default.

## Complete example

```markdown
---
description: "Create reusable variables that can be referenced in pages and spaces"
icon: icons
cover: .gitbook/assets/hero.png
coverY: -40
vars:
  latest_version: v3.0.4
  support_email: help@example.com
layout:
  width: wide
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Your Page Title

Page content starts here...
```
