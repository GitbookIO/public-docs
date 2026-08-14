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

Use tags to group related content, convey release states, mark outdated content, or anything else that helps readers scan your documentation.

#### Tag a page

Open the page, then open the **Tags** menu  — accessible by hovering over the page title — and create or add tags. You can drag tags around to change the order in which they appear on the page.

1. Open the page.
2. Hover over the page title and open **Page options**.
3. Add one or more tags.

Drag tags to change the order in which they appear on the page.

#### Show or hide tags on a page

Tags display at the top of the page by default. To hide a page's tags while keeping the associated metadata:

* Open the **Tags** menu
* Turn off **Show tags on page** to keep tags as metadata only

1. Open **Page options**.
2. Turn off **Show tags on page**.

#### Display a tag in the table of contents

For each page, you can pick one tag to display in the table of contents. To choose which tag displays:

* Open the **Tags** menu
* Use the **Display in table of contents** dropdown to choose your tag
* You can also click into a tag and **Display**, **Remove** or **Replace in table of contents**.

1. Open **Page options**.
2. Under **Tags**, choose your tag from the **Display in table of contents** dropdown.

#### Tag an update block

Each update block can have its own tags.

1. Open the update block.
2. Click **Add tag** below the date.
3. Use the tag picker to add, remove, or reorder tags.

#### Manage tags in the Library

To view, create and manage tags for your space, open the **Library** from the [table of contents](../../../documentation/create-content/content-structure/page/#table-of-contents) and choose **Tags**. You can quickly access this by opening the **Tags** menu and selecting **Open Tag Library**. \
\
You can also view an individual tag in the library by selecting the tag and choosing **Show in Library**.

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
