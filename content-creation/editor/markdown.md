# Markdown

The editor allows you to include formatted text using rich text, as well as markdown.&#x20;

Markdown is a popular markup syntax that's widely known for its simplicity and popularity online. GitBook supports it as a keyboard-friendly way to write rich and structured text.

{% hint style="info" %}
You can learn more about Markdown itself by visiting [Common Mark](https://commonmark.org/help/).
{% endhint %}

## Text formatting <a href="#text-formatting" id="text-formatting"></a>

We support all the classic inline Markdown formatting:

| Formatting    | Markdown version  | Result            |
| ------------- | ----------------- | ----------------- |
| Bold          | `**bold**`        | **text**          |
| Italic        | `_italic_`        | _italic_          |
| Strikethrough | `~strikethrough~` | ~~strikethrough~~ |

## Titles

* Heading 1: `# A first-level title`
* Heading 2: `## A second-level title`
* Heading 3: `### A third-level title`

## Code blocks

\`\`\``⏎` creates a new code block.

\`\`\``py⏎` creates a new code block with Python syntax highlighting.

{% hint style="info" %}
We use [Prism](https://github.com/PrismJS/prism) for syntax highlighting. Here's an easy way to check which languages Prism supports: [Test Drive Prism](https://prismjs.com/test.html#language=markup). If you notice a mismatch between GitBook and Prism, there's a chance we are a version or two behind. We'll catch up soon!
{% endhint %}

## Lists

We automatically detect ordered and unordered lists as you type.

* Begin a line with `-` or `*` to start a bullet list.
* Being a line with `1.` to start a numbered list. Use `Tab` to go one level deeper, and `Shift+Tab` to go up.
* Begin a line with `- [ ]` to start a task list.

## Quotes

Begin a line with `>` to create a block quote. If you select an entire paragraph from start to end, typing `>` will wrap the content in a block quote.

> This is a block quote
