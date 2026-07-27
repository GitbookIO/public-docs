---
description: "The Columns block: what it does and how to use it."
---

# Columns

Columns create side-by-side layouts. Add different block types inside each column, and adjust each side's width to fit your design — up to two columns per block.

### Example

{% columns %}
{% column width="50%" %}
**Create a seamless experience between your docs and product**

Integrate your documentation right into your product experience, or give users a personalized experience that gives them what they need faster.
{% endcolumn %}

{% column %}
Add an image, text, or any other block here.
{% endcolumn %}
{% endcolumns %}

### Representation in Markdown

```markdown
{% columns %}
{% column width="50%" %}
Content for the first column.
{% endcolumn %}

{% column %}
Content for the second column.
{% endcolumn %}
{% endcolumns %}
```
