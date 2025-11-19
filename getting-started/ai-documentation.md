---
description: >-
  Learn how AI documentation helps your users find answers, your team maintain
  docs efficiently, and your docs be more discoverable by AI tools like ChatGPT
icon: sparkles
---

# AI-native features

Documentation hosted on GitBook benefits from built-in AI features and optimizations out of the box.&#x20;

These AI-native features help your users find the information they need faster — whether they’re asking the built-in AI Assistant trained on your docs, or using other AI tools like ChatGPT. At the same time, they help your team maintain your docs more efficiently, so they’re always accurate and up to date.

## How AI in GitBook improves your documentation <a href="#what-makes-your-documentation-ai-native" id="what-makes-your-documentation-ai-native"></a>

### Help users find information <a href="#reading" id="reading"></a>

As well as just reading your docs, your users can chat with the [AI Assistant](../publishing-documentation/gitbook-ai-assistant/) in your docs to get answers to questions. It’s trained on your documentation and can provide detailed information to help guide users to the solution they need. But you can also [connect it to other tools via MCP](../publishing-documentation/gitbook-ai-assistant/#extend-gitbook-assistant-with-mcp-servers), allowing the Assistant to give answers from more sources, or even carry out actions like opening support tickets or filing bug reports from users.

You can also [embed GitBook Assistant into your product or website](../publishing-documentation/gitbook-ai-assistant/embedding/) to give users access to docs information without having to switch tools.

And you can take this even further by allowing the Assistant to understand what your users are currently working on using [adaptive content](../publishing-documentation/adaptive-content/). By passing data securely between your product and GitBook, Assistant can provide personalized, context-aware answers and even proactively suggest relevant questions.&#x20;

### Maintain docs more efficiently <a href="#writing" id="writing"></a>

GitBook includes [built-in AI tools](../creating-content/write-and-edit-with-ai.md) that help you write, simplify and summarize content in your docs. You can activate these AI tools directly in the editor and quickly write a prompt that you want the AI to follow. You can also use it to review and correct your work.

And if you want to translate your docs site into other languages, all you have to do is choose the language you want. [GitBook’s built-in AI Translation tool](../creating-content/translations.md) will handle the translation, duplicating all your primary content and localizing it ready for you to add to your site. When you update your primary content, the translated versions automatically update to reflect your changes — no effort or review needed.

### Improve docs discovery in ChatGPT and other tools <a href="#discovering" id="discovering"></a>

Your published docs site is [automatically optimized for AI tools](../publishing-documentation/llm-ready-docs.md) and search engines to help users discover your documentation when using tools like ChatGPT, Claude and Google AI Overview.

Your docs site sends pages to AI agents as Markdown rather than HTML, which are easier for AI tools to process and use fewer tokens. And you can view every page as Markdown by adding `.md` to the URL.&#x20;

GitBook also automatically creates `llms.txt` and `llms-full.txt` files for your docs site. These files are becoming industry-standard, and help LLMs index your documentation so they can respond to user questions quickly with relevant answers.

Plus, GitBook [automatically hosts an MCP server](../publishing-documentation/llm-ready-docs.md#mcp-server) for every docs site. This lets users connect their AI tools directly to the information in your docs so they can get the latest, most accurate product information rigt when they need it without needing to switch tools.

## Use GitBook’s AI documentation features <a href="#enable-ai-features" id="enable-ai-features"></a>

Choose a feature below to find out more:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-sparkles">:sparkles:</i></h4></td><td><strong>AI Assistant</strong></td><td>Embed the Assistant in your product and give users relevant answers trained on your docs — and other tools you choose to connect.</td><td><a href="../publishing-documentation/gitbook-ai-assistant/">gitbook-ai-assistant</a></td></tr><tr><td><h4><i class="fa-square-caret-down">:square-caret-down:</i></h4></td><td><strong>Page actions menu</strong></td><td>Every page on your published docs site includes a menu that lets users ask AI tools, connect your docs via MCP and more.</td><td><a href="../publishing-documentation/customization/extra-configuration.md#page-actions">#page-actions</a></td></tr><tr><td><h4><i class="fa-language">:language:</i></h4></td><td><strong>Translations</strong></td><td>Translate your docs into any language with a click, and watch them automatically update every time you edit your primary content.</td><td><a href="../creating-content/translations.md">translations.md</a></td></tr><tr><td><h4><i class="fa-server">:server:</i></h4></td><td><strong>MCP server integration</strong></td><td>Your site’s hosted MCP server lets users connect your docs to other tools so they can pull knowledge whenever they need it.</td><td><a href="../publishing-documentation/mcp-servers-for-published-docs.md">mcp-servers-for-published-docs.md</a></td></tr></tbody></table>
