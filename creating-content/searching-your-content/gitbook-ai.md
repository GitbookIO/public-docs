---
description: GitBook uses AI to help you and your users find the knowledge you need, faster
---

# GitBook AI

When engaging with GitBook AI, you have the ability to ask questions or elaborate on specific requirements. This AI-driven tool is designed to review your documentation in real-time, providing you with quick, direct answers.

{% hint style="info" %}
GitBook AI search is available both within the GitBook app to search internal content, and in published content to search that specific docs site.&#x20;
{% endhint %}

### Enable GitBook AI

#### For published content

{% include "../../.gitbook/includes/premium-and-ultimate-hint.md" %}

You can enable GitBook AI for any published space or collection in that space’s or collection’s [customization settings](../../publishing-documentation/customization/).&#x20;

Click the **Customize** button, then open to the **Configure** tab and toggle the **Enable** **GitBook AI semantic search** setting on.

#### For internal content

{% include "../../.gitbook/includes/pro-and-enterprise-hint.md" %}

You can also enable GitBook AI for your organization’s internal content, allowing you to ask questions and get semantic answers about your internal knowledge base.&#x20;

Head to the **Organization settings** page and, in the **General** tab, toggle the **Enable GitBook AI semantic search** setting on.

### Use GitBook AI <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

Once GitBook AI is enabled, simply type a question into the search bar. GitBook AI will take a few seconds to scan your documentation and summarize the results.

#### For published documentation

{% include "../../.gitbook/includes/premium-and-ultimate-hint.md" %}

Let’s give it a try right here in our own public documentation! Firstly, open the search palette by clicking **Ask or search…** in the top-right corner of the page, or by press **⌘ + K** on a Mac or **Ctrl + K** on a PC.

Then simply type your question and press `Enter`. You’ll see a number of suggested questions that you might like to ask.

For this example, in our own docs, you can try: “What makes change requests a powerful GitBook feature?” After a few seconds, you’ll get an answer from GitBook AI.

As well as a summarized answer, below you’ll also see an expandable section that shows the sources that GitBook AI used to create its answer, plus related questions you can click as a follow-up.

{% hint style="warning" %}
GitBook AI does not work across individual published spaces on different [docs sites](../../publishing-documentation/publish-a-docs-site/).

Multi-space search is _only_ available when viewing published spaces that live as [site sections](../../publishing-documentation/site-structure/site-sections.md) within the same site.&#x20;
{% endhint %}

#### For internal documentation

{% include "../../.gitbook/includes/pro-and-enterprise-hint.md" %}

If GitBook AI is enabled for internal content, you’ll be able to do the same thing when logged into the GitBook app: open the quick find command palette, type a question and receive a semantic answer.

#### Integrating GitBook AI with your product

With our API, you can embed GitBook AI into your product or website! This opens up lots of possibilities, including in-app helpers and website chat bots that can respond to questions based on the content in your documentation.

Head to [our developer documentation](https://docs.gitbook.com/developers/gitbook-api/api-reference/docs-sites/site-ai-ask#post-orgs-organizationid-sites-siteid-ask) to find out more.

#### How long does it take for GitBook AI to index changes?

When someone makes a change to your content — such as a merged [change request](../../collaboration/change-requests.md) or a new [knowledge snippet](../../snippets/snippets-beta.md) from Slack) it can take **up to one hour** for GitBook to index the changes to and reflect them in AI search results.

#### How does GitBook AI handle my data?

We pass your content to OpenAI to index and process data. OpenAI **does not** use this content for service improvements (including model training). You can find out more about how OpenAI handles data [here](https://openai.com/blog/introducing-chatgpt-and-whisper-apis#developer-focus).

#### How do I prevent hallucinations with GitBook AI search?

If you’re seeing GitBook produce answers that are incorrect, the best method for correcting this is write explicit content around the topic so the AI does not have to guess.
