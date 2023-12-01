---
description: Add Tabs to a page
---

# Tabs

Using tabs can be a good way to structure your content.

### Example

Here is an example that lists instructions relevant to specific platforms:

{% tabs %}
{% tab title="Windows" %}
Here are the instructions for Windows
{% endtab %}

{% tab title="OSX" %}
Here are the instructions for macOS
{% endtab %}

{% tab title="Linux" %}
Here are the instructions for Linux
{% endtab %}
{% endtabs %}

### Representation in Markdown

```markdown
{% raw %}
{% tabs %}

{% tab title="Windows" %} Here are the instructions for Windows {% endtab %}

{% tab title="OSX" %} Here are the instructions for macOS {% endtab %}

{% tab title="Linux" %} Here are the instructions for Linux {% endtab %}

{% endtabs %}
{% endraw %}
```
