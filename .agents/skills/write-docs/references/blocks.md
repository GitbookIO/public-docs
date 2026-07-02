# GitBook custom blocks

GitBook extends standard markdown with custom block syntax using tags like `{% tabs %}`, `{% hint %}`, etc. These blocks enable rich, interactive documentation features.

## Tabs

Use tabs to present alternative content like different programming languages or platform-specific instructions.

**When to use:** Comparing alternatives (code in different languages, platform-specific commands, configuration options).

**Syntax:**

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

Use steppers for sequential, multi-step processes where order matters.

**When to use:** Tutorials, installation guides, how-to guides, onboarding checklists, any sequential process.

**Syntax:**

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

Use hints to highlight important information without disrupting flow. Supported styles: `info`, `warning`, `danger`, `success`.

**When to use:** Supplementary information, call-outs, best practices, warnings, troubleshooting tips.

**Syntax:**

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

## Expandable

Use expandable sections for optional content that doesn't need to be visible by default.

**When to use:** Optional deep-dives, advanced explanations, lengthy logs, FAQ answers, content that would clutter the page.

**Syntax:**

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

Use columns to present content side-by-side (2 columns maximum).

**When to use:** Side-by-side comparisons (pros vs cons), before/after examples, parallel instructions.

**Syntax:**

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

## Updates

Use updates blocks for product updates, release notes, or changelogs.

**When to use:** Changelog pages, release notes, version updates, product announcements.

**Syntax:**

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

**Tags parameter:**

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

**Defining tags in `.gitbook/tags.yaml`:**

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

## Cards

Use cards to create visual, clickable navigation elements. Cards are HTML tables with special attributes.

**When to use:** Dashboards, feature overviews, linking to related pages, showcasing multiple resources.

**Canonical pattern — full-row clickable card with hidden target column:**

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

**Cards with icons:**

Prefer Font Awesome icons via `<i class="fa-...">` — they inherit theme colors and require no asset files. Use `<img>` only when you need a specific branded icon that Font Awesome doesn't cover.

*Font Awesome icon (preferred):*

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

*Inline `<img>` for custom branded icons (fallback):*

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

In both cases `<th width="48"></th>` keeps the icon column narrow. For `<img>`, `data-size="line"` constrains it to text-line height.

## Embeds

Use embeds to include external content like videos, interactive demos, or social media.

**When to use:** Demonstration videos, interactive code sandboxes, tweets, external rich media.

**Syntax:**

```markdown
{% embed url="https://www.youtube.com/watch?v=dQw4w9WgXcQ" %}

{% embed url="https://codepen.io/username/pen/example" %}
```

## Files

Use file blocks to provide downloadable files with captions.

**Syntax:**

```markdown
{% file src="https://example.com/document.pdf" %}
Complete documentation in PDF format.
{% endfile %}
```

## Buttons

Use buttons for clear call-to-action links. Supported styles: `primary` and `secondary`.

**When to use:** Download links, "Try it now" actions, external resource navigation.

**Syntax:**

```markdown
<a href="https://example.com/download" class="button primary">Download Now</a>

<a href="https://docs.example.com" class="button secondary">View Documentation</a>
```

**Buttons with icons:**

```markdown
<a href="https://github.com/user/repo" class="button primary" data-icon="github">View on GitHub</a>
```

Icons use Font Awesome names (without the `fa-` prefix).

## Icons

Inline icons from Font Awesome can enhance text readability.

**When to use:** Visual indicators, status icons, improving scannability.

**Syntax:**

```markdown
<i class="fa-check">check</i> Feature enabled
<i class="fa-warning">warning</i> Requires configuration
<i class="fa-info-circle">info</i> Learn more
```

## Reusable Content

Reusable content blocks let you sync content across multiple pages.

**When to use:** Call-to-actions, disclaimers, repeated instructions, any content that needs to stay consistent across pages.

**Syntax:**

```markdown
{% include "/reusable-content/rc12345" %}
```

Note: Reusable content blocks are different from pages. They're created through the GitBook UI and given unique IDs.

## OpenAPI Specifications

OpenAPI specifications enable interactive, testable API documentation in GitBook. However, OpenAPI specs cannot be added directly to markdown files.

**How to add OpenAPI specs:**

OpenAPI specifications must be uploaded through one of these methods:

1. **GitBook API** - Use the [OpenAPI endpoints](https://docs.gitbook.com/developers/gitbook-api/api-reference/openapi) to programmatically upload specs
2. **GitBook CLI** - Use the `gitbook openapi` command
3. **GitBook UI** - Upload specs through the web interface

**Once uploaded**, you can reference individual API methods in prose pages using the OpenAPI block:

```markdown
{% openapi src="https://api.example.com/openapi.json" path="/users" method="get" %}
[https://api.example.com/openapi.json](https://api.example.com/openapi.json)
{% endopenapi %}
```

**Auto-generating the full endpoint page tree (`builtin:openapi`):**

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

* You cannot embed OpenAPI spec content directly in markdown files
* The `src` URL in inline `{% openapi %}` blocks must point to an already-uploaded specification
* The `builtin:openapi` page-tree pattern only works in `SUMMARY.md`, not inside regular pages

## Nested markdown in custom blocks

Markdown formatting works inside custom block tags. Maintain standard markdown syntax within custom blocks:

````markdown
{% tabs %}
{% tab title="Example" %}
This tab contains markdown:

- Bullet points work
  - Nested bullets too
- **Bold text** and *italic text*
- `inline code`

```javascript
// Code blocks work too
const example = true;
```
{% endtab %}
{% endtabs %}
````

## Complete page example

````
```markdown
# API Authentication Guide

Learn how to authenticate with our API using API keys or OAuth 2.0.

{% hint style="info" %}
All API requests require authentication. Choose the method that best fits your use case.
{% endhint %}

## Authentication Methods

{% tabs %}
{% tab title="API Key" %}
The simplest authentication method. Include your API key in the request header:
```bash
curl -H "X-API-Key: your-api-key" https://api.example.com/v1/users
```

{% hint style="warning" %}
Never commit API keys to version control. Use environment variables instead.
{% endhint %}
{% endtab %}

{% tab title="OAuth 2.0" %}
More secure for user-facing applications:

{% stepper %}
{% step %}
## Register your application
Get your client ID and secret from the developer dashboard.
{% endstep %}

{% step %}
## Request authorization
Redirect users to our OAuth endpoint.
{% endstep %}

{% step %}
## Exchange code for token
Use the authorization code to get an access token.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

## Rate Limits
{% columns %}
{% column %}
### Free Tier
1,000 requests/hour
10,000 requests/day
{% endcolumn %}

{% column %}
### Pro Tier
10,000 requests/hour
100,000 requests/day
{% endcolumn %}
{% endcolumns %}

<details>
<summary>Need higher limits?</summary>

Contact our sales team to discuss enterprise plans with custom rate limits and SLAs.
</details>

<a href="https://example.com/signup" class="button primary" data-icon="rocket">Get Started</a>
```
````
