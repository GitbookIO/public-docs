---
description: Page link content block
---

# Page link

A page link is the best way to create relations between different pages.

### Example of page link block

The links below point to [blocks](./) and [inline content](../editor/inline.md):

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

{% content-ref url="../editor/inline.md" %}
[inline.md](../editor/inline.md)
{% endcontent-ref %}

## Representation in Markdown

```
{% raw %}
{% content-ref url="./" %} . {% endcontent-ref %}
{% endraw %}
```
