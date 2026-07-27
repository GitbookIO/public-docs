---
description: Optimize your published docs for consumption by LLMs and AI agents.
---

# Make your docs agent-ready

As LLMs become central to information retrieval, making your documentation LLM-friendly significantly improves how these models understand and represent your product. LLM-optimized docs help systems like ChatGPT, Claude, Cursor, and Copilot retrieve and give accurate, contextual responses about your product or API.

{% hint style="info" %}
Building your own agent that authors GitBook content, rather than optimizing your published docs for readers' agents? See Build with AI → Getting started → Agent quickstart instead.
{% endhint %}

### .md pages

Every page on your docs site is automatically available as a Markdown file — add the `.md` extension to any page URL to see its content rendered in Markdown, which you can pass to an LLM for more efficient processing than an HTML file.

### llms.txt

[llms.txt](https://llmstxt.org/) is a proposed standard for making web content available in LLM-friendly text formats. Access it by appending `/llms.txt` to your docs site's root URL.

The file serves as an index for your site, listing every available Markdown-formatted page — making it easier for LLMs to discover and process your documentation.

### llms-full.txt

Where `llms.txt` indexes page URLs and titles, `llms-full.txt` contains your entire documentation site's content in one file, ready to pass to an LLM as context.

{% hint style="info" %}
Hidden pages are included in `llms-full.txt` — hiding a page only removes it from the published table of contents.
{% endhint %}

LLMs can use `llms.txt` to navigate directly to the Markdown version of your pages, incorporating your docs into their context without parsing HTML.

### MCP server for published docs

GitBook automatically exposes a Model Context Protocol (MCP) server for every published site, giving AI tools a structured way to discover and retrieve your docs as resources — no scraping required. See [MCP server for published docs](mcp-server-for-published-docs.md).

### Tips for optimizing your docs for LLMs

With `.md` pages, `llms.txt`, and `llms-full.txt` generated automatically, these practices help LLMs understand and work with your content — and generally improve performance in AI-powered search and generative engine optimization (GEO). They also make your docs easier for people to read.

**Use clear, hierarchical structure.** Break up content with good headings (H1, H2, H3) instead of walls of text — bullet points, numbered lists, and shorter paragraphs make everything easier to parse.

**Write concise, jargon-free content.** Keep it simple, and skip complex technical terms unless you need them — LLMs do better when you say what you mean without fluff.

**Include practical examples.** Show, don't just tell — code snippets, API examples, and real scenarios help both LLMs and readers understand how things actually work.

**Keep content current and accurate.** Outdated docs mean LLMs give people wrong information about your latest features.

**Test with AI tools.** Ask ChatGPT or Claude questions about your docs to see how well they understand your content — you might be surprised by what works and what doesn't.
