---
description: Providing an LLM-friendly version of your docs site
icon: user-robot
---

# LLM-ready docs

We’re building features that make it easier for Large Language Models (LLMs) to ingest and work with your documentation content.

As LLMs become increasingly important for information retrieval and knowledge assistance, ensuring your documentation is LLM-friendly can significantly improve how these models understand and represent your products or services.

LLM-optimized documentation ensures that AI systems like ChatGPT, Claude, Cursor, and Copilot can retrieve and provide accurate, contextual responses about your product or API.

## .md pages

With GitBook, all of the pages of your docs site are automatically available as markdown files. If you add the `.md` extension to any page, you will see the content of that page rendered in markdown which you can pass to an LLM for more efficient processing than an HTML file.

<a href="https://gitbook.com/docs/publishing-documentation/llm-ready-docs.md" class="button primary">Check out the .md file for this page</a>

## llms.txt

[llms.txt](https://llmstxt.org/) is a proposed standard for making web content available in text-based formats that are easier for LLMs to process. You can access the `llms.txt` page by appending `/llms.txt` to the root URL of your docs site.

The `llms.txt` file serves as an index for your documentation site, providing a comprehensive list of all available markdown-formatted pages. With this file, you make it easier for LLMs to efficiently discover and process your documentation content.

<a href="https://gitbook.com/docs/llms.txt" class="button primary">Check out the /llms.txt for the GitBook docs</a>

## llms-full.txt

Where the `llms.txt` file contains an index of all the page URLs and titles of of your documentation site, the `llms-full.txt` contains the full content of your documentation site in one file that can be passed to LLMs as context.

<a href="https://gitbook.com/docs/llms-full.txt" class="button primary">Check out the /llms-full.txt file for the GitBook docs</a>

LLMs can use this index to navigate directly to the markdown versions of your pages, allowing them to incorporate your documentation into their context without needing to parse HTML.

## MCP server

GitBook automatically exposes a Model Context Protocol (MCP) server for every published space. MCP gives AI tools a structured way to discover and retrieve your docs as resources — no scraping required.

Your MCP server can be reached by appending `/~gitbook/mcp` to the URL of the root of your docs site. For instance, the GitBook docs MCP server is located at `https://gitbook.com/docs/~gitbook/mcp`.&#x20;

{% hint style="info" %}
Visiting this URL in your browser will result in an error. Instead, you can share this with tools that can make HTTP requests, like LLMs or IDEs.
{% endhint %}

Learn more by reading [mcp-servers-for-published-docs.md](mcp-servers-for-published-docs.md "mention").

## Tips for optimizing your docs for LLMs

Now that your GitBook site automatically generates `.md` pages, `llms.txt`, and `llms-full.txt` files, these best practices will help LLMs effectively understand and work with your content.

By using these optimizations, you may also improve your documentation’s performance in AI-powered search engines and generative engine optimization (GEO).

The best part? These guidelines will generally make your docs easier for people to read as well.

### Use clear, hierarchical structure

Break up your content with good headings (H1, H2, H3) and don’t just write giant walls of text. Bullet points, numbered lists and shorter paragraphs make everything easier to read.

### Write concise, jargon-free content

Keep it simple and skip complex technical terms unless you really need them. LLMs do much better when you say what you mean without adding fluff.

### Include practical examples

Show, don’t just tell. Code snippets, API examples, and real scenarios help LLMs — and your users — understand how things actually work in practice.

### Keep content current and accurate

Nobody likes outdated docs. Regular updates mean LLMs won’t give people wrong information about your latest features and updates.

### Test with AI tools

Actually try asking ChatGPT or Claude questions about your docs to see how well they understand your content. You might be surprised by what works and what doesn’t.
