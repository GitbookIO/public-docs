---
description: >-
  Add an expandable block to a page to keep your pages shorter, hide longer
  content, or create FAQs
---

# Expandable

Expandable blocks are helpful in condensing what could otherwise be a lengthy paragraph. They are also great in step-by-step guides and FAQs.

By default, expandable blocks will be collapsed on your published docs site. If you want an expandable block to be expanded by default, open the block’s **Options menu** <picture><source srcset="../../.gitbook/assets/25_01_10_options_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_options_light.svg" alt=""></picture> and choose **Expanded by default**.

### Example

<details open>

<summary>Step 1: Start using expandable blocks</summary>

To add an expandable block hit `/` on an empty block, or click the `+` on the left of the editor, and select **Expandable**.&#x20;

Optionally, you can set expanded blocks to be **Expanded by default** in the block’s **Options menu** <picture><source srcset="../../.gitbook/assets/25_01_10_options_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_options_light.svg" alt=""></picture> — just like this block.

</details>

<details>

<summary>Step 2: Add content to your block</summary>

Once you’ve inserted an expandable block, you can add content to it — including lists and code blocks.

</details>

## Representation in Markdown

{% code overflow="wrap" %}
```markdown
# Expandable blocks

<details open>

<summary>Add your expandable title here</summary>

Add your expandable body text here. This expandable is expanded by default.

</details>

<details>

<summary>Add your expandable title here</summary>

Add your expandable body text here. This expandable is collapsed by default.

</details>
```
{% endcode %}

### Limitations

There are some limitations on which blocks you can create inside of an expandable block. You can check the full list by starting a new line in an expandable block and pressing `/` to bring up the insert palette.
