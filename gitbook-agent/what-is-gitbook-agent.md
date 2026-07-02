---
description: >-
  Work with an AI teammate to keep your documentation accurate, complete, and up
  to date
icon: bolt-auto
---

# What is GitBook Agent?

GitBook Agent is an AI teammate that works alongside you. It helps you keep your documentation accurate, complete, and current. GitBook Agent is deeply integrated into GitBook. You don’t need new workflows to use it.

{% hint style="info" %}
If you edit your docs locally with an AI assistant, use [GitBook’s skill.md file](../creating-content/ai-coding-assistants-and-skillmd.md).
{% endhint %}

### What can GitBook Agent do?

GitBook Agent can:

* **Write docs based on a prompt:** Ask GitBook Agent to update a page, rename a product, or make any other change you need.
* **Import content into GitBook:** Attach files like PDFs and Microsoft Word documents in the GitBook Agent chat sidebar. GitBook Agent extracts and formats the content into pages in your space.
* **Plan and implement bigger changes:** Describe what you need. GitBook Agent opens a change request, explains its edits, responds to feedback, and implements the plan you create together.
* **Follow your styleguide:** Define your team's writing rules in a [styleguide](../creating-content/styleguide.md), and GitBook Agent treats it as the source of truth when writing or reviewing content.
* **Follow custom, site-level instructions:** Give GitBook Agent site-specific instructions, such as how to add links or which block types to avoid.
* **Translate your documentation:** Choose the content you want to translate, select a language, and GitBook Agent localizes your docs.
* **Summon from a comment:** Add a comment to any block on your page, type `@gitbook`, and tell GitBook Agent what you need.
* **Review change requests:** Add GitBook Agent as a reviewer on your change request. It can act as a docs linter, flag style guide issues, and suggest or fix errors.

#### Automatic documentation suggestions

{% hint style="warning" %}
**Automatic docs suggestions are in early access**

Head to [identifying-content-gaps.md](identifying-content-gaps.md "mention") to learn more.
{% endhint %}

GitBook Agent can also connect to the signals your team uses to understand your product and your customers’ needs: support conversations, tickets, and threads from your connected tools.

With this context, GitBook Agent can identify gaps, propose updates, and generate docs changes automatically.

As your docs evolve with your product, your customers get the right information when they need it.

### Explore GitBook Agent’s features

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Write with GitBook Agent</strong></td><td>Create content from a prompt, or edit a single block</td><td><a href="write-and-edit-with-ai.md">write-and-edit-with-ai.md</a></td></tr><tr><td><strong>Review with GitBook Agent</strong></td><td>Ask GitBook Agent to check your work for spelling, grammar, and style</td><td><a href="review-change-requests-with-gitbook-agent.md">review-change-requests-with-gitbook-agent.md</a></td></tr><tr><td><strong>Translate your docs site</strong></td><td>GitBook Agent can create auto-updating localizations</td><td><a href="translations.md">translations.md</a></td></tr></tbody></table>

### Add a style guide and custom instructions

You can configure GitBook Agent with your team’s style guide or site-specific instructions.

GitBook Agent uses this context whenever it creates or edits content for that site.

To add a style guide or custom instructions, open your site’s **Settings** and choose the **Agents** tab. Add your instructions in the custom instructions field.

You can also open this screen from a change request. Open the GitBook Agent chat window, then open the **Actions menu** <picture><source srcset="../.gitbook/assets/25_01_10_actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/25_01_10_actions_icon_light.svg" alt=""></picture> and choose **Configure GitBook Agent** <picture><source srcset="../.gitbook/assets/25_01_10_settings_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/25_01_10_settings_icon_light.svg" alt=""></picture>.

#### Custom instructions example

Here’s an example of the custom instructions you can add in GitBook Agent’s settings.

{% code overflow="wrap" %}
```
You are a technical writer at Stripe. Use clear, direct language and prioritize accuracy over flourish. For guides, always introduce the concept with a one-sentence summary and break content into well-structured sections. For quickstarts, always use a stepper and keep every step action-first and concise.
```
{% endcode %}

### FAQs

<details>

<summary>How does GitBook Agent use my data?</summary>

We follow our data protection practices to keep your data private.

GitBook Agent does not use your data to train AI models. We share the information you add to GitBook Agent with OpenAI only to provide GitBook Agent. See OpenAI’s privacy policy for more information.

</details>

<details>

<summary>How much does GitBook Agent cost?</summary>

GitBook Agent is free for all plans while in beta. If you’re not on Pro and not on a trial, free usage includes 10 messages per week.

[Translations](translations.md) are priced separately as a monthly add-on. Visit [the pricing section](translations.md#pricing) to find out more.

</details>

<details>

<summary>Can I override the default tone of GitBook Agent’s output?</summary>

Yes. You can override GitBook Agent’s default personality and tone.

If you want more detailed output, or a specific style or tone, tell GitBook Agent in site-level instructions or in a prompt in a change request.

</details>
