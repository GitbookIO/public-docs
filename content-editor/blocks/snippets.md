---
description: >-
  Add a snippet block to reference a specific snippet on your page, and
  highlight it as important
hidden: true
---

# Snippets

Snippet blocks are a great way to reference a snippet in your content. Snippet blocks help make the link to your snippet stand out on the page compared to [an inline link](../editing-content/inline.md#relative-links).

You can only use snippet blocks for internal pages. If you add a snippet block to a page in a published space, the public documentation will show the block as a broken link.

{% hint style="warning" %}
**Note:** If you use a snippet block, but then [convert your snippet into a page](../../snippets/snippets-beta.md#convert-a-snippet-to-a-page) in your documentation, your snippet block will still link back to the original snippet, which will be archived.
{% endhint %}

### Representation in Markdown

```
{% raw %}
{% content-ref url="./" %} . {% endcontent-ref %}
{% endraw %}
```
