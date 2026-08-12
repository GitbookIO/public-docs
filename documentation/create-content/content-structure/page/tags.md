---
description: "Tags are reusable labels you can add to pages and update blocks —\_this page tells you how to create, add and manage tags"
tags:
  - news
  - beta
---

# Tags

Use tags to group related content, convey release states, mark outdated content, or anything else that helps readers scan your documentation.

#### Tag a page

1. Open the page.
2. Hover over the page title and open **Page options**.
3. Add one or more tags.

Drag tags to change the order in which they appear on the page.

#### Show or hide tags on a page

Tags display at the top of the page by default. To hide a page's tags while keeping the associated metadata:

1. Open **Page options**.
2. Turn off **Show tags on page**.

#### Display a tag in the table of contents

For each page, you can pick one tag to display in the table of contents. To choose which tag displays:

1. Open **Page options**.
2. Under **Tags**, choose your tag from the **Display in table of contents** dropdown.

#### Tag an update block

Each update block can have its own tags.

1. Open the update block.
2. Click **Add tag** below the date.
3. Use the tag picker to add, remove, or reorder tags.

#### Manage tags in the Library

To view, create, and manage tags for your section:

1. Open the **Library** from the table of contents.
2. Click **Tags**.

Each tag has:

* A label — what readers see
* A slug — a stable identifier
* An optional icon or emoji

#### Tags in Markdown

If you use Git Sync, tags appear in the page frontmatter:

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
