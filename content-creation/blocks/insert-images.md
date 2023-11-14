---
description: Insert images content block
---

# Insert images

You can insert full-width images into your space, which can be aligned to the left, center, or right. You can optionally include alt text and/or a caption. For accessibility purposes, we highly recommend setting alt text.

### Example of an image block

Image blocks can display a gallery of images, like this:

![Each image](https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw1fHxib29rfGVufDB8fHx8MTYyODc1MTk5MA\&ixlib=rb-1.2.1\&q=85) ![can have its](https://images.unsplash.com/photo-1589998059171-988d887df646?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw5fHxib29rfGVufDB8fHx8MTYyODc1MTk5MA\&ixlib=rb-1.2.1\&q=85) ![own caption](https://images.unsplash.com/photo-1524995997946-a1c2e315a42f?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw2fHxib29rc3xlbnwwfHx8fDE2Mjg3NTIwNzY\&ixlib=rb-1.2.1\&q=85)

{% hint style="info" %}
You can now convert image blocks to full width by clicking on the <img src="../../.gitbook/assets/image (1).png" alt="" data-size="line"> next to the block. [Read more about full-width blocks.](./#new-full-width-blocks)
{% endhint %}

### Light & Dark mode

You're able to set different images for the light and dark mode versions of your published site. GitBook will automatically display the correct image depending on the mode your visitor is in.

To choose an image for light or dark mode, click the “Replace image” button while hovering over your image.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>Setting a Light or Dark mode image</p></figcaption></figure>

{% hint style="warning" %}
Note that light and dark mode images are not yet supported in some cases like Page covers or Card covers.&#x20;
{% endhint %}

### Light & Dark mode through GitHub/GitLab Sync

You can also add light & dark mode images in Markdown through HTML syntax (`<picture>` and `<source>`).

For block images, use the `<figure>` HTML element with a `<picture>` and `<source>` in it:

```html
Text before

<figure>
  <picture>
    <source srcset="https://user-images.githubusercontent.com/3369400/139447912-e0f43f33-6d9f-45f8-be46-2df5bbc91289.png" media="(prefers-color-scheme: dark)">
    <img src="https://user-images.githubusercontent.com/3369400/139448065-39a229ba-4b06-434b-bc67-616e2ed80c8f.png" alt="GitHub logo">
  </picture>
  <figcaption>Caption text</figcaption>
</figure>

Text after
```

For inline images (images with text around them), use the `<picture>` HTML element with a `<source>` in it:

```html
Text before the image <picture><source srcset="https://user-images.githubusercontent.com/3369400/139447912-e0f43f33-6d9f-45f8-be46-2df5bbc91289.png" media="(prefers-color-scheme: dark)"><img src="https://user-images.githubusercontent.com/3369400/139448065-39a229ba-4b06-434b-bc67-616e2ed80c8f.png" alt="The GitHub Logo"></picture> and text after the image
```

{% hint style="warning" %}
Note that we are not yet supporting [GitHub-only syntax](https://github.blog/changelog/2021-11-24-specify-theme-context-for-images-in-markdown/) through `#gh-dark-mode-only` or `#gh-light-mode-only`.
{% endhint %}

### Resizing

Hover over your image, and you'll see the SIZE control appear in the top-right corner. Click on it to change the size of your image from the available options.

<figure><img src="../../.gitbook/assets/image-resizing.png" alt=""><figcaption></figcaption></figure>

* **Full** - removes all size specifications and displays either a full size or capped at a maximum width of **735** **pixels** for larger images
* **Small** - 25% of the image size
* **Medium** - 50% of the image size
* **Large** - 75% of the image size

In the event that the image exceeds the size of the editor, the image's width will be limited to the ratio of the editor's width instead.

{% hint style="info" %}
When it comes to resizing images in an image gallery, the process and results can differ from resizing single images.
{% endhint %}

### Resizing images through Git Sync

If you want more control over the sizing of your image, you can specify the exact size using markdown in GitHub or GitLab.

When we export an image, we use the HTML tag `<img/>`. As per the specifications, we can specify the dimensions of the image using the `width` and `height` attributes, which only accept values in pixels or a combination of a number and a `%` sign.\
\
Valid variants of specifying the image dimensions are:\
\
`<img width="100" />`\
`<img width="100%" />`

### Related

If you are looking to embed external content into your pages, take a look at how to [embed a URL](embed-a-url.md).

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
```
