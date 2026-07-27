---
description: "The Cards block: what it does and how to use it."
---

# Cards

Use cards for a visually pleasing grid combining text and images — ideal for landing pages or displaying content non-linearly. Switch between medium and large sizes, and link each card to a resource.

### Adding links

Hover a card, open its Options menu, and add a target link so readers can click anywhere on the card to follow it.

{% hint style="success" %}
Use a target link rather than a hyperlink in the card's text — that way readers can click anywhere on the card, not just the link text.
{% endhint %}

### Adding images

Hover a card, open its Options menu (or click **Add cover image** directly on the card), and choose or upload an image in the **Select file** modal.

**For dark mode** — open the card's Options menu, choose **Cover → Edit cover → Add cover for dark mode**, and select an image the same way.

**Choosing the right size** — GitBook crops landscape images to 16:9 on both desktop and mobile. Portrait or 1:1 images crop to 16:9 on desktop, but stay square/portrait on mobile. For consistency across both, upload 16:9 images (e.g. 1920×1080). For a layout that adapts to screen size, use 1:1 images with centered content.

### Changing the size of cards

Open the block's Options menu — **Medium** shows three cards per row, **Large** shows two.

### Representation in Markdown

```markdown
<table data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
      <th data-hidden data-card-cover data-type="files"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Example title 1</strong></td>
      <td>Example description 1.</td>
      <td><a href="https://example.com">https://example.com</a></td>
      <td><a href="https://example.com/image1.svg">example_image1.svg</a></td>
    </tr>
  </tbody>
</table>
```
