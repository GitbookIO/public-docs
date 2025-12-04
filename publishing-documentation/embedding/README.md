---
description: >-
  Choose the embedding method that best fits your tech stack and integration
  requirements
icon: window-restore
---

# Embedding

Embed your GitBook docs in your product or website using the Docs Embed included in your site.

The Docs Embed can contain two tabs:

- **Assistant**: The [GitBook Assistant](../gitbook-ai-assistant.md) - an AI-powered chat interface to help users find answers
- **Docs**: A browser for navigating your documentation site

The embed is set up automatically based on your site's configuration. You can optionally customize and override the configuration with custom actions, tools, suggested questions, [Authenticated Access](../authenticated-access/README.md), and more.

<div data-with-frame="true"><figure><img src="../../../.gitbook/assets/emebeddable_assistant.png" alt="Embed GitBook Assistant into your product or website"><figcaption><p>Embed GitBook Assistant into your product or website</p></figcaption></figure></div>

### Choose your implementation method

Pick the approach that matches your setup:

- [**Script tag**](implementation/script.md) – Drop in a `<script>` tag for the fastest setup, then customize its appearance
- [**Node.js/NPM**](implementation/nodejs.md) – Install via NPM for server-side rendering or build-time control
- [**React component**](implementation/react.md) – Use prebuilt React components for seamless integration

### Prerequisites

Before embedding your docs, ensure:

1. **Your docs are published** and accessible at a URL (e.g., `https://docs.company.com`).
2. **You have retrieved the embed script URL** from your site settings (Settings → AI & MCP → Embed).

**Note**: If you want to use the Assistant tab, [GitBook Assistant must be enabled](../gitbook-ai-assistant.md) for your docs site (Settings → AI & MCP).

### Package reference

For the complete API reference and source code, see the [`@gitbook/embed` package on GitHub](https://github.com/GitbookIO/gitbook/tree/main/packages/embed).

### What's next?

Choose your embedding method above, then explore:

- [Using with authenticated docs](authentication/using-with-authenticated-docs.md) – Required if your docs require sign-in
- [Customizing the Embed](configuration/customizing-gitbook-assistant.md) – Add welcome messages, custom actions, and suggestions
- [Creating custom tools](configuration/creating-custom-tools.md) – Connect Assistant to your product APIs
- [API Reference](configuration/reference.md) – Complete API documentation
