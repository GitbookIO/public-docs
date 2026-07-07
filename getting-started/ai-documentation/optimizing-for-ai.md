---
description: >-
  Make your docs easier for LLMs, coding agents, and AI search tools to consume
  and answer from
---

# Optimizing for AI

GitBook automatically publishes AI-friendly outputs for your site.

### Make your site easy for AI tools to consume

Every published GitBook site includes AI-friendly outputs:

* Add `.md` to a page URL to get the page as Markdown.
* Use `llms.txt` to give an agent a site-wide index.
* Use `llms-full.txt` to give an agent a full snapshot of the published docs.
* Use `/~gitbook/mcp` to let MCP-compatible tools read your docs directly.

These are generated automatically and make your docs easier for LLMs, IDEs, coding agents, and search systems to understand.

### Optimize for better AI answers

GitBook handles the delivery layer, but your writing still matters.

Clear headings, short sections, concrete examples, and current information help both humans and AI systems. If you want to improve how tools like ChatGPT, Claude, and Cursor interpret your docs, start with [LLM-ready docs](../../ai-and-search/llm-ready-docs.md).

### Keep translated docs aligned

If you publish docs in multiple languages, translation quality also affects AI answers.

[Translations](../../gitbook-agent/translations.md) let you localize your docs with GitBook Agent. When you update the source content, GitBook can keep translated versions aligned with those changes.

### Writing guidelines that help AI

Focus on these basics:

* Use clear heading hierarchy.
* Keep sections short and specific.
* Include concrete examples and exact values.
* Remove stale content quickly.

These practices improve retrieval, reduce ambiguity, and make answers more accurate.

### Measure how agents use your docs

Use [Site analytics](../../docs-site/insights.md) to track traffic from LLMs and MCP clients, and see how agents access your content.
