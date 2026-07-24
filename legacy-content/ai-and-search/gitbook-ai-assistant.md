---
description: >-
  GitBook Assistant gives users accurate, contextual answers drawn from your
  entire knowledge base — not just your docs
icon: gitbook-assistant
---

# GitBook Assistant

{% include "../.gitbook/includes/ultimate-hint.md" %}

<figure><img src="../.gitbook/assets/25_03_31_gitbook_assistant@2x.png" alt="GitBook Assistant"><figcaption><p>The GitBook Assistant</p></figcaption></figure>

GitBook Assistant gives your users fast, accurate answers about your documentation using natural language. It's personalized to your users, can be embedded into your website or product, and is available in the sidebar of your published docs.

Think of it as a product expert available to all of your users, in the places and times they need it most.

The Assistant uses agentic retrieval to understand the context of queries based on the user's current page, previously-read pages, and previous conversations.

Try asking the Assistant a question in the box below:

<p align="center"><button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">Ask a question...</button></p>

## Enable GitBook Assistant <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

To enable GitBook Assistant, open **Customize**, under **Tools** in the site sidebar, and click **AI Assistant**. Here you can enable GitBook Assistant from the options available.

### Add suggested questions

Suggested questions are pre-written prompts shown when the Assistant opens with no active conversation. They help users understand what they can ask, and can help you point your users towards useful answers or workflows.

You can add suggested questions in your site’s **Settings**, under the **AI & MCP** section.

#### **Best practices for suggested questions:**

* Start with a real user goal (setup, troubleshoot, integrate).
* Use the words your users use (avoid internal codenames).
* Keep them specific. “How do I…?” beats “Tell me about…”.
* Cover different intents: quickstart, how-to, troubleshooting, and reference.

{% hint style="info" %}
If you’re embedding the Assistant in your product, you can also dynamically set suggestions in your embed configuration. See [Customizing the Embed](../docs-site/embedding/configuration/customizing-docs-embed.md#adding-suggestions).
{% endhint %}

## Using GitBook Assistant in published docs <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

Users can access GitBook Assistant in three ways:

* Press <kbd>⌘</kbd> + <kbd>I</kbd> on Mac or <kbd>Ctrl</kbd> + <kbd>I</kbd> on PC
* Click the **GitBook Assistant** <picture><source srcset="../.gitbook/assets/25_07_16_gitbook_assistant.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/25_07_16_gitbook_assistant_1.svg" alt=""></picture> button next to the **Ask or search…** bar
* Type a question into the **Ask or search…** bar and choose the 'Ask…' option at the top of the menu

## Embed GitBook Assistant in your product

You can embed GitBook Assistant directly into your product or website, giving users instant access to AI-powered help without leaving your application. The Assistant can be embedded as part of [Docs Embed](../docs-site/embedding/), which includes the Assistant tab for AI-powered chat, the Search tab for scoped discovery, and the Docs tab for browsing your documentation.

Choose the embedding method that fits your stack:

* [**Standalone script tag**](../docs-site/embedding/implementation/script.md) – Quick setup with a `<script>` tag
* [**Node.js/NPM**](../docs-site/embedding/implementation/nodejs.md) – Server-side or build-time integration
* [**React component**](../docs-site/embedding/implementation/react.md) – Prebuilt React components

### Additional Assistant embedding guides:

* [Using embedded Assistant with authenticated docs](../docs-site/embedding/using-with-authenticated-docs.md) – Required if your docs need sign-in
* [Customizing the Assistant embed](../docs-site/embedding/configuration/customizing-docs-embed.md) – Welcome messages, actions, and suggestions
* [Creating custom embed tools](../docs-site/embedding/configuration/creating-custom-tools.md) – Connect Assistant to your APIs
* [API reference](../docs-site/embedding/configuration/reference.md) – All available methods and events

## Extend GitBook Assistant’s knowledge

GitBook Assistant can use external knowledge through [connections](connections/) and [MCP servers](../publishing-documentation/mcp-servers-for-published-docs.md).

You can use connections when you want GitBook to sync records into your site, or use MCP servers when you want to hook up GitBook Assistant to custom tools.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th>Best for</th></tr></thead><tbody><tr><td><strong>Connections</strong></td><td><p>Connections work best for content-heavy sources:</p><ul><li>GitHub issues and discussions</li><li>Slack or Discord conversations</li><li>Support content</li><li>External docs, help centers, and websites</li></ul></td></tr><tr><td><strong>MCP servers</strong></td><td><p>MCP servers work best for live tools and data:</p><ul><li>Current account or product state</li><li>Internal systems that change often</li><li>Actions like creating tickets or filing bugs</li><li>Sources you don't want to sync into GitBook</li></ul></td></tr></tbody></table>

{% tabs %}
{% tab title="Add a connection" %}
{% stepper %}
{% step %}
**Open your site's settings**

Open your site dashboard. Then choose **Settings** → **Connections**.
{% endstep %}

{% step %}
**Connect a source**

Choose a source type. Then authorize it, or enter the URL to import.
{% endstep %}

{% step %}
**Expose records to GitBook Assistant**

Turn on **Expose in search / assistant** for the connection.

GitBook can then use those records in search and GitBook Assistant.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Add an MCP server" %}
{% stepper %}
{% step %}
**Open your site's settings**

Open your site dashboard. Then choose **Settings** → **AI & MCP**.
{% endstep %}

{% step %}
**Add a new server**

In the MCP servers table, click **Add MCP server**.
{% endstep %}

{% step %}
**Enter the server details**

Give the server a name. Add its URL.

Then configure any HTTP headers GitBook must send with each request.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}
