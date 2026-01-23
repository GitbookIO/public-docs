---
description: >-
  GitBook Assistant offers users answers based on your docs and tailored to
  their situation — not just generic responses
icon: gitbook-assistant
---

# GitBook Assistant

{% include "../.gitbook/includes/ultimate-hint.md" %}

<figure><img src="../.gitbook/assets/25_07_23_gitbook_assistant.svg" alt="GitBook Assistant"><figcaption><p>The GitBook Assistant</p></figcaption></figure>

GitBook Assistant gives your users fast, accurate answers about your documentation using natural language. It's personalized to your users, can be embedded into your website or product, and is available in the sidebar of your published docs.

Think of it as a product expert available to all of your users, in the places and times they need it most.

The Assistant uses agentic retrieval to understand the context of queries based on the user's current page, previously-read pages, and previous conversations.

<p align="center"><a href="https://gitbook.com/docs/publishing-documentation/gitbook-ai-assistant?ask=how+does+the+gitbook+assistant+help+tie+product+knowledge+closer+to+users+in+my+product" class="button primary">Test GitBook Assistant</a></p>

### Enable GitBook Assistant <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

To enable GitBook Assistant, open your site's dashboard, navigate to the **Settings** page and choose **AI & MCP** from the menu on the left. Here you can enable GitBook Assistant from the options available.

#### Add suggested questions

Suggested questions are pre-written prompts shown when the Assistant opens with no active conversation. They help users understand what they can ask, and can help you point your users towards useful answers or workflows.

You can add suggested questions in your site’s settings, under **AI & MCP** from the menu on the left.

**Good suggested questions:**

* Start with a real user goal (setup, troubleshoot, integrate).
* Use the words your users use (avoid internal codenames).
* Keep them specific. “How do I…?” beats “Tell me about…”.
* Cover different intents: quickstart, how-to, troubleshooting, and reference.

{% hint style="info" %}
If you’re embedding the Assistant in your product, you can also dynamically set suggestions in your embed configuration. See [Customizing the Embed](embedding/configuration/customizing-docs-embed.md#adding-suggestions).
{% endhint %}

### Using GitBook Assistant in published docs <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

Users can access GitBook Assistant in three ways:

* Press <kbd>⌘</kbd> + <kbd>I</kbd> on Mac or <kbd>Ctrl</kbd> + <kbd>I</kbd> on PC
*   Click the **GitBook Assistant**

    <picture><source srcset="../.gitbook/assets/25_07_16_gitbook_assistant.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/25_07_16_gitbook_assistant_1.svg" alt=""></picture>

    button next to the **Ask or search…** bar
* Type a question into the **Ask or search…** bar and choose the 'Ask…' option at the top of the menu

{% if visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true %}
**Embed GitBook Assistant in your product**

You can embed GitBook Assistant directly into your product or website, giving users instant access to AI-powered help without leaving your application. The Assistant can be embedded as part of [Docs Embed](embedding/), which includes both the Assistant tab for AI-powered chat and a Docs tab for browsing your documentation.

Choose the embedding method that fits your stack:

* [**Standalone script tag**](embedding/implementation/script.md) – Quick setup with a `<script>` tag
* [**Node.js/NPM**](embedding/implementation/nodejs.md) – Server-side or build-time integration
* [**React component**](embedding/implementation/react.md) – Prebuilt React components

**Additional guides:**

* [Using with authenticated docs](embedding/authentication/using-with-authenticated-docs.md) – Required if your docs need sign-in
* [Customizing the Embed](embedding/configuration/customizing-docs-embed.md) – Welcome messages, actions, and suggestions
* [Creating custom tools](embedding/configuration/creating-custom-tools.md) – Connect Assistant to your APIs
* [API Reference](embedding/configuration/reference.md) – All available methods and events
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
