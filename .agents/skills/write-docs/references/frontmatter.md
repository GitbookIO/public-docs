# Page frontmatter and variables

## Page frontmatter

GitBook supports YAML frontmatter at the top of markdown files to configure page-specific settings. Frontmatter must be placed at the very beginning of the file, before any content.

**Available frontmatter fields:**

```markdown
---
description: Page description used for SEO and page previews
icon: book-open
hidden: true
vars:
  page_variable: value
  another_var: another value
if: visitor.claims.unsigned.isPremium
layout:
  width: default
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

**Field descriptions:**

* **`description:`** - Page description text. Supports multiline with `>-` syntax:

  ```yaml
  description: >-
    This is a longer description
    that spans multiple lines
  ```
* **`icon:`** - Icon name from Font Awesome (e.g., `book-open`, `bolt`, `stars`, `icons`, `brackets-curly`)
* **`hidden: true`** - Hides the page from the table of contents in published documentation
* **`vars:`** - Page-level variables (key-value pairs) that can be referenced in expressions:

  ```yaml
  vars:
    version: v1.2.3
    api_key: example_key
  ```
* **`if:`** - Adaptive content visibility condition. Controls when the page is visible based on visitor attributes:

  ```yaml
  if: visitor.claims.unsigned.isPremium
  ```

  **Note:** While adaptive content conditions can be set in frontmatter, it's recommended to configure them through the GitBook UI for better maintainability and team visibility.
* **`layout:`** - Controls page layout and which elements are visible. This maps to the "Page Options" settings in the GitBook UI:

  * **`width:`** - Page content width
    * `default` - Standard content width
    * `wide` - Wider content area (automatically widens full-width blocks like tables and code)
  * **`title.visible:`** - Show/hide the page title (boolean: `true` or `false`)
  * **`description.visible:`** - Show/hide the page description (boolean: `true` or `false`)
  * **`tableOfContents.visible:`** - Show/hide the left sidebar table of contents (boolean: `true` or `false`)
  * **`outline.visible:`** - Show/hide the right sidebar page outline/headings (boolean: `true` or `false`)
  * **`pagination.visible:`** - Show/hide next/previous page navigation links (boolean: `true` or `false`)
  * **`metadata.visible:`** - Show/hide page metadata section (boolean: `true` or `false`)

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
* **`cover:`** - Path to a hero/banner image displayed at the top of the page. Typically a `.gitbook/assets/` path:

  ```yaml
  cover: .gitbook/assets/home-cover.png
  ```

  Requires `layout.cover.visible: true` to render. Accepts external URLs too.
* **`coverY:`** - Vertical crop offset for the cover image (integer; `0` = centered, positive moves the focal point down, negative up). Useful when the image is taller than the cover band:

  ```yaml
  coverY: -72
  ```
* **`layout.cover.visible:`** / **`layout.cover.size:`** - Control cover rendering. `size` is either `full` (full-bleed hero) or `hero` (smaller banner):

  ```yaml
  layout:
    cover:
      visible: true
      size: full
  ```

## YAML quoting in frontmatter

Always quote `description:` and any other string values that contain YAML-significant characters. Characters that require quoting: `:` (most common), `#`, `[`, `]`, `{`, `}`, `&`, `*`, `!`, `|`, `>`, `'`, `"`, `%`, `@`, `` ` `` (especially at the start of a value). The safe default is to quote any value containing punctuation:

```yaml
# Wrong — breaks YAML silently
description: Authentication: how it works

# Right — quoted
description: "Authentication: how it works"
```

Unquoted special characters cause silent failures in Git Sync — the page imports without a title or description with no error message. When generating frontmatter programmatically from migrated content, quote all string values by default.

## Complete frontmatter example

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

## Variables and Expressions

GitBook supports variables that can be dynamically displayed in your content using expressions. Variables can be defined at the space level or page level.

### Variable storage

**Space-level variables** are stored in `/.gitbook/vars.yaml` at the root of your documentation:

```yaml
# .gitbook/vars.yaml
food: apple
latest_version: v3.0.4
company_name: Acme Corp
```

**Page-level variables** are stored in the page's frontmatter under `vars:`:

```markdown
---
vars:
  page_food: orange
  page_version: v2.1.0
---
```

### Using variables with expressions

Expressions allow you to reference and display variable values dynamically in your content. Expressions use JavaScript syntax and are wrapped in `<code class="expression">` tags.

**Syntax:**

```markdown
<code class="expression">JavaScript expression here</code>
```

**Examples:**

```markdown
<!-- Simple expression -->
<code class="expression">1 + 1</code>

<!-- Reference a space-level variable -->
<code class="expression">space.vars.latest_version</code>

<!-- String concatenation with variable -->
<code class="expression">"My favorite food is " + space.vars.food</code>

<!-- Reference a page-level variable -->
<code class="expression">page.vars.page_food</code>

<!-- Conditional logic -->
<code class="expression">space.vars.latest_version === "v3.0.4" ? "Latest" : "Outdated"</code>
```

**Variable references:**

* `space.vars.variableName` - Access space-level variables defined in `/.gitbook/vars.yaml`
* `page.vars.variableName` - Access page-level variables defined in the page's frontmatter

**Important notes:**

* Expressions can contain any valid JavaScript code and are evaluated when the page is rendered
* When editing locally, you can create space variables by editing `/.gitbook/vars.yaml` and page variables by adding them to frontmatter
* The GitBook UI provides a visual editor for managing variables, but they are fully editable in markdown files
