---
description: >-
  Learn how AI documentation helps your users find answers, your team maintain
  docs efficiently, and your docs be more discoverable by AI tools like ChatGPT
icon: sparkles
---

# AI-native documentation

Documentation hosted on GitBook benefits from built-in AI features and optimizations out of the box.

These AI-native features help your users find the information they need faster — whether they’re asking the built-in AI Assistant trained on your docs, or using other AI tools like ChatGPT. At the same time, they help your team maintain your docs more efficiently, so they’re always accurate and up to date.

## How AI in GitBook improves your documentation <a href="#what-makes-your-documentation-ai-native" id="what-makes-your-documentation-ai-native"></a>

### Help users find information <a href="#reading" id="reading"></a>

As well as just reading your docs, your users can chat with the [AI Assistant](../publishing-documentation/gitbook-ai-assistant.md) in your docs to get answers to questions. It's trained on your documentation and can provide detailed information to help guide users to the solution they need. But you can also [connect it to other tools via MCP](../publishing-documentation/gitbook-ai-assistant.md#extend-gitbook-assistant-with-mcp-servers), allowing the Assistant to give answers from more sources, or even carry out actions like opening support tickets or filing bug reports from users.

You can also [embed your GitBook docs into your product or website](../publishing-documentation/embedding/) using Docs Embed, which includes both the Assistant and a docs browser, giving users access to documentation without having to switch tools.

And you can take this even further by allowing the Assistant to understand what your users are currently working on using [adaptive content](../publishing-documentation/adaptive-content/). By passing data securely between your product and GitBook, Assistant can provide personalized, context-aware answers and even proactively suggest relevant questions.

### Maintain docs more efficiently <a href="#writing" id="writing"></a>

[GitBook Agent](/broken/pages/KHHFlE1MtpVIaZboN8b2) helps you write and maintain your documentation — and you can use to create and auto-update localized versions of your docs with a click.

GitBook Agent will create content based on your prompts, allowing you to jumpstart your docs process with a first draft to review. Or you can ask the Agent to review your own work before you merge.

You can add a style guide and custom instructions that apply across your organization, reference other pages to add context, and ask for help on individual blocks — or your entire page.

And soon, the Agent will suggest and generate docs improvements based on support tickets, GitHub issues and other connected services. You’ll be able to browse through it’s suggestions, review the change requests it opens and edit or merge them if they’re useful.

If you prefer to edit your GitBook docs locally using [Git Sync](git-sync/) and AI coding assistants like Claude Code and Cursor, you can also use GitBook's [skill.md](https://gitbook.com/docs/skill.md) file to provide all of the needed context to create, edit, and manage your documentation in your own environment using all of GitBook’s features and blocks.

And if you want to translate your docs site into other languages, all you have to do is choose the language you want. [GitBook’s built-in AI Translation tool](../gitbook-agent/translations.md) will handle the translation, duplicating all your primary content and localizing it ready for you to add to your site. When you update your primary content, the translated versions automatically update to reflect your changes — no effort or review needed.

### Improve docs discovery in ChatGPT and other tools <a href="#discovering" id="discovering"></a>

Your published docs site is [automatically optimized for AI tools](../publishing-documentation/llm-ready-docs.md) and search engines to help users discover your documentation when using tools like ChatGPT, Claude and Google AI Overview.

Your docs site sends pages to AI agents as Markdown rather than HTML, which are easier for AI tools to process and use fewer tokens. And you can view every page as Markdown by adding `.md` to the URL.

GitBook also automatically creates `llms.txt` and `llms-full.txt` files for your docs site. These files are becoming industry-standard, and help LLMs index your documentation so they can respond to user questions quickly with relevant answers.

Plus, GitBook [automatically hosts an MCP server](../publishing-documentation/llm-ready-docs.md#mcp-server) for every docs site. This lets users connect their AI tools directly to the information in your docs so they can get the latest, most accurate product information rigt when they need it without needing to switch tools.

## Use GitBook’s AI documentation features <a href="#enable-ai-features" id="enable-ai-features"></a>

Choose a feature below to find out more:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-sparkles">:sparkles:</i></h4></td><td><strong>AI Assistant</strong></td><td>Embed the Assistant in your product and give users relevant answers trained on your docs — and other tools you choose to connect.</td><td><a href="../publishing-documentation/gitbook-ai-assistant.md">gitbook-ai-assistant.md</a></td></tr><tr><td><h4><i class="fa-robot">:robot:</i></h4></td><td><strong>GitBook Agent</strong></td><td>Get proactive suggestions for docs updates based on support tickets, release notes and more — or ask the Agent to review your work.</td><td><a href="/broken/pages/KHHFlE1MtpVIaZboN8b2">Broken link</a></td></tr><tr><td><h4><i class="fa-language">:language:</i></h4></td><td><strong>Translations</strong></td><td>Translate your docs into any language with a click, and watch them automatically update every time you edit your primary content.</td><td><a href="../gitbook-agent/translations.md">translations.md</a></td></tr><tr><td><h4><i class="fa-server">:server:</i></h4></td><td><strong>MCP server integration</strong></td><td>Your site’s hosted MCP server lets users connect your docs to other tools so they can pull knowledge whenever they need it.</td><td><a href="../publishing-documentation/mcp-servers-for-published-docs.md">mcp-servers-for-published-docs.md</a></td></tr></tbody></table>
