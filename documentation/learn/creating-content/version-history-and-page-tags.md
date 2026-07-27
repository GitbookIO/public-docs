---
description: Track page history and organize pages with tags.
---

# Version history and page tags

## Version history

Monitor every change made to your content using the **Version history** side panel.

The panel lists all the actions that changed a section's content: live edits, merged change requests, and Git Sync operations.

**View historical versions.** Click **Version history** in the section header, or open the Actions menu next to the section or change request title. Click any item to see how your content looked at that point — similar to viewing a change request.

**Show changes.** While viewing an old version, toggle **Show changes** at the bottom of the panel to highlight what's different from the current content — changed blocks get an icon on the left, similar to diff view in a change request.

**View historical published versions.** To preview what an old version looked like to actual visitors:

{% stepper %}
{% step %}
#### Select the revision

From the version history panel, select the revision.
{% endstep %}

{% step %}
#### Copy its ID

Copy the ID at the end of the URL.
{% endstep %}

{% step %}
#### Append it to your published URL

Add it to your published docs URL as `/~/revisions/<id>`.
{% endstep %}
{% endstepper %}

**Roll back to a previous version.** Useful after an accidental breaking change or deletion — hover the version in the side panel, click the Actions button, and click **Rollback**.

## Page tags

Use tags to group related content, convey release states, mark outdated content, or help readers scan your documentation.

**Tag a page** — open the page, hover the page title, open **Page options**, and add one or more tags. Drag tags to reorder them.

**Show or hide tags** — tags display at the top of the page by default. To hide them while keeping the metadata, open **Page options** and turn off **Show tags on page**.

**Display a tag in the table of contents** — in **Page options**, under **Tags**, choose a tag from the **Display in table of contents** dropdown.

**Tag an update block** — open the [update block](blocks/updates.md), click **Add tag** below the date, and use the tag picker to add, remove, or reorder tags.

**Manage tags in the Library** — open **Library** from the table of contents and click **Tags**. Each tag has a label (what readers see), a slug (a stable identifier), and an optional icon or emoji.

**Tags in Markdown.** With Git Sync, tags appear in page frontmatter:

```yaml
---
description: "Tags are reusable labels you can add to pages and update blocks"
tags:
  - news
  - experiment
  - tag: beta
    primary: true
  - pro
---
```

Use a plain string for a standard tag. Set `primary: true` on one tag to make it the page's primary tag — the one GitBook can show in the table of contents.
