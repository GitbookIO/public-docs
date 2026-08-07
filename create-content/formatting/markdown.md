---
description: >-
  Write Markdown directly in the editor to easily create content using common
  syntax
---

# Markdown

<figure><img src="../../.gitbook/assets/25_12_10_markdown@2x.png" alt="An image containing the markdown logo"><figcaption><p>Write Markdown in GitBook.</p></figcaption></figure>

GitBook’s editor allows you to create formatted content using Markdown.

Markdown is a popular markup syntax that’s widely known for its simplicity. GitBook supports it as a keyboard-friendly way to write rich and structured text.

{% hint style="info" %}
You can learn more about Markdown itself by visiting [Common Mark](https://commonmark.org/help/).
{% endhint %}

### Text formatting <a href="#text-formatting" id="text-formatting"></a>

GitBook supports all the classic inline Markdown formatting:

| Formatting    | Markdown version  | Result            |
| ------------- | ----------------- | ----------------- |
| Bold          | `**bold**`        | **bold**          |
| Italic        | `_italic_`        | _italic_          |
| Strikethrough | `~strikethrough~` | ~~strikethrough~~ |
| Inline code   | `` `code` ``      | `code`            |

### Line breaks

Press `Enter` to start a new paragraph.

Press `Shift` + `Enter` to insert a soft line break in the same paragraph.

### Pasting Markdown

When pasting Markdown content directly into the editor, it’s important to use the **Paste and Match Style** option (typically <kbd>Shift</kbd> + <kbd>Cmd</kbd> + <kbd>V</kbd> on Mac or <kbd>Shift</kbd> + <kbd>Ctrl</kbd> + <kbd>V</kbd> on Windows).

If you use the standard Paste option for content copied from another editor or from the web, it may be inserted as a code block instead of formatted text.

### Titles

* Heading 1: `# A first-level title`
* Heading 2: `## A second-level title`
* Heading 3: `### A third-level title`

### Code blocks

` ```⏎ ` creates a new code block.

` ```py⏎ ` creates a new code block with Python syntax highlighting.

We use [Prism](https://github.com/PrismJS/prism) for syntax highlighting. Use [Test Drive Prism](https://prismjs.com/test.html#language=markup) to check supported languages.

If GitBook and Prism differ, we might be a version or two behind.

### Lists

GitBook automatically detects and creates ordered and unordered lists as you type.

* Begin a line with `-` or `*` to start an unordered bullet list.
* Begin a line with `1.` to start a numbered list.
* Begin a line with `- [ ]` to start a task list.

When writing lists, hit `Tab` to indent, and `Shift+Tab` to outdent.

### Quotes

Begin a line with `>` to create a block quote. If you select an entire paragraph from start to end, typing `>` will wrap the content in a block quote.

> This is a block quote.

### Dividers

Type `---` then hit `Enter` to create a divider on your page.

***

This is an example of a divider.
