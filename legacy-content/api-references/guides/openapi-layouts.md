---
description: >-
  Choose between one page per tag and one page per operation for your API
  reference
---

# OpenAPI layouts

When you insert an **OpenAPI Reference**, GitBook can organize operations in two ways.

Choose the layout that matches how you want people to browse your API.

### Access this setting

To choose a layout:

1. In your section, click **Add new...** → **OpenAPI Reference**. You can also edit an existing OpenAPI Reference.
2. Choose your OpenAPI spec.
3. In **Page structure**, select **One page per tag** or **One page per operation**.

For the full setup flow, see [Insert API reference in your docs](../openapi/insert-api-reference-in-your-docs.md).

### Available layouts

GitBook supports two layouts:

* **One page per tag** creates one page for each tag. Each page lists all operations with that tag.
* **One page per operation** creates one page for each operation. GitBook groups those pages by tag in the table of contents.

### Example input

Both layouts start from the same OpenAPI data:

{% code title="openapi.yaml" %}
```yaml
paths:
  /users:
    get:
      tags:
        - users
      summary: List users
    post:
      tags:
        - users
      summary: Create user
```
{% endcode %}

### One page per tag

Use this layout when each tag represents a clear section of your API.

It works well when you want overview pages, fewer entries in the navigation, and related endpoints on the same page.

With this layout, both operations appear on the same generated page for the `users` tag.

### One page per operation

Use this layout when you want direct links to individual endpoints.

It works well for large APIs, or when each endpoint needs its own page in the navigation.

With this layout, GitBook creates one page for `GET /users` and one page for `POST /users`. Both pages appear under the `users` tag group.

### Quick recommendation

Choose **One page per tag** for smaller APIs, or when each tag is a clear section.

Choose **One page per operation** for larger APIs, or when you want a dedicated page for each endpoint.

### Control the generated navigation

In both layouts, GitBook uses your OpenAPI tags to organize the reference.

To control order, hierarchy, page titles, icons, and descriptions, see [Structuring your API reference](structuring-your-api-reference.md).
