---
description: Optimize your GitBook documentation to be discoverable via search engines.
---

# SEO

## Overview <a href="#overview" id="overview"></a>

Thanks to the following features, your GitBook projects are SEO-friendly, with little or no configuration on your end:

* ​Custom domains (e.g: `docs.example.com`)
* ​All public content is cached and served via our global CDN
* ​All content is responsive and mobile-friendly
* ​We automatically generate SEO-friendly content (URLs, HTML, etc.)

## Technicalities <a href="#technicalities" id="technicalities"></a>

* ​We automatically generate sitemaps based on your ToC
* We generate SEO friendly URLs based on each page's title
* ​The HTML we generate covers the essentials:
  * We generate HTML titles and descriptions based on your GitBook page's title and description
  * We avoid duplicate content through smart canonical URLs
  * Image captions are rendered as alt attributes
* ​HTML sent to crawlers is pre-rendered (i.e server-side) this means that crawlers do NOT need JavaScript to index your content ([app.gitbook.com](https://app.gitbook.com) is a [Single Page Application](https://en.wikipedia.org/wiki/Single-page\_application) and requires JS, but not user content).

## Notes <a href="#notes" id="notes"></a>

We don't generate keyword meta tags, because modern search engines do not use them to rank pages. This was officially confirmed by Google a few years ago.

{% embed url="https://webmasters.googleblog.com/2009/09/google-does-not-use-keywords-meta-tag.html" %}
