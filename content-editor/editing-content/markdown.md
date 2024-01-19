---
description: >-
  GitBook supports Markdown directly in the editor, so you can quickly and
  easily create content using common syntax.
---

# Markdown

GitBook’s editor allows you to create formatted content using Markdown.

Markdown is a popular markup syntax that’s widely known for its simplicity. GitBook supports it as a keyboard-friendly way to write rich and structured text.

{% hint style="info" %}
You can learn more about Markdown itself by visiting [Common Mark](https://commonmark.org/help/).
{% endhint %}

### Text formatting <a href="#text-formatting" id="text-formatting"></a>

GitBook supports all the classic inline Markdown formatting:

| Formatting    | Markdown version  | Result            |
| ------------- | ----------------- | ----------------- |
| Bold          | `**bold**`        | **text**          |
| Italic        | `_italic_`        | _italic_          |
| Strikethrough | `~strikethrough~` | ~~strikethrough~~ |

### Titles

* Heading 1: `# A first-level title`
* Heading 2: `## A second-level title`
* Heading 3: `### A third-level title`

### Code blocks

` ```⏎ ` creates a new code block.

` ```py⏎ ` creates a new code block with Python syntax highlighting.

{% hint style="info" %}
We use [Prism](https://github.com/PrismJS/prism) for syntax highlighting. You can use [Test Drive Prism](https://prismjs.com/test.html#language=markup) to check which languages Prism supports. If you notice a mismatch between GitBook and Prism, there’s a chance we’re a version or two behind. We’ll catch up soon!
{% endhint %}

### Lists

GitBook automatically detects and creates ordered and unordered lists as you type.

* Begin a line with `-` or `*` to start an unordered bullet list.
* Begin a line with `1.` to start a numbered list.&#x20;
* Begin a line with `- [ ]` to start a task list.

{% hint style="info" %}
When writing any kind of list, hit `Tab` to add a indent, and `Shift+Tab` to outdent.
{% endhint %}

### Quotes

Begin a line with `>` to create a block quote. If you select an entire paragraph from start to end, typing `>` will wrap the content in a block quote.

> This is a block quote.

### Dividers

Type `---` then hit `Enter` to create a divider on your page.&#x20;

***

This is an example of a divider.
