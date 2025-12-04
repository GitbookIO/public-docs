---
description: >-
  GitBook Assistant offers users answers based on your docs and tailored to
  their situation — not just generic responses
icon: gitbook-assistant
---

# GitBook Assistant

{% include "../../.gitbook/includes/ultimate-hint.md" %}

<figure><img src="../../.gitbook/assets/23_07_25_gitbook_assistant.svg" alt="GitBook Assistant"><figcaption><p>The GitBook Assistant</p></figcaption></figure>

GitBook Assistant gives your users fast, accurate answers about your documentation using natural language. It's personalized to your users, can be embedded into your website or product, and is available in the sidebar of your published docs.

Think of it as a product expert available to all of your users, in the places and times they need it most.

The Assistant uses agentic retrieval to understand the context of queries based on the user's current page, previously-read pages, and previous conversations.

<p align="center"><a href="https://gitbook.com/docs/publishing-documentation/gitbook-ai-assistant?ask=how+does+the+gitbook+assistant+help+tie+product+knowledge+closer+to+users+in+my+product" class="button primary">Test GitBook Assistant</a></p>

### Enable GitBook Assistant <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

To enable GitBook Assistant, open your site's dashboard, navigate to the **Settings** page and choose **AI & MCP** from the menu on the left. Here you can enable GitBook Assistant from the options available.

### Using GitBook Assistant in published docs <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

Users can access GitBook Assistant in three ways:

* Press <kbd>⌘</kbd> + <kbd>I</kbd> on Mac or <kbd>Ctrl</kbd> + <kbd>I</kbd> on PC
*   Click the **GitBook Assistant**&#x20;

    <picture><source srcset="../../.gitbook/assets/gitbook-assistant-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/gitbook-assistant.svg" alt=""></picture>

    &#x20;button next to the **Ask or search…** bar
* Type a question into the **Ask or search…** bar and choose the 'Ask…' option at the top of the menu

{% if visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true %}
#### Embed GitBook Assistant in your product

You can embed GitBook Assistant directly into your product or website, giving users instant access to AI-powered help without leaving your application. The Assistant can be embedded as part of [Docs Embed](../embedding/README.md), which includes both the Assistant tab for AI-powered chat and a Docs tab for browsing your documentation.

Choose the embedding method that fits your stack:

* [**Script tag**](../embedding/script.md) – Quick setup with a `<script>` tag
* [**Node.js/NPM**](../embedding/nodejs.md) – Server-side or build-time integration
* [**React component**](../embedding/react.md) – Prebuilt React components

**Additional guides:**

* [Using with authenticated docs](../embedding/authentication/using-with-authenticated-docs.md) – Required if your docs need sign-in
* [Customizing the Embed](../embedding/configuration/customizing-gitbook-assistant.md) – Welcome messages, actions, and suggestions
* [Creating custom tools](../embedding/configuration/creating-custom-tools.md) – Connect Assistant to your APIs
* [API Reference](../embedding/configuration/reference.md) – All available methods and events
{% endif %}

### Extend GitBook Assistant with MCP servers

You can also add external data sources to GitBook Assistant to give it more context and data to pull answers from. You can do this by connecting Assistant to MCP servers for external platforms, such as:

* Your community (Slack, Discord, GitHub Communities etc)
* Support tools (Intercom etc)
* Your future product roadmap (GitHub, Linear etc)
* Docs for external integrations with products

To add an MCP server to GitBook Assistant, follow these steps:

{% stepper %}
{% step %}
**Open your site's settings**

Navigate to your site dashboard and choose the **Settings** option from the site header. Then choose the **AI & MCP** section from the left-hand menu
{% endstep %}

{% step %}
**Add a new server**

At the bottom of the page is a table showing all the connected MCP servers. To add a new server, click **Add MCP server**
{% endstep %}

{% step %}
**Choose your MCP server**

To add your server you'll need to give it a name, add the URL for the server, and configure the HTTP headers that will be sent along with the request to the server when a user submits a query.
{% endstep %}
{% endstepper %}
