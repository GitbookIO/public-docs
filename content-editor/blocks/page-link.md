---
description: Add a page link to a page.
---

# Page links

A page link is the best way to create relations between different pages.

### Example of page link block

The links below point to [blocks](./) and [inline content](../editing-content/inline.md):

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

{% content-ref url="../editing-content/inline.md" %}
[inline.md](../editing-content/inline.md)
{% endcontent-ref %}

## Representation in Markdown

```
{% raw %}
{% content-ref url="./" %} . {% endcontent-ref %}
{% endraw %}
```
