---
description: >-
  Help your users find the information they need faster with powerful knowledge
  discovery tools for your published content
icon: magnifying-glass
---

# Search & GitBook Assistant

<figure><img src="../.gitbook/assets/23_07_25_gitbook_assistant.svg" alt="GitBook Assistant"><figcaption><p>The GitBook Assistant</p></figcaption></figure>

### Choose your site’s search experience

GitBook sites offer different search experiences depending on what you want for your users:

* **Keyword search** – A standard search experience based on keywords. Automatically enabled on all sites.
* **GitBook AI search** – Users get short answers to questions directly from the search box.
* **GitBook Assistant** – Users get an advanced, interactive chat experience with GitBook’s AI agent.

To choose your site’s search experience, open your site’s dashboard, navigate to the **Settings** page and choose **AI & MCP** from the menu on the left. Here you can choose your preferred experience.

<figure><img src="../.gitbook/assets/29_07_25_search_ai.svg" alt=""><figcaption><p>Choose the search experience you want in your published docs</p></figcaption></figure>

{% hint style="warning" %}
When the GitBook Assistant is enabled, AI search is disabled. Standard keyword searches will always provide the results in the search bar no matter which experience you choose.
{% endhint %}

## Searching published documentation

**​**Users can open the **Ask or search…** bar by pressing <kbd>⌘</kbd> + <kbd>K</kbd> on Mac or <kbd>Ctrl</kbd> + <kbd>K</kbd> on PC.

Your users can search for keywords within your docs site and jump quickly to specific pages or page sections across your entire site.

If your docs site has multiple [sections](site-structure/site-sections.md), the search results will contain pages from all of these sections so that you users can jump straight to the page they need.

## GitBook AI search

{% include "../.gitbook/includes/premium-and-ultimate-hint.md" %}

GitBook AI search offers basic AI-powered answers in the **Search and find…** bar of your site. It’s trained on the content of your docs site, but cannot pull in information from external sources.&#x20;

### Using GitBook AI search

If you have enabled GitBook AI search from your site’s settings page, your users can access it by asking a question directly in the **Ask or search…** bar at the top of the page.

They can open this by clicking it directly, or by pressing <kbd>⌘</kbd> + <kbd>K</kbd> on a Mac or <kbd>Ctrl</kbd> + <kbd>K</kbd> on a PC.

As well as a summarized answer, below your users will also see an expandable section that shows the sources that GitBook AI used to create its answer, plus related questions you can click as a follow-up.

{% hint style="warning" %}
GitBook AI does not work across individual published spaces on different [docs sites](publish-a-docs-site/).

Multi-space search is _only_ available when viewing published spaces that live as [site sections](site-structure/site-sections.md) within the same site.&#x20;
{% endhint %}

## GitBook Assistant

{% include "../.gitbook/includes/ultimate-hint.md" %}

GitBook Assistant gives your users fast, accurate answers about your documentation using natural language. It’s embedded right into your docs site, so users can ask questions, request more information about the page they’re on, or get other contextual help.

The Assistant uses agentic retrieval to understand the context of the query based on the user’s current page, previously-read pages, and previous conversations they’ve had.&#x20;

GitBook Assistant is trained on your documentation, but you can also add external sources to expand it’s context and knowledge and give better answers.

{% hint style="info" %}
## Try GitBook Assistant for yourself!

You can try GitBook Assistant for yourself right here in our docs. To get started, click the **Assistant** button next to the **Ask or search…** bar. Here are some ideas to test it out:

* Ask  a simple question about something on this page
* Ask a technical question about our API
* Ask follow-up questions or ask for more details about a specific part of Assistant’s answer
* Ask a question about conversations in our GitHub Community, which we’ve [connected to Assistant using an MCP server](search-and-gitbook-assistant.md#how-do-i-use-gitbook-ai) — something like “What discussions have there been about customization options?”
{% endhint %}

### Using GitBook Assistant <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

Users can access GitBook Assistant in three ways:

* Press <kbd>⌘</kbd> + <kbd>I</kbd> on Mac or <kbd>Ctrl</kbd> + <kbd>I</kbd> on PC
* Click the **GitBook Assistant** <picture><source srcset="../.gitbook/assets/gitbook-assistant-dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/gitbook-assistant.svg" alt=""></picture> button next to the **Ask or search…** bar
* Type a question into the **Ask or search…** bar and choose the ‘Ask…’ option at the top of the menu.

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

## FAQs

#### Integrating GitBook AI with your product

With our API, you can embed GitBook AI into your product or website! This opens up lots of possibilities, including in-app helpers and website chat bots that can respond to questions based on the content in your documentation.

Head to [our developer documentation](https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api/api-reference/docs-sites/site-ai-ask) to find out more.
