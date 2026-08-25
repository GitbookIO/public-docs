---
description: Make your published docs easier for AI tools to discover, read, and use
---

# LLM-ready docs

GitBook automatically publishes AI-friendly formats for your docs site.

They help large language models (LLMs), coding agents, and AI search systems. These tools can discover and retrieve accurate documentation without parsing HTML.

## Markdown pages

Append `.md` to any published page URL to view its Markdown. Markdown gives AI tools structured content without the surrounding HTML.

<a href="https://gitbook.com/docs/publishing-documentation/llm-ready-docs.md" class="button primary">Check out the .md file for this page</a>

## llms.txt

[llms.txt](https://llmstxt.org/) is a proposed standard for LLM-friendly web content. Append `/llms.txt` to your docs site's root URL.

It lists every published page with a Markdown version. AI tools can use this index to discover your documentation.

<a href="https://gitbook.com/docs/llms.txt" class="button primary">Check out the /llms.txt for the GitBook docs</a>

## llms-full.txt

Append `/llms-full.txt` to your docs site's root URL. This file includes your full documentation content in one place.

Hidden pages are included in `llms-full.txt`. Hiding a page only removes it from the published table of contents.

<a href="https://gitbook.com/docs/llms-full.txt" class="button primary">Check out the /llms-full.txt file for the GitBook docs</a>

## MCP server for published docs

GitBook exposes a Model Context Protocol (MCP) server for every published docs site. Compatible tools can discover and retrieve your docs as structured resources.

Hidden pages remain available through the site’s MCP server. Hiding a page only removes it from the published table of contents.

Append `/~gitbook/mcp` to your docs site's root URL. For example, GitBook's MCP server is `https://gitbook.com/docs/~gitbook/mcp`.

{% hint style="info" %}
Opening this URL in a browser returns an error. Use a tool that can make HTTP requests.
{% endhint %}

Learn more in [MCP servers for published docs](../ai-for-your-readers/mcp-servers-for-published-docs.md).

## Optimizing your docs for AI

GitBook handles the delivery layer. Your writing shapes the quality of AI answers.

Write content that AI tools can interpret reliably:

* Give each page a clear purpose.
* Use descriptive headings and short sections.
* State constraints, defaults, and requirements directly.
* Include concrete examples and exact values.
* Update content when your product changes.

These practices improve retrieval, reduce ambiguity, and help people find answers.

### Keeping translations aligned

If you publish in multiple languages, keep each translation aligned with its source.

[Translations](../gitbook-agent-1/translations.md) let you localize content with GitBook Agent. When source content changes, GitBook can keep translated versions aligned.

### Measuring AI traffic

Use [Site analytics](../analytics/insights.md) to track traffic from LLMs and MCP clients.
