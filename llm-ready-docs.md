---
description: Providing an LLM-friendly version of your docs site
icon: user-robot
---

# LLM-ready docs

We're building features that make it easier for Large Language Models (LLMs) to ingest and work with your documentation content.&#x20;

As LLMs become increasingly important for information retrieval and knowledge assistance, ensuring your documentation is LLM-friendly can significantly improve how these models understand and represent your products or services.

## .md pages

With GitBook, all of the pages of your docs site are automatically available as markdown files. If you add the `.md` extension to any page, you will see the content of that page rendered in markdown which you can pass to an LLM for more efficient processing than an HTML file.&#x20;

For example, if your docs page is found at [https://tomatopy.pizza/docs/getting-started/basic-concepts](https://tomatopy.pizza/docs/getting-started/basic-concepts), then you can view a markdown version of the page at [https://tomatopy.pizza/docs/getting-started/basic-concepts.md](https://tomatopy.pizza/docs/getting-started/basic-concepts.md).

## llms.txt index page

[llms.txt](https://llmstxt.org/) is a proposed standard for making web content available in text-based formats that are easier for LLMs to process. You can access the `llms.txt` page by appending `/llms.txt` to the root URL of your docs site.&#x20;

For example, if your docs are hosted at [https://tomatopy.pizza/docs/](https://tomatopy.pizza/docs/), you will find your `llms.txt` file at [https://tomatopy.pizza/docs/llms.txt](https://tomatopy.pizza/docs/llms.txt).

The `llms.txt` file serves as an index for your documentation site, providing a comprehensive list of all available markdown-formatted pages. With this file, you make it easier for LLMs to efficiently discover and process your documentation content.&#x20;

LLMs can use this index to navigate directly to the markdown versions of your pages, allowing them to incorporate your documentation into their context without needing to parse HTML.
