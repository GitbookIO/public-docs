---
description: "The Page link block: what it does and how to use it."
---

# Page link

Page link blocks create relations between pages within your content. Unlike a hyperlink in text, a page link fills its own block, so it stands out on the page.

### Example

```markdown
{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}
```

### Representation in Markdown

```markdown
{% content-ref url="./" %} . {% endcontent-ref %}
```
