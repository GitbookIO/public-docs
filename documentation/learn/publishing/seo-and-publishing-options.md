---
description: Reference for SEO controls and publishing-related site options.
---

# SEO and publishing options

Published documentation is automatically optimized for both search engines (SEO) and AI systems like ChatGPT, Claude, and Google AI Overview (GEO) — most of this happens automatically, so writing content with your target keywords and terms is usually all you need to do. This page is a reference for the options you can control directly.

### Page metadata

Each page's title and description double as its search-engine snippet — descriptions can run up to 200 characters. See [Page title and description](../../resources/the-gitbook-interface.md#page-title-and-description).

### Sitemap and caching

GitBook automatically generates a sitemap from your table of contents, and serves pages from a global CDN for performance — both handled for you, with nothing to configure.

### Search engine indexing

Control whether a published site (and individual pages within it) can be indexed by search engines — see [Publish and unpublish a site](publish-and-unpublish.md#public-publishing) for public/unindexed publishing and the page-level indexing inheritance model.

### Social preview

Control what a shared link looks like on Slack, X, and other platforms that read OpenGraph metadata — see [Social sharing and custom code](../customization/social-sharing-and-custom-code.md#social-preview).

### AI optimization (GEO)

GitBook automatically creates a Markdown version of every page, making it easy for LLMs to parse, and exposes a Model Context Protocol (MCP) server for every published site so AI tools can discover and retrieve your docs as structured resources — no scraping required. Your site also generates `llms.txt` and `llms-full.txt`, designed for AI ingestion.

See [Make your docs agent-ready](../gitbook-ai/readers-ai/make-your-docs-agent-ready.md) and [MCP server for published docs](../gitbook-ai/readers-ai/mcp-server-for-published-docs.md) for more.
