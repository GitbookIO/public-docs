---
description: >-
  Add a block with multiple tabs to a page, so you can display large blocks of
  related information without creating a long, hard-to-navigate page.
---

# Tabs

A tab block is a single block with the option to add multiple tabs.&#x20;

Each tab is like a mini page — it can contain multiple other blocks, of any type. So you can add code blocks, images, integration blocks and more to individual tabs in the same tab block.

They’re great for adding similar or related information without making your page really long — such as code snippets in multiple languages, or instructions for completing the same tasks on different operating systems.

### Add or delete tabs

To add a new tab to a tab block, hover over the edge of a tab and click the `+` button that appears. To delete a tab, open the tab’s **Options menu** <img src="../../.gitbook/assets/Options menu.png" alt="" data-size="line"> then select **Delete**.

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
