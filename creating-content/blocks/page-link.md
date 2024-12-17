---
description: Add a page link block to show relations between pages in your space.
---

# Page links

Page link blocks are the best way create relations between different pages within your content. Page links stand out on the page as they fill their own block — compared to a hyperlink added to some text.&#x20;

### Example of page link block

The links below point to [blocks](./) and [inline content](../formatting/inline.md):

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

{% content-ref url="../formatting/inline.md" %}
[inline.md](../formatting/inline.md)
{% endcontent-ref %}

## Representation in Markdown

```markdown
{% raw %}
{% content-ref url="./" %} . {% endcontent-ref %}
{% endraw %}
```
