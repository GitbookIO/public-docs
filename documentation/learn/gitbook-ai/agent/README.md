---
description: GitBook Agent writes, edits, reviews, and audits your documentation.
---

# GitBook Agent

GitBook Agent is an AI teammate that works alongside you to keep your documentation accurate, complete, and current. It's deeply integrated into GitBook, so you don't need new workflows to use it.

{% hint style="info" %}
Editing your docs locally with an AI coding assistant instead? Use GitBook's skill.md file — see Build with AI → GitBook Skills.
{% endhint %}

### What can GitBook Agent do?

* **Write docs based on a prompt** — ask it to update a page, rename a product, or make any other change. See [Write and edit with Agent](write-and-edit.md).
* **Import content into GitBook** — attach files like PDFs and Word documents in the Agent chat sidebar, and it extracts and formats them into pages.
* **Plan and implement bigger changes** — describe what you need, and it opens a change request, explains its edits, responds to feedback, and implements the plan you build together.
* **Follow your style guide** — define your team's writing rules in a [style guide](style-guide.md), and Agent treats it as the source of truth when writing or reviewing.
* **Follow custom, site-level instructions** — give it site-specific direction, like how to add links or which block types to avoid.
* **Translate your documentation** — choose content and a language, and it localizes your docs. See [AI translations](ai-translations.md).
* **Summon from a comment** — comment on any block, type `@gitbook`, and tell it what you need.
* **Review change requests** — add it as a reviewer to act as a docs linter, flagging style guide issues and suggesting or fixing errors. See [Review change requests with Agent](review-change-requests.md).

#### Automatic documentation suggestions

{% hint style="warning" %}
This feature is in early access.
{% endhint %}

Agent can also connect to the signals your team already uses to understand your product and customers — support conversations, tickets, and threads from connected tools. With that context, it can identify gaps, propose updates, and generate docs changes automatically. See [Run an Agent audit](run-an-audit.md).

### Add a style guide and custom instructions

Configure Agent with your team's [style guide](style-guide.md) or site-specific instructions, and it uses that context whenever it creates or edits content for that site.

To add either, open your site's **Settings**, under **General** in the site sidebar, and click **Agents**, then add your instructions in the custom instructions field. You can also open this from a change request — open the Agent chat window, then its Actions menu, and click **Configure GitBook Agent**.

**Example custom instructions:**

```
You are a technical writer at Stripe. Use clear, direct language and prioritize accuracy over flourish. For guides, always introduce the concept with a one-sentence summary and break content into well-structured sections. For quickstarts, always use a stepper and keep every step action-first and concise.
```

### FAQ

<details>

<summary>How does GitBook Agent use my data?</summary>

We follow our data protection practices to keep your data private. GitBook Agent doesn't use your data to train AI models — we share the information you add to it with OpenAI only to provide the feature. See OpenAI's privacy policy for more information.

</details>

<details>

<summary>How much does GitBook Agent cost?</summary>

GitBook Agent is free for all plans while in beta. If you're not on a paid plan and not on a trial, free usage includes 10 messages per week.

[Translations](ai-translations.md) are priced separately as a monthly add-on — see [pricing](ai-translations.md#pricing).

</details>

<details>

<summary>Can I override the default tone of GitBook Agent's output?</summary>

Yes. Tell it your preferred style or tone in site-level instructions, or in a prompt within a change request.

</details>
