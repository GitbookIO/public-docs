---
description: Insert images content block
---

# Insert images

You can insert full-width images into your space, which can be aligned to the left, center, or right. You can optionally include alt text and/or a caption. For accessibility purposes, we highly recommend setting alt text.

### Example of an image block

Image blocks can display a gallery of images, like this:

![Each image](https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw1fHxib29rfGVufDB8fHx8MTYyODc1MTk5MA\&ixlib=rb-1.2.1\&q=85) ![can have its](https://images.unsplash.com/photo-1589998059171-988d887df646?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw5fHxib29rfGVufDB8fHx8MTYyODc1MTk5MA\&ixlib=rb-1.2.1\&q=85) ![own caption](https://images.unsplash.com/photo-1524995997946-a1c2e315a42f?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw2fHxib29rc3xlbnwwfHx8fDE2Mjg3NTIwNzY\&ixlib=rb-1.2.1\&q=85)

### Related

If you are looking to embed external content into your pages, take a look at how to [embed a URL](embed-a-url.md).

### Git Sync representation in Markdown

```markdown
//Simple Block
![](https://gitbook.com/images/gitbook.png)

//Block with Caption
![The GitBook Logo](https://gitbook.com/images/gitbook.png)

//Block with Alt text
<figure><img src="https://gitbook.com/images/gitbook.png" alt="The GitBook Logo"></figure>

//Block with Caption and Alt text
<figure><img src="https://gitbook.com/images/gitbook.png" alt="The GitBook Logo"><figcaption><p>GitBook Logo</p></figure>
```
