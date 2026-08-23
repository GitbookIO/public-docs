---
description: >-
  GitBook handles most SEO automatically. Published sites are responsive,
  pre-rendered, and served via a global CDN, with little configuration needed
  from you.
---

# SEO

### What GitBook does automatically

#### Responsive design

Published content adapts to any screen size — phones, tablets, and desktops.

#### URLs and metadata

* Page URLs are based on the page title by default, but can be customized.
* Canonical URLs prevent duplicate content issues.
* HTML and Open Graph titles pull from the page and site title.
* Meta and Open Graph descriptions pull from the page description.
* Images support alt text, which helps both search engines and accessibility.
* HTML is pre-rendered server-side, so crawlers don't need JavaScript to index your content.

{% hint style="info" %}
GitBook doesn't generate keyword meta tags. Modern search engines don't use them for ranking — [Google confirmed this in 2009](https://developers.google.com/search/blog/2009/09/google-does-not-use-keywords-meta-tag).
{% endhint %}

#### Sitemaps

GitBook automatically generates a sitemap for any published site that isn't set to unlisted. To find it, append `/sitemap-pages.xml` to your site's home URL — for example, [gitbook.com/docs/sitemap-pages.xml](https://gitbook.com/docs/sitemap-pages.xml).

#### CDN and caching

All published content is cached and served via a global CDN. Faster load times improve both user experience and search rankings.

### What you can do

#### Set a custom domain

A custom domain like `docs.example.com` can improve search visibility compared to a `yourorganization.gitbook.io` subdomain. Set up a custom domain →

#### Improve indexing speed

GitBook has no control over how quickly search engines index your content, but two things can help:

1. Link to your site from pages that are already indexed. When Google re-crawls those pages, it's more likely to discover your site.
2. Submit your site to Google directly. This requires a custom domain and ownership verification via a TXT DNS record. [Submit your site to Google →](https://developers.google.com/search/docs/advanced/crawling/ask-google-to-recrawl)

#### Set up redirects

Moving content to GitBook or restructuring your site can break existing links and affect SEO. Set up [redirects](site-redirects.md) → to forward old URLs to new ones.

When you move or rename a page, GitBook automatically creates an [HTTP 307 redirect](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/307) from the old URL to the new one. [Learn more about automatic redirects →](site-redirects.md#about-automatic-redirects)
