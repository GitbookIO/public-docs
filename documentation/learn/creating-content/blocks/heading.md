---
description: "The Heading block: what it does and how to use it."
---

# Heading

Headings give your documents structure — and keywords in headings help search engines understand that structure, which can help your page rank higher.

GitBook offers three heading levels. H1 and H2 appear in the [page outline](../../../resources/the-gitbook-interface.md#page-outline).

### Anchor links

Adding a heading creates an anchor link, so you can link directly to that section.

**Link to an anchor** — hover the title (in public content, or private content in read-only mode) and click the `#` that appears, which updates your browser's URL bar so you can copy it. To link from a page within your section, use a [relative link](../format-your-content.md#links) instead, so it updates automatically if the heading changes.

**Edit an anchor** — by default, the anchor matches your header text, so changing the header later breaks any external link to that anchor. To prevent this, open the header's Options menu, choose **Edit anchor**, and set a fixed anchor that survives header changes.

### Representation in Markdown

GitBook generates SEO-optimized pages, so page titles are automatically represented as a first-level heading:

```markdown
# I'm a page title
```

This means that if you [sync your content with Git](../../git-sync/README.md), page headers added through the editor are represented one level lower:

```markdown
## My heading 1
### My heading 2
#### My heading 3
```

{% hint style="info" %}
Page titles are separate from heading blocks in the page body. Hiding the page title in **Page options** doesn't remove your H1, H2, and H3 headings.
{% endhint %}
