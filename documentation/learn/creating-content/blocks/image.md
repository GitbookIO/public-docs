---
description: "The Image block: what it does and how to use it."
---

# Image

Insert an image, choose its size and alignment (left, center, right), and optionally add alt text and/or a caption.

{% hint style="info" %}
Set alt text on images for accessibility.
{% endhint %}

### Uploading an image

Two ways to add one:

1. Drag and drop an image from your file system directly into an empty block.
2. Add an image block, then use the **Select images** panel — upload a file, pick a previously uploaded one, paste an image URL, or search [Unsplash](https://unsplash.com/) directly.

{% hint style="warning" %}
GitBook allows uploads up to 100MB per file.
{% endhint %}

**Create an image gallery** — add more than one image to a block to create a gallery. Open the block's Options menu and choose **Add images…** to reopen the panel. To remove one, open its Edit menu and press **Delete**.

### Light and dark mode images

Set different images for light and dark mode — GitBook shows the right one automatically. Hover the image, open its Edit menu, click **Replace image**, then choose **Add image for Dark mode**. Replace either image from the same menu afterward.

{% hint style="warning" %}
Light/dark mode images aren't currently supported for page covers or [card](cards.md) image covers.
{% endhint %}

**Through Git Sync**, use HTML `<picture>`/`<source>` syntax. For a block image, wrap a `<figure>` around a `<picture>`:

```html
<figure>
  <picture>
    <source
      srcset="https://example.com/dark.png"
      media="(prefers-color-scheme: dark)"
    />
    <img
      src="https://example.com/light.png"
      alt="GitHub logo"
    />
  </picture>
  <figcaption>Caption text</figcaption>
</figure>
```

For an inline image, use `<picture>`/`<source>` without the `<figure>` wrapper.

{% hint style="warning" %}
GitBook doesn't yet support GitHub-only `#gh-dark-mode-only` / `#gh-light-mode-only` syntax.
{% endhint %}

### Resizing

Hover the image, open its Edit menu, and click **Size**:

* **Small** — 25% of the image size
* **Medium** — 50%
* **Large** — 75%
* **Fit** — full size, capped at 735px wide for larger images

If an image is wider than the editor, GitBook caps it to the editor's width, and resizing is based on that limit.

{% hint style="info" %}
Resizing an image inside a gallery can behave differently than resizing it alone.
{% endhint %}

**Through Git Sync**, specify exact pixel or percentage dimensions using the `<img/>` tag's `width`/`height` attributes — e.g. `<img width="100" />` or `<img width="100%" />` (still capped by the editor).

### Aligning images

By default, images show at full size, centered. To change this, open the block's Options menu and choose an alignment — this only affects images narrower than the editor, or images you've resized.

### Framing images

Add a frame to give an image a consistent look, visually separated from surrounding content — hover it, open the Options menu, and enable **With frame**.

{% hint style="info" %}
Only single images can be framed — galleries and inline images can't.
{% endhint %}

### Representation in Markdown

```markdown
//Simple Block
![](https://gitbook.com/images/gitbook.png)

//Block with Caption
![The GitBook Logo](https://gitbook.com/images/gitbook.png)

//Block with Alt text
<figure><img src="https://gitbook.com/images/gitbook.png" alt="The GitBook Logo"></figure>

//Block with Caption and Alt text
<figure><img src="https://gitbook.com/images/gitbook.png" alt="The GitBook Logo"><figcaption><p>GitBook Logo</p></figcaption></figure>

// Block with framed image
<div data-with-frame="true"><img src="https://gitbook.com/images/gitbook.png" alt="The GitBook Logo"></div>
```
