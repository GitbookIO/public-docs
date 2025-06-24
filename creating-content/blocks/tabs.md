---
description: >-
  Add tabs so you can display large blocks of related information without
  creating a long, hard-to-navigate page
---

# Tabs

A tab block is a single block with the option to add multiple tabs.

Each tab can contain multiple other blocks, of any type. So you can add code blocks, images, integration blocks and more to individual tabs in the same tab block.

### Add or delete tabs

To add a new tab to a tab block, hover over the edge of a tab and click the `+` button that appears. To delete a tab, open the tab’s **Options menu** <picture><source srcset="../../.gitbook/assets/options_menu_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/options_menu_icon_light.svg" alt="The Options menu icon in GitBook"></picture> then select **Delete**.

### Example

Here is an example that lists instructions relevant to specific platforms:

{% tabs %}
{% tab title="Windows" %}
Here are the instructions for Windows
{% endtab %}

{% tab title="macOS" %}
Here are the instructions for macOS
{% endtab %}

{% tab title="Linux" %}
Here are the instructions for Linux
{% endtab %}
{% endtabs %}

### Representation in Markdown

```markdown
{% tabs %}

{% tab title="Windows" %} Here are the instructions for Windows {% endtab %}

{% tab title="OSX" %} Here are the instructions for macOS {% endtab %}

{% tab title="Linux" %} Here are the instructions for Linux {% endtab %}

{% endtabs %}
```
