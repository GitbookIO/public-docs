---
description: >-
  Create and publish AI translations that stay synchronized with your source
  docs.
---

# Translating your docs with AI

As far as any good documentation goes, accessibility — and [Internationalization](https://en.wikipedia.org/wiki/Internationalization_and_localization) (i18n) specifically — plays an important role.

GitBook Agent can [translate your documentation](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/gitbook-agent/translations) into multiple languages and keep it synchronized with its source. You can use built-in translations rather than maintaining a custom translation workflow.

{% hint style="info" %}
Only organization admins can create and access translations. Translations are a paid add-on — see [our pricing page](https://www.gitbook.com/pricing) for more information.
{% endhint %}

### How translations work

[A translation in GitBook](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/gitbook-agent/translations) creates a translated [section](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/site-structure/site-sections) from a source section. GitBook Agent translates the content and keeps it current.

Whenever you merge changes to your content source, GitBook automatically re-translates only the changed pages. The translated section stays aligned with the source without a separate workflow.

{% hint style="info" %}
Set a fixed slug on source pages before translating if you need stable language-specific URLs. Otherwise, translated page slugs might change.
{% endhint %}

### Create a translation

To create a translation:

1. In your organization **Home**, click **Translations**.
2. Click **Create translation**.
3. Under **Source**, select the section you want to translate.
4. Select the source language under **From**.
5. Select the target language under **To**.
6. Click **Create**.

GitBook will create a translated section and start the translation workflow. The **Translations** screen shows each workflow’s status, source, runs, translated pages, and word count.

### Configure translation instructions

If you want to add custom instructions to a translation, before you click **Create**, click **Show advanced instructions** to set optional translation guidance.

#### Add custom AI instructions

Use custom instructions to guide tone, style, and other translation preferences. GitBook Agent will always follow and preserve the source structure.

Custom instructions cannot add content, create new elements, or change the structure from the source content.

#### Add a glossary

Add glossary terms to keep product terminology consistent. Each term must use the source-language wording.

For example, an English glossary can map `SSO` to `SSO` and `Git Sync` to `Git Sync`. GitBook Agent then keeps those terms unchanged in translated output.

{% hint style="warning" %}
Changing a glossary triggers a full re-translation. This can increase processing time and cost.
{% endhint %}

### Publish the translated docs

Add the translated section to [variant](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/site-structure/variants) on your site so visitors can switch languages.

To add the translation, follow these steps:

1. In the site sidebar, under **General**, click **Site structure**.
2. Select the source section you’ve translated and click **Add variant**, then open the **Use existing content** tab
3. Search for the translated section, hover over it and choose **Use as content**.
4. Give your variant a title and click **Add variant**.&#x20;
5. Optionally, change the slug of your variant.

Once undrafted and published, your users can then select the language from the published site’s language switcher.

{% hint style="info" %}
**Note:** Variants are created as drafts by default. To publish your translaltion, undraft the variant and ensure your site is published.
{% endhint %}

### Understand translation limits and pricing

You can’t edit translated content directly. Use custom AI instructions and the glossary to improve translated output.

Translations don’t localize variant UI elements automatically. In the site sidebar, open **Customize** under **Tools** to localize the interface for each variant.

Translations are billed monthly or annually:

* $25 per month includes 50,000 translated words each month.
* $250 per year includes 50,000 translated words each month.
* Additional translation costs $0.20 per 1,000 words.

Your first translation counts every word. Later runs charge for pages containing new or updated words. A small change on a large page re-translates the entire page, but not the entire section.

### FAQ

<details>

<summary>Can I use a CI/CD workflow with translated docs?</summary>

Yes. Use [GitHub & GitLab Sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync "mention") to connect your source documentation to GitHub or GitLab. Your CI/CD workflow can update that source repository.

When Git Sync imports the commit, GitBook updates the source content. After the source changes merge, the translation workflow re-runs for changed pages.

Use Git Sync for source-content automation. Use built-in translations for the translation workflow.

</details>

<details>

<summary>How many translation workflows do I need?</summary>

Create one workflow for each target language and source section. Multiple workflows for the same language create duplicate costs.

</details>

<details>

<summary>Can I add a banner that says content was AI translated?</summary>

Translations cannot add content that isn’t in the source. Add a separate page to the translated section, or add an announcement banner to its site variant.

</details>
