---
description: "The Hint block: what it does and how to use it."
---

# Hint

Hints (callouts) draw a reader's attention to specific elements — tips, warnings, or other important information.

There are four styles — change one by opening the block's Options menu. Each style has a default icon, which you can customize by clicking it and choosing another from [Font Awesome](../format-your-content.md#icons).

Hint blocks support [inline content](../format-your-content.md) and formatting, plus some specific block types — hit `/` on an empty line inside one to see which.

### Examples

{% hint style="info" %}
**Info hints** are great for general information, tips, and tricks.
{% endhint %}

{% hint style="success" %}
**Success hints** are good for positive actions or achievements.
{% endhint %}

{% hint style="warning" %}
**Warning hints** are good for important information or non-critical warnings.
{% endhint %}

{% hint style="danger" %}
**Danger hints** are good for destructive actions or critical information.
{% endhint %}

To add a heading to a hint, make a heading block the first block inside it.

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
```
