---
description: Have GitBook Agent draft and edit content for you.
---

# Write and edit with Agent

GitBook Agent can write short passages, edit existing blocks, or create new pages and more inside a change request.

{% hint style="info" %}
**Agent follows your style guide.** Define your team's writing rules in a [style guide](style-guide.md), and Agent treats it as the source of truth — it loads the style guide's first page into context on every task, so keep your main rules there. You can also add short [custom instructions](README.md#add-a-style-guide-and-custom-instructions) at the site level.
{% endhint %}

### What can GitBook Agent do?

Agent is deeply integrated into the GitBook app, so it understands the blocks available in the editor and the wider content of your section. Use it to:

* Write new content based on your prompts.
* Search existing pages and update specific content.
* Reformat content to make the most of GitBook's blocks.
* Update code samples.
* Move content between pages.
* Add new pages in specific locations.

### How to interact with GitBook Agent

**Open the chat window in any change request.** Click **GitBook Agent** in the section header bar to open its chat window on the right. Write a prompt — it explains what it's doing as it follows your instructions, with changes appearing in your section as it works. Give follow-up instructions, or edit the content directly at any point, working alongside it.

**Implement a change request with Agent.** Click the **GitBook Agent** part of the **Edit** button, top-right of a section. Write a prompt describing what your change request should include, add reference pages as context, and click **Start change request** — Agent opens the change request and starts working, narrating each step in the chat window. When it's done, edit the content yourself, or give it more instructions to keep refining.

**Tag Agent in a comment.** To have it review a specific block, click **Comment on block**, type `@gitbook`, and describe what you need. It updates the content and replies telling you what it did.

**Use the Improve menu.** Hover over the page title, or open the page's Actions menu, to access presets for common improvements:

* Add an icon for the page
* Generate a page description based on its content
* Fix spelling and grammar
* Rewrite for consistency with other pages
* Optimize for SEO
* Add a summary and next steps section
* Link to related topics and pages
* Divide the page into multiple pages

The first two options are conditional — they only show if the page doesn't already have an icon or description. Click any option and Agent gets to work immediately.

**Create new content in an empty block.** Press `Space` on any empty line, or type `/` and choose **Write with AI**. Type any prompt — for example, "Write me a two-paragraph overview explaining why documentation is important for product teams" — or choose a suggested prompt:

* **Continue writing** — generates more content based on the current page.
* **Explain…** — explains anything you ask, not limited to page content.
* **Summarize** — summarizes the page, good for a TL;DR at the top or bottom.
* **Explain this** — rewrites complex information in simpler language, including acronyms and jargon.
* **Translate** — translates the current page into one of several languages, or type a language not on the list.

### Write effective prompts for GitBook Agent

Agent is like a teammate that's great at taking direction — clear instructions and context get the best results:

* **Break it down** — it's best at focused tasks; split complex projects into smaller steps.
* **Be specific** — generic prompts like `@gitbook improve this page` apply general best practices, but won't necessarily hit your specific goal.
* **Focus on outcomes** — tell it about specific customer problems or the outcomes you want, and it suggests improvements based on those.
* **Give direct instructions** — if you want a stepper block, or an FAQ section with expandable blocks, say so explicitly to get the right result the first time.
* **Use broad prompts for wider improvements** — for maintenance tasks like fixing typos or renaming a feature across pages, use commands like `@gitbook replace all instances of v2.3.9 with v2.4.0`.
