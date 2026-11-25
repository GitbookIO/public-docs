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

Tags can form a hierarchy in two ways:

* **Categories** group tags in the tag library. A category can contain tags and other categories, up to three levels deep. You cannot apply a category to a page or update block.
* **Nested tags** sit one level under a parent tag. You can apply the parent tag, the nested tag, or both.

For example, use this taxonomy for a product with several areas:

```
Product area             (category)
├── Editor               (tag)
│   ├── Blocks           (nested tag)
│   └── Change requests  (nested tag)
└── Integrations         (tag)
```

This structure keeps large tag libraries scannable. Tags without a parent appear under **Uncategorized** in the tag library.

### Manage tags in the Library

To view, create, and manage tags for your space, open **Library → Tags**. You can also click **Tags** above the page title and select **Open Tag Library**.

The Library lists categories and tags as a tree. Each category shows the number of tags it contains. Use the arrow next to a category or parent tag to expand or collapse it.

#### Create a category or tag

1. In **Library → Tags**, click **+**.
2. Select **New category** or **New tag**.
3. Enter a label. GitBook generates the slug from the label. Edit the slug now if you need a different one — you cannot change it after you create the item.
4. In **Parent**, select where to place the item. **Root** keeps it at the top level. A category can sit under another category. A tag can sit under a category or under another tag.
5. Optionally, choose an icon or emoji and a color.
6. Click **Create**.

Create a category or parent tag before its children. To add a tag directly under an existing tag, open the tag's **Actions** menu and select **New child tag**.

Each tag has:

* A label, which readers see.
* A slug, which is its stable identifier.
* An optional icon or emoji.
* A color.

#### Move, reorder, or delete a tag

Hover over a tag in the Library and open its **Actions** menu:

* **Edit tag** changes the label, icon, color, or parent.
* **Move up** and **Move down** reorder the tag among its siblings.
* **Move to…** moves the tag to **Uncategorized**, to a category, or under another tag.
* **Remove from category** takes the tag out of its category.
* **Delete tag** removes the tag from the Library and from every page and update block that uses it. Its nested tags move up to the deleted tag's parent.

You can delete a category only when it is empty. Move or delete its tags and subcategories first.

### Tag a page

To add tags to a page:

1. Open the page.
2. Hover over the page title and click **Page options**.
3. In the **Layout** tab, under **Tags**, click **+**, then search for or select one or more tags.

You can also click **Tags** next to **Page options** to open the tag picker directly. The picker lists tags and nested tags. It does not list categories. Drag applied tags to change their display order.

#### Show or hide tags on a page

Tags display at the top of a page by default. To keep tags as metadata only:

1. Open **Page options**.
2. In the **Layout** tab, turn off **Show tags on page**.

#### Display a tag in the table of contents

You can display one page tag in the table of contents:

1. Open **Page options**.
2. In the **Layout** tab, under **Tags**, select a tag in **Display in table of contents**.

### Tag an update block

Each update block can have its own tags:

1. Open the update block.
2. Click **Add tag** below the date.
3. Search for or select tags.

### Manage tags with Git Sync

Git Sync stores the tag library in `.gitbook/tags.yaml`. Define categories with `kind: category`. Set `parent` to the slug of the parent category or parent tag.

```yaml
product-area:
  label: Product area
  color: blue
  kind: category

editor:
  label: Editor
  color: blue
  parent: product-area

blocks:
  label: Blocks
  color: blue
  parent: editor

integrations:
  label: Integrations
  color: green
  parent: product-area
```

Categories can contain nested categories. A tag can have one parent, which is either a category or another tag. The `parent` value is a slug, not a label.

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

The editor, Git Sync, the [GitBook API](https://gitbook.com/docs/developers/gitbook-api/api-reference), and GitBook MCP all read and write the same tag hierarchy.

#### List tags and find pages

```http
GET /spaces/{spaceId}/content/tags
GET /spaces/{spaceId}/content/pages?tag={tagSlug}
```

The tag list returns every tag and category in the space's published content, in hierarchy order. Each item includes its parent and a `pageCount`. The count covers pages tagged with the item or with any tag nested under it, so a category's count is the total for the tags it contains.

```json
{
  "tags": [
    {
      "slug": "beta",
      "label": "Beta",
      "icon": "flask-round-potion",
      "color": "default",
      "pageCount": 6
    }
  ]
}
```

To find the pages for a tag, pass its slug in the `tag` parameter of the pages endpoint. You can also pass a category slug. Repeat the parameter to match pages with any of the given tags. The response is the space's page hierarchy, narrowed to the matching pages and the pages above them.

#### Create, update, or delete tags

Tag changes go through a change request, like other content changes. Send `insert_tags`, `update_tag`, or `delete_tag` changes to the change request's content endpoint:

```http
POST /spaces/{spaceId}/change-requests/{changeRequestId}/content
```

```json
{
  "changes": [
    {
      "operation": "insert_tags",
      "tags": [
        { "label": "Product area", "slug": "product-area", "kind": "category" },
        { "label": "Editor", "slug": "editor", "parent": "product-area" },
        { "label": "Blocks", "slug": "blocks", "parent": "editor" }
      ]
    }
  ]
}
```

Tags in one request apply in order, so list each parent before its children.

Use a personal access token for API requests. In GitBook MCP, ask the agent to list tags, find the pages for a tag, or update the tag library in a change request. See [gitbook-mcp.md](../../../docs-as-code/gitbook-mcp.md "mention") for connection options.

{% hint style="info" %}
GitBook MCP manages tags in your workspace. A published docs MCP server only reads published content. It can search and retrieve pages, but it cannot manage your tag library.
{% endhint %}
