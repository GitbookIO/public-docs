---
description: Use the inline palette to add images, links, math & TeX, and more
---

# Inline content

<figure><img src="../../.gitbook/assets/10_01_25_inline_content.svg" alt=""><figcaption><p>Add inline elements to your content.</p></figcaption></figure>

The inline palette lets you quickly add extra content to your text block without moving your hands away from the keyboard. Simply hit `/` on any text block to open the inline palette. The forward slash will be replaced by the content you choose to insert.

### Annotations

With annotations, you can add extra context to your words without breaking the reader’s train of thought. You can use them to explain the meaning of a word, insert extra information, and more. Readers can hover over the annotated text to show the annotation above the text.

#### Create an annotation

To create an annotation, select the text you would like to annotate and click the **Annotate** option in the context menu. Once you’ve written your annotation, click outside of it to continue writing in the text block.

#### Markdown representation

You can write content as [Markdown footnotes](https://www.markdownguide.org/extended-syntax/#footnotes) to add them as annotations in GitBook.

```markdown
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.
```

### Images

Inline images will sit alongside your text on the page.&#x20;

By default, images are set to their original size with a maximum width of 300px. You can change the size by clicking the image to open the formatting palette, then choosing one of the three options:

1. **Inline size:** The image is proportionally sized to the font — great for icons and badges.
2. **Original size:** The image will remain inline at its original size, with a maximum width of 300 pixels.
3. **Convert to block:** This turns an inline image into a [image block](../blocks/insert-images.md), which is as wide as your content.&#x20;

{% hint style="info" %}
[Image blocks](../blocks/insert-images.md) offer more options, including more sizes and the ability to add a caption — but will not appear inline with your text.
{% endhint %}

### Emojis

You can add emojis by hitting `/` to open the inline palette. Alternatively, type `:` and a list of emojis will pop up directly in line — you can start typing the name of an emoji to narrow down the selection.

### Links

You can insert three different types of links:

* [Relative links](inline.md#relative-links)
* [Absolute links](inline.md#absolute-links)
* [Email address `mailto` links](inline.md#email-address-mailto-links)

#### Relative links

Relative links are links created by linking to [pages](../content-structure/page.md) that already exist in your space. The advantage of using relative links is that if the page’s URL, name, or location changes, its reference will be kept up to date — so you’ll end up with fewer broken links.&#x20;

Here’s how to insert a relative link:

1. Click somewhere in your paragraph where you want to insert the link, or select some text.
2. Hit / to open the inline palette and choose Link, click the **Link** button in the context menu, or hit **⌘ + K**.
3. Start typing the title of the page you want to link to.
4. Select the page from the drop-down search results.
5. Hit `Enter`.

#### Absolute links

Absolute links are external links that you can copy and paste into your content. They’re great when you want to link to something outside your documentation.

To insert an absolute link:

1. Click somewhere in your paragraph where you want to insert the link, or select some text.
2. Hit / to open the inline palette and choose Link, click the **Link** button in the context menu, or hit **⌘ + K**.
3. Paste the URL you want to link to.
4. Hit `Enter`.

#### Email address mailto links

Email address `mailto` links are useful when you want your visitors to click on a link that will open up their default email client and fill in the `To` field with the email address of your link, so they can write an email to send.

Here’s how to insert an email address `mailto` link:

1. Click somewhere in your paragraph where you want to insert the link, or select some text.
2. Hit / to open the inline palette and choose Link, click the **Link** button in the context menu, or hit **⌘ + K**.
3. Paste or type `mailto:something@address.com`, replacing `something@address.com` with the email address you would like to use.
4. Hit `Enter`.

### Math & TeX

Using this option, you can create an inline math formula in your content, like this: $$f(x) = x * e^{2 pi i \xi x}$$. We use the [KaTeX](https://katex.org/docs/supported.html) library to render formulas.

{% hint style="info" %}
You can also insert [a block-level math formula](../blocks/math-and-tex.md) by opening the command palette in an empty block and choosing the second Math & TeX option.
{% endhint %}

### Buttons

Buttons are a great way to describe calls to action. You can use them to send users to other pages in GitBook, or to external URLs.

Buttons have both primary and secondary styles. Here are a couple of examples:

<a href="https://app.gitbook.com/join" class="button primary">Sign up to GitBook</a> <a href="inline.md#annotations" class="button secondary">Go to top</a>
