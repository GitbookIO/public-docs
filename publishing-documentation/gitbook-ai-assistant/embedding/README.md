---
description: >-
  Choose the embedding method that best fits your tech stack and integration
  requirements
if: visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Embedding

GitBook Assistant can be embedded directly into your website or app, giving your users instant access to product knowledge right where they need it.

<div data-with-frame="true"><figure><img src="../../../.gitbook/assets/emebeddable_assistant.png" alt="Embed GitBook Assistant into your product or website"><figcaption><p>Embed GitBook Assistant into your product or website</p></figcaption></figure></div>

### Choose your integration method

Pick the approach that matches your setup:

* [**Script tag**](script.md) – Drop in a `<script>` tag for the fastest setup
* [**Node.js/NPM**](nodejs.md) – Install via NPM for server-side rendering or build-time control
* [**React component**](react.md) – Use prebuilt React components for seamless integration

### Prerequisites

Before embedding the Assistant, ensure:

1. **GitBook Assistant is enabled** for your docs site (Settings → AI & MCP)
2. **Your docs are published** and accessible at a URL (e.g., `https://docs.company.com`)
3. **You have the embed script URL** from your site settings (Settings → AI & MCP → Embed)

### What's next?

Choose your embedding method above, then explore:

* [Using with authenticated docs](../authentication/using-with-authenticated-docs.md) – Required if your docs require sign-in
* [Customizing the Assistant](../configuration/customizing-gitbook-assistant.md) – Add welcome messages, buttons, and suggestions
* [Creating custom tools](../configuration/creating-custom-tools.md) – Connect Assistant to your product APIs
