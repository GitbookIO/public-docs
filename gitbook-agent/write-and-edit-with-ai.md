---
description: Use GitBook Agent to generate and build content for your page
icon: wand-magic-sparkles
---

# Writing with GitBook Agent

GitBook Agent is a powerful tool for generating content for your documentation in GitBook.

The Agent can do everything from write small sections of text on your page, to edit existing blocks and create new pages, sections and more in a change request.

{% hint style="info" %}
## GitBook Agent follows your style guide

You can [add your own style guide and custom instructions](what-is-gitbook-agent.md#add-a-style-guide-and-custom-instructions) at an organization level — so the Agent will always match your tone and style whenever you ask it to help.
{% endhint %}

### What can GitBook Agent do?

GitBook Agent is deeply integrated into the GitBook app, so it understands the blocks you can create in the editor, and the wider content of your space.&#x20;

That means you can use the Agent to:

* Write new content based on your prompts
* Search through existing pages and update specific content
* Reformat content to make the most of GitBook’s different blocks
* Update code samples
* Move content around between pages
* Add new pages in specific locations

### How to interact with GitBook Agent

There are a few ways to work with GitBook Agent:

* Open the Agent within an existing change request and tell it what you need
* Plan and implement a new change request with GitBook Agent
* Tag the Agent in a comment on a block
* Create new content on an empty line on your page

Let’s run through each of these to find out how they work.

#### Open GitBook Agent chat window in any change request

You can open the Agent chat window in a change request at any time by hitting the **GitBook Agent** button in the space header bar. This will open the Agent’s chat window on the right of the app.

<div data-with-frame="true"><figure><img src="../.gitbook/assets/CleanShot 2025-12-08 at 21.41.29@2x.png" alt=""><figcaption><p>Open GitBook Agent in a change request</p></figcaption></figure></div>

Here you can write a prompt for the Agent to follow — it will explain what it’s doing as it follows your instructions, with the changes appearing in your space is it works.&#x20;

You can give follow-up instructions or clarify steps, or edit the content of your space directly at any point, allowing you to work alongside GitBook Agent.&#x20;

#### Implement a change request with GitBook Agent

Click the **GitBook Agent** section of the **Edit** button in the top-right of a space to open a modal.

Here you can write a prompt to tell the Agent what you want your change request to include, then add reference pages that might be useful as context for the changes.

Once you click **Start change request** the Agent will open a change request for you and start carrying out your instructions. At every stage, the Agent will tell you what it’s doing in the chat window on the right-hand side of the app.&#x20;

When it’s done, you can edit the content yourself directly on the page, or give the Agent more instructions to continue refining your changes.&#x20;

#### Tag GitBook Agent in a comment

If you want the Agent to review a specific block on your page, you can tag it in a comment and tell it what you need. Simply click **Comment on block** and tag @gitbook to tag the Agent, then tell it what you want it to do.

GitBook Agent will update the content based on your prompt, then reply to your comment telling you what it did.

#### Create new content in an empty block

{% include "../.gitbook/includes/pro-and-enterprise-hint.md" %}

You can use GitBook Agent to create content on any empty line on your page. It can create all kinds of content — formatted in Markdown — including code samples, templates, page summaries and more.

<figure><img src="../.gitbook/assets/Write with AI@2x.png" alt="A GitBook screenshot showing the AI writing options"><figcaption><p>Write with GitBook AI.</p></figcaption></figure>

Press `Space` on any empty line, or type `/` and choose **Write with AI** to launch GitBook Agent.

You can instantly start typing any prompt you want. GitBook Agent will analyze the prompt and generate content based on it. For example:

> Write me a two-paragraph overview explaining why documentation is important for product teams.

Alternatively, you can choose from one of the suggested prompts or prompt starters:

* **Continue writing** – GitBook Agent will analyze the content on your current page and then generate more content based on that.
* **Explain…** – Choose this, then tell GitBook Agent what you want it to explain. This isn’t limited by content on your page, so you can ask it to explain anything at all.
* **Summarize** – Summarize all the content on your page. This is great for writing a TL;DR at the bottom of a detailed document, or adding a quick summary at the top for people just checking in.
* **Explain this** – This will explain the complex information on your page in simpler language — including explaining acronyms and other jargon. This is perfect if the page you’re reading involves a lot of complex information, or you want to add an explainer for less technical folks.
* **Translate** – Translate your current page into one of a set number of languages. If you want to translate into a language that’s not on the list, simply type it into the prompt box.

### Write effective prompts for GitBook Agent <a href="#write-effective-prompts" id="write-effective-prompts"></a>

GitBook Agent is like a teammate that’s great at taking directions. You need to give it clear instructions and context to get the best results from it.

Here are some quick tips for writing good prompts:

* **Break it down** – The Agent is best at completing focused tasks. Break down complex projects into smaller steps and ask the Agent to complete them one at a time.
* **Be specific** – Generic prompts like `@gitbook improve this page` will apply general best practices, but without more specific guidance the Agent may not achieve the goal you had in mind.
* **Focus on outcomes** – If you’re hearing about a specific problem customers are having, tell the Agent about those problems — or the outcomes you want to achieve. It will suggest improvements based on those outcomes.
* **Give direct instructions** – If you want the Agent to use a stepper block for a step-by-step guide, or add an FAQ section with a bunch of expandable blocks, tell it precisely what to do to get the right results first time.
* **Use broad prompts for wider improvements** – For maintenance tasks like fixing typos, updating a feature name across pages or removing specific block types from your docs, you can use commands like `@gitbook replace all instances of v2.3.9 with v2.4.0`.
