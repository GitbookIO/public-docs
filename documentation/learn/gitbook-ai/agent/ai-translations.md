---
description: Translate your docs automatically with GitBook Agent.
---

# AI translations

{% hint style="info" %}
Only [organization admins](../../collaboration/roles-permissions-inheritance.md) can create and access translations, since it's a billable feature.
{% endhint %}

Auto translations keep your documentation current in multiple languages with minimal manual effort — create a section as a translation of another, and let GitBook Agent handle the rest.

### How translations work

* **Create a translation section** — set up a new section as a translation of an existing one, choosing a source section and target language.
* **Continuous updates** — every change to the source content only re-runs translation for the pages that changed.
* **Automatic sync** — after changes merge, the translation workflow runs automatically, keeping the translated section current.

{% hint style="info" %}
Page slugs in auto-translated sections may change unless the page has a fixed slug. Set a fixed slug before translating to keep URLs stable across languages.
{% endhint %}

### Set up an auto translation

From your organization **Home**, click **Translations** in the sidebar, then **Create translation**. Choose:

* **Source** — the section to translate.
* **From** language.
* **To** language.

Click **Create** to start the workflow — it translates your section into a duplicated, translated section in your organization. The **Translations** screen lists your configured workflows, their status, source, runs, and translated pages and words. Workflows re-run whenever the source content updates.

#### Advanced configuration

Click **Show advanced instructions** in the **Create translation** modal:

**Custom AI instructions** — guide the AI on tone of voice, style, or other preferences, to match your brand or audience.

{% hint style="info" %}
Custom instructions can't create new elements on a translated section, add extra text, or change the source content's structure.
{% endhint %}

**Glossary support** — define how specific terms are translated, keeping terminology consistent across languages.

{% hint style="warning" %}
Changing your glossary triggers a full re-translation of your content. There's no partial re-translation based on glossary usage — updating the glossary can be time- and cost-intensive.
{% endhint %}

### Add a translation to a variant

After creating a translation, add it to a published docs site as a [variant](../../publishing/site-sections-and-variants/README.md), so readers can toggle between languages in the upper right.

{% hint style="info" %}
Set the variant's default language when configuring it — best practice is to match the language of the translated section.
{% endhint %}

Set up a new variant from the structure editor, under **Site structure** → **General** in the site sidebar.

### Pricing

Translations are a paid monthly add-on:

* $25 for up to 50,000 translated words.
* $0.20 per additional 1,000 words.

Your 50,000-word allowance resets each month. Your first translation counts every word toward your bill; after that, only pages with new or updated words count.

{% hint style="warning" %}
Be cautious working on multiple translations with large pages — the translated word count includes every word on a page that contains a change, so changing a few words on a large page re-translates the whole page.
{% endhint %}

### FAQ

<details>

<summary>Why use auto-translations?</summary>

* **Effortless multilingual docs** — reach a global audience without manual translation work.
* **Smart updates** — only changed pages re-translate, saving time and resources.
* **Full control** — customize with advanced instructions and glossary management.

</details>

<details>

<summary>Can I edit the translation?</summary>

Not currently — translations are a pure transformation of the source content, so GitBook can't reconcile edits made on the result with a new translation. Instead:

* Use the glossary to define specific translations the AI should use.
* Use custom instructions to iterate on the output.

</details>

<details>

<summary>How many translations do I need to create?</summary>

Only one translation workflow per language, per source content. Creating multiple workflows accrues extra, duplicated costs.

</details>

<details>

<summary>What are some current limitations?</summary>

* Translations don't localize UI elements in your variant automatically — open **Customize** → **Configure** to [localize the interface](../../customization/social-sharing-and-custom-code.md#localize-user-interface) for a specific variant. This includes user-input customizations like announcement banners.
* Translations can't add extra content to a page, like a hint noting it was AI-translated — consider an extra page in the translated section, or an [announcement banner](../../customization/layout-and-navigation.md#announcement) on the variant.
* Changing the glossary triggers a full re-translation of all pages — there's no partial re-translation based on glossary usage.

</details>

If you need help getting started, [contact support](../../../resources/get-support.md).
