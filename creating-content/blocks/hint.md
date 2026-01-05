---
description: >-
  Add a hint to a page to draw your reader’s attention to specific pieces of
  important information.
---

# Hints

Hints, or callouts, are a great way to bring the reader’s attention to specific elements in your documentation, such as tips, warnings, and other important information.&#x20;

There are four different hint styles — you can change the style by clicking the colored icon, or by opening the block’s **Options menu** <picture><source srcset="../../.gitbook/assets/25_01_10_cards_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_cards_light.svg" alt="The Options menu icon in GitBook"></picture> and selecting the style you want.

Hint blocks support [inline content](../formatting/inline.md) and [formatting](../formatting/), as well some specific block types. To see which block types you can use in a hint, hit `/` on an empty line and check the [insert palette](./#inserting-a-new-content-block).

### Examples of hint blocks <a href="#example-of-a-hint" id="example-of-a-hint"></a>

{% hint style="info" %}
**Info hints** are great for showing general information, or providing tips and tricks.
{% endhint %}

{% hint style="success" %}
**Success hints** are good for showing positive actions or achievements.
{% endhint %}

{% hint style="warning" %}
**Warning hints** are good for showing important information or non-critical warnings.
{% endhint %}

{% hint style="danger" %}
**Danger hints** are good for highlighting destructive actions or raising attention to critical information.
{% endhint %}

{% hint style="info" %}
#### This is a H2 heading

This is a line

This is an inline <img src="../../.gitbook/assets/25_01_10_command_icon_light.svg" alt="The Apple computer command icon" data-size="line"> image

* This is a second <mark style="color:orange;background-color:purple;">line using an unordered list and color</mark>
{% endhint %}

To add a heading to your hint, you need to create a heading block as the the first block in the hint.

### Representation in Markdown

```markdown
{% hint style="info" %}
**Info hints** are great for showing general information, or providing tips and tricks.
{% endhint %}

{% hint style="success" %}
**Success hints** are good for showing positive actions or achievements.
{% endhint %}

{% hint style="warning" %}
**Warning hints** are good for showing important information or non-critical warnings.
{% endhint %}

{% hint style="danger" %}
**Danger hints** are good for highlighting destructive actions or raising attention to critical information.
{% endhint %}

{% hint style="info" %}

## This is a H2 heading

This is a line

This is an inline <img src="../../.gitbook/assets/25_01_10_command_icon_light.svg" alt="The Apple computer command icon" data-size="line"> image

- This is a second <mark style="color:orange;background-color:purple;">line using an unordered list and color</mark>
{% endhint %}
```
