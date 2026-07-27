---
description: Markdown syntax supported by GitBook.
---

# Markdown reference

GitBook's editor lets you create formatted content using Markdown — a popular, keyboard-friendly markup syntax known for its simplicity.

{% hint style="info" %}
Learn more about Markdown itself at [CommonMark](https://commonmark.org/help/).
{% endhint %}

### Text formatting

| Formatting | Markdown | Result |
|---|---|---|
| Bold | `**bold**` | **bold** |
| Italic | `_italic_` | _italic_ |
| Strikethrough | `~strikethrough~` | ~~strikethrough~~ |
| Inline code | `` `code` `` | `code` |

### Line breaks

Press `Enter` for a new paragraph. Press `Shift+Enter` for a soft line break within the same paragraph.

### Pasting Markdown

Use **Paste and Match Style** (Shift+Cmd+V on Mac, Shift+Ctrl+V on Windows) when pasting Markdown directly into the editor. The standard paste option can insert content copied from another editor or the web as a code block instead of formatted text.

### Titles

* Heading 1: `# A first-level title`
* Heading 2: `## A second-level title`
* Heading 3: `### A third-level title`

### Code blocks

` ``` ` followed by Enter creates a code block. ` ```py ` followed by Enter creates one with Python syntax highlighting. GitBook uses [Prism](https://github.com/PrismJS/prism) for highlighting — check [Test Drive Prism](https://prismjs.com/test.html#language=markup) for supported languages; if GitBook and Prism differ, GitBook might be a version or two behind.

### Lists

GitBook detects and creates lists as you type:

* Start a line with `-` or `*` for an unordered (bullet) list.
* Start a line with `1.` for a numbered list.
* Start a line with `- [ ]` for a task list.

Use `Tab` to indent and `Shift+Tab` to outdent.

### Quotes

Start a line with `>` for a block quote — or select an entire paragraph and type `>` to wrap it.

### Dividers

Type `---` and hit `Enter` to create a [divider](blocks/divider.md).
