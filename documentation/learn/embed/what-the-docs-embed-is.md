---
description: The Docs Embed puts your documentation and Assistant inside your own product.
---

# What the Docs Embed is

The Docs Embed is a window into your product knowledge that you can add to any product or website. Users can ask questions to [GitBook Assistant](../gitbook-ai/assistant/README.md), search your docs, or browse pages directly, without leaving your product. Open it with a button, place it in any component, or control it entirely programmatically.

### What's inside

The embed can show three tabs, all enabled by default — set `tabs` to show only specific ones:

* **Assistant** — the AI-powered chat interface that helps users find answers.
* **Search** — a focused surface for quickly finding pages and asking scoped questions.
* **Docs** — a browser for navigating your documentation site.

You can override the default configuration with custom actions, tools, suggested questions, [authenticated access](authenticate-the-embed.md), and more — see [Customize the embed](customize-the-embed/README.md).

### Before you start

1. Your docs must be **published** and accessible at a URL (e.g. `https://docs.company.com`).
2. Retrieve the embed script URL from your site settings (**Settings → AI & MCP → Embed**).

{% hint style="info" %}
To use the Assistant tab, [GitBook Assistant must be enabled](../gitbook-ai/assistant/enable-assistant.md) for your docs site (**Settings → AI & MCP**).
{% endhint %}

When you're ready, see [Install the embed](install-the-embed.md) to add it to your site.
