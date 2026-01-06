---
description: >-
  GitBook uses AI to help you find the knowledge you need within your
  organization, faster
---

# GitBook AI

When engaging with GitBook AI, you have the ability to ask questions or elaborate on specific requirements. This AI-driven tool is designed to review your documentation in real-time, providing you with quick, direct answers.

{% hint style="info" %}
GitBook AI search is available both within the GitBook app to search internal content, and [in published content to search that specific docs site](../../publishing-documentation/ai-search.md).&#x20;
{% endhint %}

## GitBook AI helps you find answers in the GitBook app

{% include "../../.gitbook/includes/pro-and-enterprise-hint.md" %}

You can enable GitBook AI for your organization’s internal content, allowing you to ask questions and get semantic answers about your internal knowledge base.&#x20;

Head to the **Organization settings** page and, in the **General** tab, toggle the **Enable GitBook AI** setting on.

### Using GitBook AI search <a href="#how-do-i-use-gitbook-ai" id="how-do-i-use-gitbook-ai"></a>

Once GitBook AI is enabled, open the **Ask or search** <picture><source srcset="../../.gitbook/assets/25_07_16_quick_find_1.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_07_16_quick_find.svg" alt=""></picture> menu from the left sidebar and simply type out a question. GitBook AI will take a few seconds to scan your documentation and summarize the results.

### FAQs

#### How long does it take for GitBook AI to index changes?

When someone makes a change to your content — such as a merged [change request](../../collaboration/change-requests/) — it can take **up to one hour** for GitBook to index the changes to and reflect them in AI search results.

#### How does GitBook AI handle my data?

We pass your content to OpenAI to index and process data. OpenAI **does not** use this content for service improvements (including model training). You can find out more about how OpenAI handles data [here](https://openai.com/blog/introducing-chatgpt-and-whisper-apis#developer-focus).

#### How do I prevent hallucinations with GitBook AI search?

If you’re seeing GitBook produce answers that are incorrect, the best method for correcting this is write explicit content around the topic so the AI does not have to guess.
