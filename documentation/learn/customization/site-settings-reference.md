---
description: Reference for every site-level setting.
---

# Site settings reference

This is a lookup reference for every settings tab on a docs site. Where a setting is covered in depth elsewhere, this page links out instead of duplicating it.

### General

<details>

<summary>Site title and icon</summary>

See [Themes, colors, and typography](themes-colors-typography.md#title-icon-and-logo).

</details>

<details>

<summary>Analytics cookie</summary>

If your site uses [site analytics](../analytics/README.md), it sets cookies to identify returning visitors and gather that data. Disabling these cookies also disables site analytics for that site.

The cookie notice appears whenever analytics is enabled through an integration — especially Google Analytics. To remove the notice, open **Site settings → Integrations** and disable or remove Google Analytics.

</details>

<details>

<summary>Unpublish site</summary>

Unpublish your site while keeping its settings and customizations — publish it again at any time.

</details>

<details>

<summary>Delete site</summary>

Unpublish and remove your site from the **Docs site** section of the GitBook app.

{% hint style="danger" %}
Deleting a site is permanent — its settings and customizations are lost, though the underlying content remains in its [space](../creating-content/content-structure.md).
{% endhint %}

</details>

<details>

<summary>Access</summary>

Manage who can access and administer your docs site — open **Access** and click **Manage permissions**, or use **Share** from the site's **Overview** page. Site permissions are available on all plans.

New sites derive permissions from their linked [spaces](../creating-content/content-structure.md) by default, until you update permissions from the site permissions modal. Site permissions can also affect linked spaces in **Inherited** mode — each inherited space receives the highest permission level granted by the organization, any parent collection, and any site that includes it.

</details>

### Agents

Manage organization-level settings for [GitBook Agent](../gitbook-ai/agent/README.md).

### Styleguide

Create, reuse, or detach the [style guide](../gitbook-ai/agent/style-guide.md) that defines your team's writing rules and keeps GitBook Agent consistent.

### Audience

<details>

<summary>Audience</summary>

Choose who sees your published content — see [Publishing your site](../publishing/README.md).

</details>

<details>

<summary>Adaptive content</summary>

{% hint style="info" %}
Available on the Ultimate plan.
{% endhint %}

Turn on [adaptive content](../access/adaptive-content-concepts.md) for your site's pages, variants, and sections, to show or hide content based on visitor permissions. Your visitor token signing key is also shown here.

</details>

### Domain and URL

<details>

<summary>Custom domain</summary>

Configure a custom domain to unify your site with your own branding — see [Set a custom domain](../publishing/custom-domain/README.md).

</details>

<details>

<summary>GitBook subdirectory</summary>

Publish your content on a subdirectory (like `yourcompany.com/docs`) — see [Custom subdirectories](../publishing/custom-domain/custom-subdirectories.md).

</details>

### Redirects

See [Create redirects](../publishing/create-redirects.md).

### Features

<details>

<summary>PDF export</summary>

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Let visitors export your docs as a PDF — see [PDF export](../publishing/pdf-export.md).

</details>

<details>

<summary>Page ratings</summary>

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Let visitors rate each page — sad, neutral, or happy. Review results from [site analytics](../analytics/README.md) → **Pages & feedback**.

</details>

### AI & MCP

AI settings have different plan entitlements: AI Search is available on Premium and Ultimate; GitBook Assistant and MCP connectors are Ultimate-only.

<details>

<summary>Choose the AI experience</summary>

Choose your site's search experience — see [AI search on your site](../gitbook-ai/ai-search.md).

</details>

<details>

<summary>Extend GitBook Assistant with MCP connectors</summary>

{% hint style="info" %}
Available on the Ultimate plan.
{% endhint %}

Configure MCP servers that GitBook Assistant can use when answering questions in your docs — see [Connect knowledge sources](../gitbook-ai/assistant/knowledge-sources.md).

</details>

### Connections

See [Connect knowledge sources](../gitbook-ai/assistant/knowledge-sources.md).

### Structure

See [Site sections and variants](../publishing/site-sections-and-variants/README.md).

### Plan

See [How pricing works](../../account-and-billing/how-pricing-works.md).
