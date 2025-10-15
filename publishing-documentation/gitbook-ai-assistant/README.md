---
description: >-
  GitBook Assistant offers users answers based on your docs and tailored to
  their situation — not just generic responses
icon: messages
---

# GitBook Assistant

{% include "../../.gitbook/includes/ultimate-hint.md" %}

<figure><img src="../../.gitbook/assets/23_07_25_gitbook_assistant.svg" alt="GitBook Assistant"><figcaption><p>The GitBook Assistant</p></figcaption></figure>

GitBook Assistant gives your users fast, accurate answers about your documentation using natural language. It’s personalized on your users, can be embedded into your website or product, and available in the sidebar of your docs.

Think of it as a product expert available to all of your users, in the places and times they need it most.

The Assistant uses agentic retrieval to understand the context of the query based on the user’s current page, previously-read pages, and previous conversations they’ve had.&#x20;

GitBook Assistant is trained on your documentation, but you can also add external sources to expand it’s context and knowledge and give better answers.

<p align="center"><a href="https://gitbook.com/docs/publishing-documentation/gitbook-ai-assistant?ask=how+does+the+gitbook+assistant+help+tie+product+knowledge+closer+to+users+in+my+product" class="button primary">Test GitBook Assistant</a></p>

### Using GitBook Assistant in published docs <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

Users can access GitBook Assistant in three ways:

* Press <kbd>⌘</kbd> + <kbd>I</kbd> on Mac or <kbd>Ctrl</kbd> + <kbd>I</kbd> on PC
* Click the **GitBook Assistant** <picture><source srcset="../../.gitbook/assets/gitbook-assistant-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/gitbook-assistant.svg" alt=""></picture> button next to the **Ask or search…** bar
* Type a question into the **Ask or search…** bar and choose the ‘Ask…’ option at the top of the menu.

{% if visitor.claims.unsigned.bucket.EMBED_ASSISTANT_PANEL == true || visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true %}
### Add GitBook Assistant to your website or app

You can embed GitBook Assistant to help you bring your product and product knowledge closer together.

With GitBook Assistant embedded into your website or app, your users can access knowledge from your docs and [connected tools](./#extend-gitbook-assistant-with-mcp-servers) with a click. This is ideal for offering onboarding help, product suggestions when they get stuck, and contextual solutions tailored to each user.

You can also customize GitBook Assistant in many ways, including configuring custom tools to seamlessly integrate the assistant alongside your product.

Head to [our embedding guide](adding-gitbook-assistant-to-your-website-or-app.md) to learn more about adding the Assistant to your product.
{% endif %}

### Extend GitBook Assistant with MCP servers

You can also choose to add external data sources to GitBook Assistant to give it more context and data to pull answers from. You can do this by connecting Assistant to MCP servers for external platforms, such as:

* Your community (Slack, Discord, GitHub Communities etc)
* Support tools (Intercom etc)
* Your future product roadmap (GitHub, Linear etc)
* Docs for external integrations with products

To add an MCP server to GitBook Assistant, follow these steps:

{% stepper %}
{% step %}
#### Open your site’s settings

Navigate to your site dashboard and choose the **Settings** option from the site header. Then choose the **AI & MCP** section from the left-hand menu
{% endstep %}

{% step %}
#### Add a new server

At the bottom of the page is a table showing all the connected MCP servers. To add a new server, click **Add MCP server**
{% endstep %}

{% step %}
#### Choose your MCP server

To add your server you’ll need to give it a name, add the URL for the server, and configure the HTTP headers that will be sent along with the request to the server when a user submits a query.
{% endstep %}
{% endstepper %}
