---
description: "The Expandable block: what it does and how to use it."
---

# Expandable

Expandable blocks condense what could be a lengthy paragraph — great for step-by-step guides and FAQs.

They're collapsed by default on your published site. To have one expanded by default, open its Options menu and choose **Expanded by default**.

### Example

<details open>

<summary>Step 1: Start using expandable blocks</summary>

To add an expandable block, hit `/` on an empty block, or click the `+` on the left of the editor, and select **Expandable**.

Optionally set it to **Expanded by default** in its Options menu — just like this block.

</details>

<details>

<summary>Step 2: Add content to your block</summary>

Once inserted, add content to it, including lists and code blocks.

</details>

### Representation in Markdown

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

### Limitations

Some block types can't be created inside an expandable block — start a new line inside one and press `/` to see the full list available.
