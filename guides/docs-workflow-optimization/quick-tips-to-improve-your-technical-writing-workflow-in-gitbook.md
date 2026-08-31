---
description: >-
  10 practical GitBook tips for technical writers to ship better docs faster —
  including Markdown, keyboard shortcuts, integrations, Git Sync and more
---

# 10 quick tips to improve your technical writing workflow in GitBook

Your technical documentation probably already contains the right information. Nice work! Now it’s time to make it faster to maintain and easier to consume.

And with GitBook, there are a few simple ways to improve your workflow and speed things up. That includes links, blocks, and two-way sync with GitHub or GitLab.

This post shares 10 tips you can apply today. Each one saves time and improves clarity.

### Quick takeaways

* Use Markdown and keyboard shortcuts to write faster.
* Use `/` to add blocks and inline content without leaving the keyboard.
* Use relative links, descriptive captions, and alt text for accessibility and crawlability.
* Use GitBook Agent for writing and reviewing.
* Add integrations to bring your tooling into your docs.
* Use Git Sync to keep docs and repos aligned, in both directions.

### Use Markdown to write faster <a href="#use-markdown-to-write-faster" id="use-markdown-to-write-faster"></a>

Yes, you can certainly write into the GitBook editor in plain text. But it also supports Markdown as a keyboard-friendly way to format your content and add blocks fast.

GitBook supports basic formatting, including **bold** and _italic_. But you can also add H1, H2 and H3 titles using hashes (`#`) at the start of a new block, add code and quote blocks, and create lists with a few keystrokes.

_New to Markdown? We’ve got your back. Many other tools outside GitBook support it — so learning it now will likely prove useful in other places. You can learn more about our Markdown support_ [_in our documentation_](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/formatting/markdown)_, and explore Markdown itself in more detail over at_ [_CommonMark_](https://commonmark.org/)_._

### Learn some handy keyboard shortcuts <a href="#learn-some-handy-keyboard-shortcuts" id="learn-some-handy-keyboard-shortcuts"></a>

Okay, so you’re a Markdown master. In that case, here are some quick keyboard shortcuts that will speed up the tiny tasks you carry out multiple times every day. Below, we’ve chosen a few of our most-used shortcuts to get you started. You can head [to our documentation](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/reference/keyboard-shortcuts) to explore the full list.

<kbd>⌘</kbd> + <kbd>K</kbd> (Mac) or <kbd>Ctrl</kbd> + <kbd>K</kbd> (Windows) — Open the **Ask or search** panel

<kbd>⌘</kbd> + <kbd>Enter</kbd> (Mac) or <kbd>Ctrl</kbd> + <kbd>Enter</kbd> (Windows) — Exit from content block (code, tabs, table, quote, etc)

<kbd>Esc</kbd> — Select the entire active block (or multiple active blocks)

<kbd>⌘</kbd> + <kbd>⌥</kbd> + <kbd>0</kbd> / <kbd>1</kbd> / <kbd>2</kbd> /<kbd>3</kbd> — Turn text into a paragraph/heading 1/heading 2/heading 3 block

### Add and change blocks fast <a href="#add-and-change-blocks-fast" id="add-and-change-blocks-fast"></a>

There’s one keyboard shortcut we didn’t list above, because we think it’s important enough to deserve its own section. Hitting <kbd>/</kbd> opens the [block-insert palette](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/blocks#inserting-a-new-content-block) — and unlocks a whole selection of possibilities for your content.

Use it on a new, empty block and you can select from the full list of blocks in GitBook, plus any integrations you’ve added. You can scroll through the list, or type to narrow it down.

Alternatively, use <kbd>⌘</kbd> + <kbd>/</kbd> or <kbd>Ctrl</kbd> + <kbd>/</kbd> on a block you’re editing — whatever its type. This opens a context menu for that block.

In a text block, you can switch between paragraph and heading. In [a code block](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/blocks/code-block), you can set syntax, add line numbers, and more.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2F4Jiwi9cm2XZEvFLJtulz%2Fcode-block.mp4?alt=media&token=72bd7161-c0f0-4511-8334-d398336fa1d4?autoplay=1" %}
Add and update blocks using the block insert menu.
{% endembed %}

Try it on different blocks and explore the options. It’s one of the fastest ways to edit in GitBook.

### Add inline content <a href="#add-inline-content" id="add-inline-content"></a>

Using the block-insert palette isn’t the only way to add content to your pages fast, though. When typing in a text block, you can hit <kbd>/</kbd> at any time to open [the inline palette](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/formatting/inline).

The inline palette lets you add an image, [button](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/formatting/inline#buttons), emoji, link, math & TeX, icon or expression. It’s the fastest way to add common elements without context switching.

<figure><img src="../.gitbook/assets/inline-palette@2x.png" alt="The GitBook inline palette for inserting images, emoji, links, and math"><figcaption><p>Add inline content directly in your page.</p></figcaption></figure>

{% hint style="info" %}
**Tip:** Alternatively, you can add emoji by typing `:` followed by the name of the emoji you want to add 👍
{% endhint %}

### Select and move blocks <a href="#select-and-move-blocks" id="select-and-move-blocks"></a>

One shortcut we did list above, but bears repeating, is the option to select a whole block or blocks — simply by hitting the `Esc` key. This is great for reorganizing content within your page, as you can drag multiple blocks around at once, or use commands like cut, copy, paste and delete to manage your content.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2FASqYAgNxI2JT1EnRmC6k%2Fblock-selection.mp4?alt=media&token=1fb80dc2-688b-4148-b95c-fe550d0369c6?autoplay=1" %}
Select and move blocks.
{% endembed %}

### Use GitBook Agent to write or review  <a href="#add-email-address-links-using-mailto" id="add-email-address-links-using-mailto"></a>

GitBook includes [a built-in AI Agent](/broken/spaces/NkEGS7hzeqa35sMXQZ4X/pages/KHHFlE1MtpVIaZboN8b2) that can write content for you based on a prompt — or review your changes before they go live.

The best part? The Agent can understand and follow your style guide. So not only does it find and fix spelling and grammar mistakes — it can also tell you when you’ve deviated from your standard style.

You can open a chat with the GitBook Agent in any change request by hitting the **GitBook Agent** <picture><source srcset="../.gitbook/assets/gitbook-agent-dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/gitbook-agent-light.svg" alt=""></picture>button in the space header bar, or open a comment and tagging **@gitbook** to call it.

And to [get the Agent to review your work](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/gitbook-agent/review-change-requests-with-gitbook-agent), click **Request a review** and simply add the Agent as a reviewer — it’ll comment on your page directly.

### Use relative links <a href="#use-relative-links" id="use-relative-links"></a>

Relative links in GitBook are the best way to link to other parts of your documentation. Why? Because if someone changes the URL, name, or location of the linked content, GitBook will still keep its reference up to date. And that means fewer broken links — and better [documentation SEO](../seo-and-llm-optimization/how-to-use-seo-techniques-to-improve-your-documentation.md) and [AI optimization](../seo-and-llm-optimization/geo-guide.md).

If your technical documentation is published, you can link to anchors, other pages or even other [sections](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/site-structure/site-sections) on your docs site.&#x20;

You add them like any other link. Highlight the text, click the link button on the inline palette, or hit <kbd>⌘</kbd> + <kbd>K</kbd> / <kbd>Ctrl</kbd> + <kbd>K</kbd>. Then type the name of the anchor, page, or space you want to link to.

<figure><img src="../.gitbook/assets/relative-links@2x.png" alt="Adding a relative link to another GitBook page using the link picker"><figcaption><p>Add relative links to other pages in your documentation.</p></figcaption></figure>

### Change the hint color and icon with a click <a href="#change-the-hint-color-and-icon-with-a-click" id="change-the-hint-color-and-icon-with-a-click"></a>

We’re sure you know that [hint blocks](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/blocks/hint) have four different colors and styles that you can choose from, to match the kind of content inside. What you may not know is that you can quickly cycle through the different styles simply by clicking the icon in the block itself. There are four to choose from — and it saves you opening the menu to change it!

{% hint style="info" %}
**Bonus tip:** If you’ve published your documentation, you can control the color of your hint blocks (and code blocks) by [customizing the semantic colors](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/customization/icons-colors-and-themes) for your site.
{% endhint %}

### Add integrations <a href="#add-integrations" id="add-integrations"></a>

While there are plenty of built-in tools that will make your life with GitBook easier, you shouldn’t stop there. We have a whole host of integrations that you can add to improve your workflows — and your technical documentation.

From adding extra [analytics tools](https://www.gitbook.com/integrations/googleanalytics) to embedding [Linear issues](https://www.gitbook.com/integrations/linear), [Mermaid diagrams](https://www.gitbook.com/integrations/mermaid) and [RunKit notebooks](https://www.gitbook.com/integrations/runkit), you’ll find plenty of ways to supercharge your technical docs and get extra features with just a few clicks.

Take a look at [all our integrations](https://www.gitbook.com/integrations), and see how you can [build your own](/broken/spaces/2SyQSbIa1iYS7z6Dx5di/pages/NOEnejpO7KQZo2RcdYWI).

### Set up Git Sync <a href="#set-up-git-sync" id="set-up-git-sync"></a>

This last entry is a big one — and if you haven‘t set it up already, it could save you hours of work in the long-run.

[Git Sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync) lets technical teams synchronize GitHub or GitLab repositories with GitBook — and turn existing Markdown files into beautiful, user-friendly technical documentation. And when you edit that content in GitBook, Git Sync will automatically update your codebase in GitHub or GitLab to keep everything in sync.

Best of all, Git Sync is two-way — so if you merge a pull request in GitHub or GitLab, that change will also appear automatically in GitBook. How handy is that?

Once you’ve set up the sync, your whole team can contribute to your technical documentation — and your wider knowledge base — no matter which tool they prefer to use.

Find out how to get set up [in our documentation](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync).

***

### FAQ: technical writing workflow in GitBook

#### What’s the fastest way to format docs in GitBook?

Use Markdown for headings, lists, code, and emphasis. Pair it with keyboard shortcuts for repeat actions.

#### How do I add blocks without using the mouse?

Type <kbd>/</kbd> on a new line to open the block insert menu. Use <kbd>⌘</kbd> + <kbd>/</kbd> or <kbd>Ctrl</kbd> + <kbd>/</kbd> to edit the current block type.

#### When should I use relative links?

Use relative links for anything inside GitBook. They stay valid when pages move or get renamed.

#### How do I make my docs easier for AI tools to cite?

Use descriptive headings, short sections, and explicit definitions. Add alt text and captions for images.

#### How do I keep docs in sync with my repo?

Use Git Sync for two-way sync with GitHub or GitLab. That keeps Markdown and GitBook content aligned.

### Related reading

[**→ How to use SEO techniques to improve your documentation**](../seo-and-llm-optimization/how-to-use-seo-techniques-to-improve-your-documentation.md)

[**→ GEO guide: How to optimize your docs for AI search and LLM ingestion**](../seo-and-llm-optimization/geo-guide.md)

[**→ 7 tips to improve your public docs**](7-ways-to-make-your-public-documentation-more-useful-for-users.md)
