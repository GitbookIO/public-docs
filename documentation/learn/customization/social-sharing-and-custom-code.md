---
description: Configure social preview images and add custom scripts or styles.
---

# Social sharing and custom code

{% hint style="info" %}
GitBook doesn't support inserting custom code (CSS, HTML, or JS) directly into a site. GitBook already integrates with a number of popular tools, and offers [rich embeds](../creating-content/blocks/embed-a-url.md) for many more — the options below cover what you *can* configure around sharing and site behavior.
{% endhint %}

## Social accounts

Add social accounts to your site's metadata and footer from the **Sharing** tab in the customization menu. Click **+ Add account** and choose a type — X, GitHub, LinkedIn, Discord, Bluesky, and others. Adding an account here also adds it to your site's metadata; you can toggle its footer visibility independently, without affecting the metadata.

## Social preview

Upload a custom social preview image to set your site's `og:image` — shown when your site's link is shared on platforms that support OpenGraph images, like Slack or X. Without one, GitBook generates a preview automatically from your theme color, page title, and description.

If your site has multiple [site sections](../publishing/site-sections-and-variants/README.md), switch between them from the dropdown at the top of the Customization screen to set a custom preview per section.

## Extra configuration

The **Configuration** tab covers interface localization, link behavior, and page actions for AI tools.

### Localize user interface

Choose a language to localize your published content's interface — this translates the non-custom areas of the UI, but doesn't auto-translate your actual content. See [AI translations](../gitbook-ai/agent/ai-translations.md) for translating content itself.

Want a language that isn't offered yet? [Let us know](https://github.com/GitbookIO/gitbook/issues), or contribute your own translation.

### Primary link

Set a custom URL for the logo in your site's top-left corner. By default, clicking the logo returns visitors to your docs' first page — set a custom URL (external, or a specific page/section/variant) if your docs are part of a larger website and you want the logo to return visitors there instead.

### External links

Controls whether links to external URLs open in the same tab (default) or a new tab.

### Page actions

Adds a page-level dropdown for quick actions on a page's content — useful for feeding your docs into an AI prompt as context.

{% hint style="warning" %}
Disabling **Page actions** also disables the MCP server at `~gitbook/mcp`. Keep it enabled to use MCP.
{% endhint %}

* **Open in AI providers** — adds an action to open ChatGPT or Claude with the page content.
* **Copy/View as Markdown** — adds an action to copy or view the page as Markdown.
* **Connect with MCP server** — shows the MCP server link in the page actions menu. This doesn't enable the MCP server itself — that only works when Page actions is enabled overall. See [MCP server for published docs](../gitbook-ai/readers-ai/mcp-server-for-published-docs.md).
* **Edit on GitHub/GitLab** — if your section is Git Sync-connected, shows a link for readers to contribute via your linked repository.
* **Export PDF** — lets visitors [export your docs as a PDF](../publishing/pdf-export.md).

### Privacy policy

Link to your own privacy policy so visitors understand how your site uses cookies and protects their privacy. Without one, your site defaults to [GitBook's privacy policy](https://gitbook.com/docs/policies/privacy-and-security/statement/cookies).
