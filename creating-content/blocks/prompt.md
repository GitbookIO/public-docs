---
description: Add a prompt block to a page to share reusable AI prompts
---

# Prompt

Prompt blocks let you share reusable AI prompts in your docs. Readers can copy the prompt in one click, or open it in a supported AI tool.

### Add a prompt block

1. On an empty line, type `/`.
2. Click **Prompt** in the insert menu.
3. Add the block content and settings.

### Prompt block fields

Each prompt block includes these fields:

* **Description**: A short summary of what the prompt does.
* **Icon**: An optional icon that helps readers scan the block.
* **Prompt**: The prompt text you can copy or send to an AI tool.

The prompt field supports Markdown, so you can structure longer prompts with headings, lists, and other formatting.

### Open in AI providers

The **Open in AI providers** setting controls whether the block shows a menu of AI tools that can open the prompt directly.

If you enable this setting, readers can open the prompt from the provider menu in published docs.

If you leave this setting unset, GitBook derives its initial value from the site-level **Open in AI providers** page action. You can manage that setting in [Extra configuration](../../docs-site/customization/extra-configuration.md#open-in-ai-providers).

### Example

Use a prompt block when you want readers to reuse a prompt exactly as written. For example:

{% code title="Example prompt" overflow="wrap" %}
```markdown
Summarize the key changes in this release note. Group the response into: new features, breaking changes, and recommended next steps. Keep the answer under 150 words.
```
{% endcode %}

### When to use a prompt block

Prompt blocks work well for:

* Reusable prompts for support, onboarding, or troubleshooting
* Prompt templates for summaries, analysis, or drafting
* Workflows that start in your docs and continue in an AI tool

### Best practices

Write prompts the same way you want readers to use them:

* State the task clearly.
* Define the output format.
* Add constraints like length, tone, or required inputs.

### Published docs behavior

On a published page, a prompt block helps readers move faster.

* **Copy prompt** copies the full prompt to the clipboard.
* **Open in AI providers** shows a provider menu when enabled.
