---
icon: window-restore
description: Add structure to your published documentation using site sections and variants
---

# Site structure

The content on your site comes from [spaces](../../creating-content/content-structure/space.md) in your organization. You can link one or multiple spaces. GitBook will publish each one and handle the navigation between spaces.

## Content types

Linked spaces can serve as one of two different content types, which determine how GitBook treats them in relation to each other and shows them to visitors.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden><select></select></th></tr></thead><tbody><tr><td><strong>Content variants</strong></td><td>Publish multiple versions of the same content — ideal for localization, versioning, and more.</td><td><a href="../../.gitbook/assets/Content variants.svg">Content variants.svg</a></td><td><a href="variants.md">variants.md</a></td><td></td></tr><tr><td><strong>Site sections</strong></td><td>Split your site into distinct parts — ideal for multiple products or parts of your organization.</td><td><a href="../../.gitbook/assets/Site sections.svg">Site sections.svg</a></td><td><a href="site-sections.md">site-sections.md</a></td><td></td></tr></tbody></table>

## Managing your site structure

From your docs site’s dashboard, click the **Settings** <picture><source srcset="../../.gitbook/assets/settings - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/settings.svg" alt=""></picture> button, then click **Structure**. Here you can see all the content of your site, divided into sections and variants.&#x20;

Your site starts out with a single section with your site's name and a single variant with the space you linked during your [site's set-up](https://app.gitbook.com/o/d8f63b60-89ae-11e7-8574-5927d48c4877/s/NkEGS7hzeqa35sMXQZ4X/~/changes/426/published-documentation/publish-a-docs-site).

<figure><img src="../../.gitbook/assets/publishing-documentation-site-structure.png" alt=""><figcaption><p>The structure of a published docs site.</p></figcaption></figure>

### Linking a space to your docs site

To add a [site section](site-sections.md), click the **Add section** button underneath the table and choose a space to link as a section. The new section is then added to the table and will be available to visitors as a tab at the top of your site.

To add a [variant](variants.md), click the **Add variant** button in the section you’d like to add to, then choose a space to link. The new variant is then added to the list of variants within the chosen section and will be available to visitors in the variant dropdown on your site.

When you add a space — as a variant or a section — a name and slug will be generated based on the space’s title.&#x20;

### Changing sections or variants

<div data-full-width="false"><figure><img src="../../.gitbook/assets/publishing-documentation-change-linked-space.png" alt=""><figcaption><p>Update a site section or variant.</p></figcaption></figure></div>

You can change the name and slug of each of sections and variants by clicking the **Edit** <picture><source srcset="../../.gitbook/assets/edit - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/edit.svg" alt=""></picture> button in the table row of the item you’d like to edit. This will open a modal. Edit the field(s) you’d like to change, then click the **Save** button to save.

{% hint style="info" %}
Changing a linked space's slug will change the space's canonical URL. GitBook will create an automatic redirect from the old URL to the new one. You can also [manually create redirects](../site-redirects.md).
{% endhint %}

To replace a section or variant, first delete it by clicking its **Edit** <picture><source srcset="../../.gitbook/assets/edit - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/edit.svg" alt=""></picture> button, then click the **Delete** button in the lower left of the modal. Once the item is deleted, click the **Add section** or **Add variant** button to add it again.

### Reordering sections or variants

Your site displays sections and variants in the order that they appear in your **Site structure** table. They can be reordered by grabbing the **Drag handle** <picture><source srcset="../../.gitbook/assets/options-menu-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/options-menu.svg" alt=""></picture> and moving it up or down. The changed order will be reflected on your site immediately.

You can also use the keyboard to select and move content. Select a section or variant with the space bar, then use the arrow keys to move it up or down. Hit the space bar again to confirm the new position.&#x20;

### Setting default content

If you have multiple sections in your site, one section will be marked as **Default**. This section is shown when visitors arrive on your site, and is served from your site’s root URL. Other sections each have a slug that is appended to the root URL.

If you have multiple variants within a section, one variant will be marked as the default. Like sections, the default variant is shown when visitors arrive on your site, or when they visit a section. Other variants each have a slug that’s appended to the section’s URL.

To set a space as default, click on the **Actions menu** <picture><source srcset="../../.gitbook/assets/actions - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions.svg" alt=""></picture> in the space’s table row and then click **Set as default**.

{% hint style="info" %}
Setting a space as default removes its slug field, as it will be served from the section root instead. GitBooks redirects the space’s slug to the appropriate path, to ensure visitors keep seeing your content.
{% endhint %}

### Remove content from a site

To remove the content of a space from a site, click the **Settings** <picture><source srcset="../../.gitbook/assets/settings - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/settings.svg" alt=""></picture> button from your docs site dashboard, then click **Structure** to find the content you want to remove. Click the **Edit** <picture><source srcset="../../.gitbook/assets/edit - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/edit.svg" alt=""></picture> button next to the space you want to remove, then click the **Delete** button in the lower left of the modal. This will remove it from the published site, but **will not delete the space or the content within**.

