---
description: "Tags are reusable labels you can add to pages and update blocks —\_this page tells you how to create, add and manage tags"
tags:
  - news
  - experiment
  - tag: beta
    primary: true
  - pro
---

# Tags

Use tags to group related content, convey release states, mark outdated content, or help people and agents find relevant pages.

### Organize tags with a hierarchy

Tags can form a hierarchy of categories, subcategories, and tags. Categories organize the tag library. You apply tags to pages and update blocks.

For example, use this taxonomy for a product with several features:

```
Product
└── Sub-product
    └── Feature
```

This structure keeps large tag libraries scannable. It also lets you browse to a focused set of tags in the tag picker.

### Manage tags in the Library

To view, create, and manage tags for your space, open **Library → Tags**. You can also open the **Tags** menu and click **Open Tag Library**.

In the Library, create categories before their children. Select a category to browse its subcategories and tags. When you create or edit an item, select its parent to place it in the hierarchy.

Each tag has:

* A label, which readers see.
* A slug, which is its stable identifier.
* An optional icon or emoji.

Categories organize tags only. You cannot apply a category to a page or update block.

### Tag a page

To add tags to a page:

1. Open the page.
2. Hover over the page title and click **Page options**.
3. Under **Tags**, browse or search the hierarchy, then select one or more tags.

The picker shows the category path for nested tags. Use it to distinguish tags with similar labels. Drag applied tags to change their display order.

#### Show or hide tags on a page

Tags display at the top of a page by default. To keep tags as metadata only:

1. Open **Page options**.
2. Turn off **Show tags on page**.

#### Display a tag in the table of contents

You can display one page tag in the table of contents:

1. Open **Page options**.
2. Under **Tags**, select a tag in **Display in table of contents**.

### Tag an update block

Each update block can have its own tags:

1. Open the update block.
2. Click **Add tag** below the date.
3. Browse or search the tag hierarchy, then select tags.

### Manage tags with Git Sync

Git Sync stores the tag library in `.gitbook/tags.yaml`. Define categories with `kind: category`. Set `parent` to the parent category slug.

```yaml
product:
  label: Product
  color: blue
  kind: category

sub-product:
  label: Sub-product
  color: blue
  kind: category
  parent: product

feature:
  label: Feature
  color: green
  parent: sub-product
```

Categories can contain nested categories. A standard tag can have one category parent. The `parent` value is a slug, not a label.

Git Sync stores page tags in the page frontmatter:

```yaml
---
description: "Tags are reusable labels you can add to pages and update blocks — this page tells you how to create, add, and manage tags"
tags:
  - news
  - experiment
  - tag: beta
    primary: true
  - pro
---
```

Use a string for a standard tag. Use `primary: true` on one tag to make it the page's primary tag — GitBook can show that tag in the table of contents.

### Use tags through the API and MCP

The [GitBook API reference](https://gitbook.com/docs/developers/gitbook-api/api-reference) exposes tag management, page counts, and page discovery. GitBook MCP exposes the same workspace capabilities to connected agents.

Use the tag list operation to retrieve the hierarchy. Each returned tag includes its `parent` relationship. Use the page-count operation to identify tags that have attached pages before you search.

To discover pages for a tag, use the tag pages operation with the tag slug. The response returns the matching pages. For example, an agent can list the `feature` tag, read its page count, then retrieve the pages that use `feature`.

```http
GET /spaces/{spaceId}/content/tags
GET /spaces/{spaceId}/content/tags/{tagSlug}/page-count
GET /spaces/{spaceId}/content/tags/{tagSlug}/pages
```

```json
{
  "count": 12
}
```

Use a personal access token for API requests. In GitBook MCP, ask the agent to list tags, get the page count for a tag, or list pages for that tag. See [gitbook-mcp.md](../../../docs-as-code/gitbook-mcp.md "mention") for connection options.

{% hint style="info" %}
GitBook MCP manages tags in your workspace. A published docs MCP server only reads published content. It can search and retrieve pages, but it cannot manage your tag library.
{% endhint %}

### Choose the right workflow

The editor, API, GitBook MCP, and Git Sync support the same tag hierarchy and page-tag assignments.

Use the editor to browse and manage a visual taxonomy. Use the API or GitBook MCP for automated management and page discovery. Use `.gitbook/tags.yaml` when your repository is the source of truth. Published docs MCP supports search and retrieval, not tag-library administration.
