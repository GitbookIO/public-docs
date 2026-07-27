---
description: Make a docs site live, or take it down.
---

# Publish and unpublish a site

### Create a docs site

{% stepper %}
{% step %}
#### Start a new site

From your organization **Home**, click the **+** icon next to **Sites**.
{% endstep %}

{% step %}
#### Name it

Enter a name visitors will recognize, then click **Create**.
{% endstep %}

{% step %}
#### Choose a starting point

Pick a documentation template, an import, an OpenAPI specification, a blank section, or Git Sync.
{% endstep %}
{% endstepper %}

For a complete walkthrough, see the [Quickstart](../../getting-started/quickstart.md).

{% hint style="info" %}
Manage site permissions in **Settings → Members**, independently of organization settings — see [Roles, permissions, and inheritance](../collaboration/roles-permissions-inheritance.md).
{% endhint %}

### Publish a docs site

Open your site from organization **Home**, and click **Publish** in the site header. Sites are public by default — change visibility in **Settings → Audience** (see [Site settings reference](../customization/site-settings-reference.md)).

Choose an audience:

* **Public** — publish to the web for anyone.
* **Privately with share links** — publish with private, shareable links.
* **Authenticated access** — protect published docs behind a sign-in. See [Authenticated access](../access/authenticated-access/README.md).

#### Public publishing

If your docs are for a public audience, publish them to the web — public spaces can be indexed by search engines, or you can disable that.

However you publish, you keep control over who can *edit* your content, and only your primary content branch publishes — any [change requests](../collaboration/change-requests/README.md) stay private until merged.

To publish publicly, open your site, click **Publish**, and choose **Public**.

**Publish without search engine indexing:** by default, your site is indexed by search engines. Disable this to keep your docs accessible to anyone with the link, but out of search results — useful for a beta version of your docs, or large-scale user testing without affecting SEO with potentially duplicate content.

**Page-level search indexing controls.** GitBook provides two separate controls, at the individual page level:

* **Internal search indexing** — controls whether a page is indexed in GitBook's internal search and Ask AI, affecting content search within your section and Ask AI's ability to reference the page.
* **External search indexing** — controls whether search engines and web crawlers (Google, ChatGPT, etc.) can index the page, affecting SEO and web discoverability.

{% hint style="info" %}
Page-level search indexing controls are available on Premium and Ultimate plans.
{% endhint %}

Search indexing settings inherit hierarchically: disabling indexing on a parent page disables it for every sub-page beneath it, and sub-pages can't re-enable it — the effect cascades down the whole hierarchy. This keeps indexing policy consistent within a section, and prevents accidentally exposing content that should stay private.

#### Private publishing with share links

{% hint style="info" %}
Share links are available on Premium and Ultimate plans.
{% endhint %}

Share content privately with customers or partners without inviting them to your organization. Open your site's settings, click **Audience settings**, and choose **Share links**. Click **Create link** to generate one — review and name it, customize its domain, and copy it.

Once active, the link carries a private token unique to your section. Anyone with the link gets read-only access, in an interface that looks like any other published content. Generate as many links as you need from **Audience settings**.

The content is accessible to anyone with the link. Your team can access it from the **Docs sites** section of the sidebar, or by navigating there directly.

**Revoke a link** to disable or regenerate it — open the visibility menu, go to link and domain settings, and revoke. Anyone with the old link immediately loses access. You can revoke and regenerate share links at any time.

### Unpublish or delete a docs site

To **unpublish** your site (keeping its settings and customizations), open **Settings → General** and select **Unpublish site**.

To **delete** a docs site, open **Settings → General** and select **Delete site**.

{% hint style="danger" %}
Deleting a site permanently removes its settings and customizations. Your content remains in your organization — find it in [the GitBook interface's "All content" section](../../resources/the-gitbook-interface.md).
{% endhint %}
