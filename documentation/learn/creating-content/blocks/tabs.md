---
description: "The Tabs block: what it does and how to use it."
---

# Tabs

A tabs block holds multiple tabs, each able to contain any other block type — code blocks, images, integration blocks, and more.

### Add or delete tabs

Hover a tab's edge and click the `+` that appears to add one. To delete a tab, open its Options menu and select **Delete**.

### Tab icons

Open a tab's Options menu and select **Set icon** (or **Change icon** / **Remove icon**) to manage its icon via the icon picker.

### Example

{% tabs %}
{% tab title="Windows" icon="windows" %}
Here are the instructions for Windows
{% endtab %}

{% tab title="macOS" icon="apple" %}
Here are the instructions for macOS
{% endtab %}

{% tab title="Linux" icon="linux" %}
Here are the instructions for Linux
{% endtab %}
{% endtabs %}

### Representation in Markdown

```markdown
{% tabs %}

{% tab title="Windows" icon="windows" %} Here are the instructions for Windows {% endtab %}

{% tab title="macOS" icon="apple" %} Here are the instructions for macOS {% endtab %}

{% tab title="Linux" icon="linux" %} Here are the instructions for Linux {% endtab %}

{% endtabs %}
```
