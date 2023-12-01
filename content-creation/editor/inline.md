---
description: Space inline content
---

# Inline content

You can choose to insert inline content using the inline palette. This palette becomes available when you type a forward slash. The forward slash will be replaced by the inline content you choose to insert.

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/inline-menu.png" alt="Screenshot showing the inline palette with all the inline options available to an editor."><figcaption><p>Inline palette</p></figcaption></figure>

</div>

## Annotations

Annotations allow you to add more context to your text without breaking the reader’s train of thought.

### Example of an annotation

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/annotations_example.png" alt=""><figcaption><p>Example of an annotation</p></figcaption></figure>

</div>

### How to create an annotation

To create an annotation select the word or phrase you would like to annotate. Once you have selected the text, write the annotation, then click out of it to continue writing in your main paragraph.

### Git Sync representation in Markdown

Markdown footnotes will be imported as annotations

## Images

You can insert inline images to your content. By default, their size is proportional to the font size as their main purpose is to be inserted in line with your content. This is great for badges and icons.‌

There are 3 different sizes of inline images:‌

1. **Inline size:** the default one is proportionally sized to the font.
2. **Original size:** will remain inline but with its original size with a maximum width.
3. **Convert to block:** this turns an inline image into a [block image](../blocks/insert-images.md) with its original size.

{% hint style="info" %}
You can switch the size of an inline image by clicking on the image to open the formatting palette, and then choosing one of the options above.
{% endhint %}

## Emojis

You can add emoji by opening the **inline palette**. Alternatively, type `:` and a list of emojis will pop up directly in line.&#x20;

## Links

You can insert three different types of links:

- [Relative links](inline.md#relative-links)
- [Absolute links](inline.md#absolute-links)
- [Email address `mailto` links](inline.md#email-addresses)

## Relative links

Relative links are links created by linking pages that already exist in your content. The advantage of using relative links is that if the page’s URL, name, or location changes, its reference will be kept up to date resulting in fewer broken links.

Here’s how to insert a relative link:

1. Select some text or click somewhere in your paragraph where you want to insert the link.
2. Wait for the inline palette to appear.
3. Click the inline palette.
4. Start typing the page title.
5. Select the page from the drop-down search results.
6. Hit `enter`.

## Absolute links

Absolute links are for external links.

{% hint style="info" %}
External links will always open in a new tab.
{% endhint %}

Here’s how to insert an absolute link:

1. Select some text or click somewhere in your paragraph where you want to insert the link.
2. Wait for the inline palette to appear.
3. Click the inline palette.
4. Paste a URL.
5. Hit `enter`.

## Email address mailto links

Email address `mailto` links are useful when you want your visitors to click on a link that will open up their default email client, fill in `TO` with the email address of your link, and allow them to write an email to send out.

Here’s how to insert an email address `mailto` link:

1. Select some text or click somewhere in your paragraph where you want to insert the link.
2. Wait for the inline palette to appear.
3. Click the inline palette.
4. Paste or type `mailto:something@address.com`, replacing `something@address.com` with the email address you would like to use.
5. Hit `enter`.

## Math & TeX

You can create an inline math formula like this: $$f(x) = x * e^{2 pi i \xi x}$$

{% hint style="info" %}
You can also insert a block-level math formula directly from the [**command palette**](../blocks/#math-equation).
{% endhint %}
