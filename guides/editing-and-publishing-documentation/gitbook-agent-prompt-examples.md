---
description: >-
  Discover 7 practical ways teams use GitBook Agent to optimize docs for SEO and
  AI, automate content updates, import from PDF and Microsoft Word files, and
  manage documentation at scale
---

# 7 ways teams are using GitBook Agent to streamline their docs workflows (with prompt examples)

[GitBook Agent](/broken/spaces/NkEGS7hzeqa35sMXQZ4X/pages/KHHFlE1MtpVIaZboN8b2) unlocks all kinds of abilities for documentation maintainers — from bulk content operations to automated housekeeping tasks.

This post highlights some of the most practical and creative ways teams (including us!) are using the Agent inside their documentation spaces — with real prompts you can try yourself.

Use these examples as inspiration for streamlining your own workflows and unlocking new ways to manage content at scale.

### 1. Find and replace across an entire space

Find and replace has been a common request in our support queue for a while. Until now, the best process to achieve this was to enable [Git Sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync), pull your content into a code editor, run a find-and-replace locally, and push the changes back to GitBook.

Now it's possible to do this directly in the GitBook UI by asking the Agent. Here’s an example prompt:

> Find all instances of “Gitbook” (lowercase ‘b’) in my space and replace them with “GitBook” (capital B). Ignore any in code blocks or URLs. Let me know how many replacements you make.

The Agent handles the sweep for you — and respects formatting constraints you specify.

### 2. Bulk-add page descriptions

GitBook uses page descriptions to generate meta tags. These descriptions [improve SEO](../seo-and-llm-optimization/how-to-use-seo-techniques-to-improve-your-documentation.md) and [give LLMs stronger semantic signals](../seo-and-llm-optimization/geo-guide.md) about your content. But on larger spaces, they’re easy to miss.

But instead of adding them manually, now you can let the Agent fill the gaps.

> Go through all pages in my space. For any page missing a description, generate and add an appropriate page description based on the page content. Make these descriptions informative and optimized for SEO and AEO.

You get consistent, search-friendly descriptions across your entire space in minutes.

### 3. Optimize for SEO and AI ingestion

Talking of SEO, search engines — and AI systems — rely on structure, clarity, and semantic signals to understand your content.&#x20;

Over time, documentation spaces naturally drift: headings become inconsistent, keywords aren’t used intentionally, images have missing alt text, and internal links don’t reflect how topics relate to each other.

The Agent can audit your space and optimize it for search and AI — tightening structure, clarifying intent, and making your content easier to index, retrieve, and cite. Here’s an example prompt:

> Audit my entire space for SEO and AI optimization.
>
> For each page:\
> – Ensure headings follow a clear H1–H3 hierarchy and are descriptive.\
> – Improve clarity and keyword alignment based on the page topic.\
> – Add or refine page descriptions to be concise and search-optimized.\
> – Suggest or add internal links to related pages where relevant.\
> – Add missing alt text to images.\
> – Rewrite any vague section titles to be more specific and intent-driven.
>
> Prioritize clarity, structured content, and semantic richness to improve both search engine rankings and LLM ingestion.

You can also run a more focused version of this prompt on a specific section of your docs if you’d rather optimize incrementally.

### 4. Import/convert PDF and MS Word content to GitBook pages

PDFs and Microsoft Word docs can be convenient for sharing content — but adding them to your docs site is better. However, converting these files into into clean, structured Markdown documentation has always been a pain.&#x20;

Before, we’d help users convert their content into Markdown with external tools, clean up the formatting, then import them via Git Sync. Now the Agent can do it directly. Simply upload a PDF or document and use a prompt like:

> Convert this PDF into GitBook pages while maintaining the original structure. Convert all elements (headings, lists, tables, images, code blocks, etc.) into their corresponding GitBook blocks. Create the pages with the converted content.

The Agent analyzes layout and structure — then recreates it using native GitBook blocks.

### 5. Fix broken relative links

Documentation is always a work in progress. Pages get renamed, moved, or deleted — and broken links inevitably follow.&#x20;

While [GitBook flags broken links](/broken/spaces/NkEGS7hzeqa35sMXQZ4X/pages/V297D65uuYU7RDPKpkSV) in the UI, identifying every occurrence across a large space can be time-consuming. The Agent can find and fix broken links for you:

> Check all pages in my space for broken relative links. Give me a list organized by destination page, showing: the broken destination page and all occurrences (which pages the broken links appear on).

Then follow up with:

> Replace all links pointing to \[page x] with links to \[page y] throughout my entire space.

You can clean up structural debt across your documentation in a single workflow.

### 6. Generate TL;DR summaries

Long pages benefit from a quick summary at the top. It makes them more scannable, supports search visibility, and helps AI systems extract key points.&#x20;

The Agent can generate and format these consistently with a prompt like this:

> Read the content of each page in my space and generate a TL;DR summary. Add it as an info hint block at the top of each page with this format: a “TL;DR” heading followed by the summary in bullet points or numbered lists as appropriate.

This works especially well for API references, internal process documentation, and technical deep dives. We’ve heard from customers who use this for internal process docs, as well as large technical reference pages.

### 7. Automatically add relevant page icons

Choosing [page icons](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/content-structure/page#page-icons-and-emojis) manually across a large space is repetitive — and often inconsistent. Thankfully, the Agent can assign them contextually:

> Add appropriate icons to all page titles in my space based on each page’s title and content.

It’s a small improvement — but across hundreds of pages, it saves time and creates visual consistency.

***

These are just a few of the ways teams are already [using GitBook Agent](/broken/spaces/NkEGS7hzeqa35sMXQZ4X/pages/KHHFlE1MtpVIaZboN8b2). Tasks that used to require external tooling, scripting, or manual cleanup can now happen directly inside your documentation space.

We’re excited to see what you build next!
