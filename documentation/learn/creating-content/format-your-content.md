---
description: Text formatting, inline elements, and styling options in the editor.
---

# Format your content

Select text and choose a format from the context menu, or use a keyboard shortcut or Markdown syntax.

{% hint style="info" %}
Shortcuts below use Mac keys — use **Control** instead of **⌘** on Windows or Linux. See [Keyboard shortcuts](../../resources/keyboard-shortcuts.md) for every OS.
{% endhint %}

| Format | Shortcut | Markdown |
|---|---|---|
| Bold | ⌘+B | `**Bold**` |
| Italic | ⌘+I | `_Italic_` |
| Strikethrough | ⇧+⌘+S | `~~Strikethrough~~` |
| Code | ⌘+E | `` `Code` `` |
| Link | ⌘+K | `[text](url)` |

**Link.** When you add a link, you'll be prompted for the URL — any URL works, but for another page or section in your site, use a relative link so it stays valid if the target moves.

**Color and background color.** Click the color icon in the context menu to set a text or background color.

## The inline palette

Hit `/` on any text block to open the inline palette and quickly add extra content without leaving the keyboard — the `/` is replaced by whatever you insert.

### Annotations

Add extra context to a word or phrase without breaking the reader's flow — readers hover the annotated text to see it. Select text and click **Annotate** in the context menu, then write your annotation.

In Markdown, write annotations as [footnotes](https://www.markdownguide.org/extended-syntax/#footnotes), with the footnote indicator immediately after the annotated word (not after punctuation):

```markdown
Here's a simple footnote[^1], and here's a longer one[^bignote].

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.
```

### Inline images

Inline images sit alongside your text. By default they're sized to their original dimensions, capped at 300px wide — click the image to choose:

1. **Inline size** — proportional to the surrounding font, good for icons and badges.
2. **Original size** — inline at full size, capped at 300px.
3. **Convert to block** — turns it into an [image block](blocks/image.md), as wide as your content.

{% hint style="info" %}
Image blocks offer more options — more sizes, a caption — but won't sit inline with text.
{% endhint %}

In Markdown: `<img src=".gitbook/assets/example.jpg" alt="Example" data-size="line">`

### Emojis

Hit `/` to open the inline palette, or type `:` to trigger an inline emoji picker — start typing an emoji's name to narrow the list. In Markdown: `:house:`, `:car:`, `:dog:`.

### Links

Three types:

**Relative links** — link to a page that already exists in your section. If the page's URL, name, or location changes later, the reference updates automatically, so you get fewer broken links. Click where you want the link (or select text), open the link tool (`/`, the context menu, or ⌘+K), type the target page's title, and select it from the results.

**Absolute links** — external URLs you paste in, for linking outside your documentation. Same steps, but paste the URL instead of searching.

{% hint style="info" %}
External links open in the same tab, not a new one — GitBook follows this [W3C-recommended behavior](https://www.w3.org/TR/WCAG20-TECHS/G200.html) for accessibility and a consistent experience.
{% endhint %}

**Email (`mailto`) links** — open the reader's default email client with your address pre-filled. Same steps, but type or paste `mailto:something@address.com`.

In Markdown:

```markdown
[This is a relative link to another page in this section](content-structure.md)
[This is an absolute link](https://www.gitbook.com/blog)
[This is a link](mailto:support@gitbook.com) to our support email address
```

### Math & TeX (inline)

Create an inline math formula, like $$f(x) = x * e^{2 pi i \xi x}$$, rendered with the [KaTeX](https://katex.org/docs/supported.html) library. Insert a block-level formula instead by opening the block palette in an empty block and choosing the block-level Math & TeX option — see [Math & TeX](blocks/math-and-tex.md).

In Markdown:

```markdown
$$f(x) = x * e^{2 pi i \xi x}$$
```

### Icons

Add extra visual indicators inline — in a paragraph, inside a card, or anywhere you want some flair. Icons use the visual style from your customization settings. Browse the full set at [Font Awesome](https://fontawesome.com/).

In Markdown: `<i class="fa-github">:github:</i>`
