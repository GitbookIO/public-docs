---
description: GitBook uses AI to help you find the knowledge you need, faster.
---

# GitBook AI (beta)

{% embed url="https://youtu.be/X-3DAtaK2F8" %}

Simply tell GitBook AI what you want, or ask it a question. It’ll use AI to scan your documentation and give you a simple, semantic answer — with clickable references if you want to dive deeper.

### Which GitBook plans include GitBook AI?

While GitBook AI is in open beta, it is available at no additional cost on **all plans** during that time!

In future, we plan to incorporate GitBook AI into our **Pro and Enterprise plans**, but we’ll let you know before that happens.

### How do I enable GitBook AI?

#### For published content

You can enable GitBook AI for any published space or collection in that space’s or collection’s [customization settings](../../published-documentation/customization/space-customization.md). Click the **customize** button, go to the **configure** tab, and toggle the **enable** GitBook AI **semantic search** setting on.

#### For internal content

You can also enable GitBook AI for your organization’s internal content, allowing you to ask questions and get semantic answers about your internal knowledge base. Head to the **organization settings page** and, on the **general** tab, toggle the **enable** GitBook AI **semantic search** setting on.

### How do I use GitBook AI?

Once GitBook AI is enabled, simply type a question into the search bar. GitBook AI will take a few seconds to scan your documentation and summarize the results.

#### Using GitBook AI in published documentation

Let’s give it a try right here in GitBook’s public documentation! Firstly, open the search command palette. You’ll find it in the top-right corner of the page. You can click on it to open it, or press `⌘+K` on a Mac or `Ctrl+K` on a PC.

Then, click on the GitBook AI tab. You’ll see a number of suggested questions that you might like to ask.

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/gitbook-ai.png" alt=""><figcaption><p>Ask a question with GitBook AI.</p></figcaption></figure>

</div>

For this example, lets try: "What makes change requests a powerful GitBook feature?" After a few seconds, you’ll get an answer from GitBook AI!

#### Using GitBook AI in internal documentation

If GitBook AI is enabled for internal content, you’ll be able to do the same thing when logged into the GitBook app: open the quick find command palette, click on the GitBook AI tab, type a question and receive a semantic answer.

#### Integrating GitBook AI with your product

With our API, you can embed GitBook AI into your product or website! This opens up lots of possibilities, including in-app helpers and website chat bots that can respond to questions based on the content in your documentation.

[Take a look at our developer documentation](https://developer.gitbook.com/gitbook-api/reference/search#get-ai-search-results-from-all-spaces-for-the-currently-authenticated-user).

#### How long does it take for changes to be indexed by GitBook AI?

When a change is made to your content (a merged change request or a new Slack knowledge snippet) it can take **up to one hour** for the new changes to be indexed by GitBook and reflected in AI search results.

#### How does GitBook AI handle my data?

We pass your content to OpenAI to index and process data. OpenAI **does not** use this content for service improvements (including model training). You can find out more about how OpenAI handles data [here](https://openai.com/blog/introducing-chatgpt-and-whisper-apis#developer-focus).

#### How do I prevent hallucinations with GitBook AI search?

If you're seeing GitBook produce answers that are incorrect, the best method for correcting this is write explicit content around the topic so the AI does not have to guess.
