---
description: "Add one or more updates to a page —\_perfect for adding a changelog to your site"
---

# Updates

An updates block lets you share new releases on your site in a format that matches established best practices for changelog updates.

You can add a date to your update block, then format the content inside the block using other blocks as you would expect. To change the date or update the date format, click the date in your block. You can choose between the full date, a shortened date, or a date using only numbers (e.g. 12/25/2025).

Once you’ve added an update block to your page, you can hover your cursor above or below the block to see the option to add another in sequence.&#x20;

### Example

{% updates format="full" %}
{% update date="2025-12-25" %}
## A brand new update

This block is perfect for telling users all about a brand new update to your product. You can easily add other blocks within this update block, including images, code, lists and much more.
{% endupdate %}
{% endupdates %}

### Representation in Markdown

{% code overflow="wrap" %}
```markdown
{% update date="2025-12-25 %}
## A brand new update

This block is perfect for telling users all about a brand new update to your product. You can easily add other blocks within this update block, including images, code, lists and much more.
{% endupdate %}
```
{% endcode %}
