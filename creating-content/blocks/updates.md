---
description: "Add one or more updates to a page —\_perfect for adding a changelog to your site"
---

# Updates

An updates block lets you add a changelog to any page. Each update has a date, optional tags, and supports any block content inside it — text, images, code blocks, lists, and more.

### Adding updates

Insert an updates block on any page. Once it's on the page, hover above or below an existing update to add another in sequence.

To change the date format, click the date in the block. You can display the full date, a shortened version, or numbers only (for example, 12/25/2025).

### Tags

Each update can have its own tags. Use the tag picker below the date to add, remove, or reorder them.

### RSS feed

Any page with an updates block automatically gets an RSS feed. Your readers can open the feed from the button at the top of the page, copy the URL, and add it to their preferred reader. New updates you publish are pushed to that reader automatically.

### Example

{% updates format="full" %}
{% update date="2025-12-25" tags="beta" %}
## A brand new update

Use this block to tell users about a new update. Add any additional blocks you need inside it — images, code, lists, and more.
{% endupdate %}
{% endupdates %}

{% code overflow="wrap" %}
```markdown
{% updates format="full" %}
{% update date="2025-12-25" tags="beta" %}
## A brand new update

This block is perfect for telling users all about a brand new update to your product. You can easily add other blocks within this update block, including images, code, lists and much more.
{% endupdate %}
{% endupdates %}
```
{% endcode %}
