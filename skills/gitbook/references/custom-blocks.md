# GitBook custom blocks

GitBook extends standard markdown with custom block syntax using tags like `{% tabs %}`, `{% hint %}`, etc. These blocks enable rich, interactive documentation features.

For the decision guide — which block to reach for in which content situation — see `block-ecosystem.md`.

## Contents

- When-to-use-which-block cheat sheet
- Tabs
- Stepper
- Hints
- Expandable (`<details>`)
- Columns
- Updates (changelog) + tags.yaml
- Cards (`<table data-view="cards">`)
- Embeds
- Files
- Buttons
- Icons (Font Awesome inline)
- Reusable content (`{% include %}`)
- OpenAPI specifications
- Common pitfalls

## When-to-use-which-block cheat sheet

| Need                                       | Use                         | Why                                                                   |
| ------------------------------------------ | --------------------------- | --------------------------------------------------------------------- |
| Sequential, ordered instructions           | `{% stepper %}`             | Guides users through multi-step processes with clear progression      |
| Alternative options (languages, platforms) | `{% tabs %}`                | Lets users choose their relevant option without cluttering the page   |
| Optional or detailed information           | `<details>` (Expandable)    | Keeps page scannable while providing depth for interested readers     |
| Important warnings or tips                 | `{% hint %}`                | Draws attention with colored styling (info, warning, danger, success) |
| Side-by-side comparisons                   | `{% columns %}`             | Shows related information in parallel (max 2 columns)                 |
| Timeline or changelog                      | `{% updates %}`             | Displays dated entries in reverse chronological order                 |
| Visual navigation cards                    | `<table data-view="cards">` | Creates clickable card grid for section navigation                    |
| Downloadable files                         | `{% file %}`                | Provides files with captions and descriptions                         |
| Call-to-action links                       | `<a class="button">`        | Highlights primary or secondary actions                               |
| Reusable content across pages              | `{% include %}`             | Maintains consistency for repeated content blocks                     |
| Dynamic content                            | `<code class="expression">` | Displays variable values that update automatically                    |

## Tabs

Present alternative content like different programming languages or platform-specific instructions.

**When to use:** Comparing alternatives (code in different languages, platform-specific commands, configuration options).

````markdown
{% tabs %}
{% tab title="JavaScript" %}
```javascript
const greeting = 'Hello World';
console.log(greeting);
```
{% endtab %}

{% tab title="Python" %}
```python
greeting = "Hello World"
print(greeting)
```
{% endtab %}
{% endtabs %}
````

## Stepper

Sequential, multi-step processes where order matters.

**When to use:** Tutorials, installation guides, how-to guides, onboarding checklists, any sequential process.

```markdown
{% stepper %}
{% step %}
## First step

Complete the initial setup by installing the required dependencies.
{% endstep %}

{% step %}
## Second step

Configure your environment variables in the `.env` file.
{% endstep %}

{% step %}
## Third step

Run the application with `npm start`.
{% endstep %}
{% endstepper %}
```

## Hints

Highlight important information without disrupting flow. Supported styles: `info`, `warning`, `danger`, `success`.

**When to use:** Supplementary information, call-outs, best practices, warnings, troubleshooting tips.

```markdown
{% hint style="info" %}
This is an informational hint with helpful context.
{% endhint %}

{% hint style="warning" %}
Be careful when running this command in production.
{% endhint %}

{% hint style="danger" %}
This action cannot be undone. Make sure you have backups.
{% endhint %}

{% hint style="success" %}
Your configuration has been saved successfully!
{% endhint %}
```

## Expandable (`<details>`)

Optional content that doesn't need to be visible by default.

**When to use:** Optional deep-dives, advanced explanations, lengthy logs, FAQ answers, content that would clutter the page.

````markdown
<details>
<summary>Advanced Configuration Options</summary>

Here you can find detailed information about advanced settings that most users won't need.

```yaml
advanced:
  option1: value1
  option2: value2
```
</details>
````

## Columns

Side-by-side content (2 columns maximum).

**When to use:** Side-by-side comparisons (pros vs cons), before/after examples, parallel instructions.

```markdown
{% columns %}
{% column %}
### Before

Old implementation that was inefficient.
{% endcolumn %}

{% column %}
### After

New optimized approach with better performance.
{% endcolumn %}
{% endcolumns %}
```

## Updates (changelog) + tags.yaml

Product updates, release notes, or changelogs.

**When to use:** Changelog pages, release notes, version updates, product announcements.

```markdown
{% updates format="full" %}
{% update date="2024-01-15" %}
# Version 2.0 Released

We've added new features including dark mode and improved search.
{% endupdate %}

{% update date="2024-01-01" %}
# Bug Fixes

Fixed several issues reported by the community.
{% endupdate %}
{% endupdates %}
```

### Tags parameter

Individual `{% update %}` entries can carry one or more tags via `tags=""` (comma-separated). Tags are rendered as filter chips in the published timeline and GitBook generates an RSS feed for the space automatically.

```markdown
{% updates format="full" %}
{% update date="2026-04-22" tags="api,beta" %}
## AI topic auto-classification (beta)

New endpoint for automatic topic tagging.
{% endupdate %}

{% update date="2026-03-10" tags="security" %}
## OAuth 2.0 Support

Added OAuth 2.0 authentication flow.
{% endupdate %}
{% endupdates %}
```

### Defining tags in `.gitbook/tags.yaml`

Tags must be declared before they can be used. Create `.gitbook/tags.yaml` at the root of the space. Tag slugs must exactly match the values used in `tags=""`:

```yaml
# .gitbook/tags.yaml
- tag: api
  label: API
  icon: code
- tag: security
  label: Security
  icon: shield-halved
- tag: beta
  label: Beta
  icon: flask
- tag: breaking
  label: Breaking Change
  icon: triangle-exclamation
```

Each entry: `tag` (slug, no spaces), `label` (display text), `icon` (Font Awesome name without `fa-` prefix).

## Cards (`<table data-view="cards">`)

Visual, clickable navigation elements. Cards are HTML tables with special attributes.

**When to use:** Dashboards, feature overviews, linking to related pages, showcasing multiple resources.

### Canonical pattern — full-row clickable card with hidden target column

The cleanest card-table uses `data-hidden` on the link column so the entire card tile becomes clickable, rather than showing a visible "Read more" link column which clutters the layout:

```markdown
<table data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Getting Started</strong></td>
      <td>Install and send your first event in five minutes.</td>
      <td><a href="getting-started/quickstart.md">quickstart</a></td>
    </tr>
    <tr>
      <td><strong>API Reference</strong></td>
      <td>Full endpoint and schema documentation.</td>
      <td><a href="api-reference/overview.md">overview</a></td>
    </tr>
  </tbody>
</table>
```

`data-hidden` makes the column invisible to readers. `data-card-target` marks it as the link target — the whole row becomes a link.

### Cards with icons

Prefer Font Awesome icons via `<i class="fa-...">` — they inherit theme colors and require no asset files. Use `<img>` only when you need a specific branded icon that Font Awesome doesn't cover.

**Font Awesome icon (preferred):**

```markdown
<table data-view="cards">
  <thead>
    <tr>
      <th width="48"></th>
      <th></th>
      <th></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><i class="fa-bolt"></i></td>
      <td><strong>Quickstart</strong></td>
      <td>Send your first event in five minutes.</td>
      <td><a href="getting-started/quickstart.md">quickstart</a></td>
    </tr>
  </tbody>
</table>
```

**Inline `<img>` for custom branded icons (fallback):**

```markdown
<table data-view="cards">
  <thead>
    <tr>
      <th width="48"></th>
      <th></th>
      <th></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img src=".gitbook/assets/quickstart.svg" alt="" data-size="line"/></td>
      <td><strong>Quickstart</strong></td>
      <td>Send your first event in five minutes.</td>
      <td><a href="getting-started/quickstart.md">quickstart</a></td>
    </tr>
  </tbody>
</table>
```

In both cases `<th width="48"></th>` keeps the icon column narrow. For `<img>`, `data-size="line"` constrains it to text-line height. Both `<i class="fa-...">` and `<img>` work anywhere else in markdown too — not just inside card-tables.

## Embeds

Include external content like videos, interactive demos, or social media.

**When to use:** Demonstration videos, interactive code sandboxes, tweets, external rich media.

```markdown
{% embed url="https://www.youtube.com/watch?v=dQw4w9WgXcQ" %}

{% embed url="https://codepen.io/username/pen/example" %}
```

## Files

Downloadable files with captions.

```markdown
{% file src="https://example.com/document.pdf" %}
Complete documentation in PDF format.
{% endfile %}
```

## Buttons

Clear call-to-action links. Supported styles: `primary` and `secondary`.

**When to use:** Download links, "Try it now" actions, external resource navigation.

```markdown
<a href="https://example.com/download" class="button primary">Download Now</a>

<a href="https://docs.example.com" class="button secondary">View Documentation</a>
```

### Buttons with icons

```markdown
<a href="https://github.com/user/repo" class="button primary" data-icon="github">View on GitHub</a>
```

Icons use Font Awesome names (without the `fa-` prefix).

## Icons (Font Awesome inline)

Inline icons from Font Awesome can enhance text readability.

**When to use:** Visual indicators, status icons, improving scannability.

```markdown
<i class="fa-check">check</i> Feature enabled
<i class="fa-warning">warning</i> Requires configuration
<i class="fa-info-circle">info</i> Learn more
```

## Reusable content (`{% include %}`)

Reusable content blocks let you sync content across multiple pages.

**When to use:** Call-to-actions, disclaimers, repeated instructions, any content that needs to stay consistent across pages.

```markdown
{% include "/reusable-content/rc12345" %}
```

Reusable content blocks are different from pages. They can be created through the GitBook UI (each gets a unique ID) or stored as files in `.gitbook/includes/<name>.md` and included by path.

## OpenAPI specifications

OpenAPI specifications enable interactive, testable API documentation in GitBook. **OpenAPI specs cannot be added directly to markdown files.**

### How to add OpenAPI specs

OpenAPI specifications must be uploaded through one of these methods:

1. **GitBook API** — Use the [OpenAPI endpoints](https://docs.gitbook.com/developers/gitbook-api/api-reference/openapi) to programmatically upload specs
2. **GitBook CLI** — Use the `gitbook openapi` command
3. **GitBook UI** — Upload specs through the web interface

### Inline endpoint reference in prose pages

Once uploaded, you can reference individual API methods in prose pages using the OpenAPI block:

```markdown
{% openapi src="https://api.example.com/openapi.json" path="/users" method="get" %}
[https://api.example.com/openapi.json](https://api.example.com/openapi.json)
{% endopenapi %}
```

### Auto-generating the full endpoint page tree (`builtin:openapi`)

For an API reference space, instead of hand-authoring one page per endpoint, use the `builtin:openapi` pattern in `SUMMARY.md` to auto-generate the entire page tree from a registered spec. The entry is a fenced YAML block as the bullet content:

```markdown
# Table of contents

* [Overview](README.md)

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

`spec: my-api-v1` is the slug of a spec registered with the GitBook organization (configured separately via the GitBook API or UI — the SUMMARY entry just references it). The generated operation pages are virtual and don't correspond to files in the repo; only the parent `README.md` files need to exist as real files. Pair each resource section with a brief prose README covering base URL, version policy, and what the resource is for.

**Important notes:**

- You cannot embed OpenAPI spec content directly in markdown files
- The `src` URL in inline `{% openapi %}` blocks must point to an already-uploaded specification
- The `builtin:openapi` page-tree pattern only works in `SUMMARY.md`, not inside regular pages

## Common pitfalls

- **Always close blocks properly** (`{% endtab %}`, `{% endhint %}`, etc.)
- **Match opening and closing tags exactly** — capitalization, spacing, attribute order
- **Test custom blocks in GitBook after editing locally** — some malformations only show at render time
- **Avoid plain markdown tables** for navigation — use card-tables instead
- **Avoid excessive nested lists** — keep hierarchy simple, use a stepper or expandable instead
