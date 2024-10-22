---
description: Decide how your site is structured to best fit your content.
icon: window-restore
---

# Site structure and navigation

The content on your site comes from [spaces](../../content-editor/editor/content-structure/what-is-a-space.md) in your organization. You can link one or multiple spaces. GitBook will publish each one and take care of navigation between spaces.

## Content types

Linked spaces can serve as one of two different content types, which determine how GitBook treats them in relation to each other and shows them to customers.

{% hint style="warning" %}
Updated site sections are slowly rolling out to users. Hang tight, as you may not have access to this feature at this point.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th><select><option value="2imVPYM2ofOh" label="Premium sites" color="blue"></option><option value="Vn0fvP8MQ7Vj" label="Ultimate sites" color="blue"></option></select></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden><select></select></th></tr></thead><tbody><tr><td><strong>Content variants</strong></td><td>Publish multiple versions of the same content — ideal for localization, versioning, and more.</td><td><span data-option="2imVPYM2ofOh">Premium sites</span></td><td><a href="../../.gitbook/assets/variants (2).png">variants (2).png</a></td><td><a href="../publish-a-docs-site/share-links.md">share-links.md</a></td><td></td></tr><tr><td><strong>Site sections</strong></td><td>Split your site into distinct parts — ideal for multiple products or parts of your organization.</td><td><span data-option="Vn0fvP8MQ7Vj">Ultimate sites</span></td><td><a href="../../.gitbook/assets/sections.png">sections.png</a></td><td><a href="../publish-a-docs-site/public-publishing.md">public-publishing.md</a></td><td></td></tr></tbody></table>

## Managing your site structure

From your docs site’s dashboard, click the **Settings** <picture><source srcset="../../.gitbook/assets/settings-dark.png" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/settings-light.png" alt="" data-size="line"></picture> button, then scroll down to **Site structure**. Here you can see all the content of your site, divided into sections and variants.&#x20;

Your site starts out with a single section with your site's name and a single variant with the space you linked during your [site's set-up](https://app.gitbook.com/o/d8f63b60-89ae-11e7-8574-5927d48c4877/s/NkEGS7hzeqa35sMXQZ4X/\~/changes/426/published-documentation/publish-a-docs-site).

<figure><img src="../../.gitbook/assets/Site structure initial.png" alt=""><figcaption></figcaption></figure>

### Linking a space to your docs site

To add a variant, click the **Add variant** button in the section you'd like to add to, then choose a space to link. The new variant is then added to the list of variants within the chosen section and will be available to visitors in the variant dropdown on your site.

To add a section, click the **Add section** button underneath the table and choose a space to link as a section. This space will serve as the first (or only) variant within your new section. The new section is then added to the table and will be available to visitors as a tab at the top of your site.

When you add a space (as a variant or section), we generate a name and slug for it based on the space's title.&#x20;

### Changing a linked space

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/Site structure full.png" alt=""><figcaption></figcaption></figure>

</div>

You can change the name and slug of each of your linked spaces by tapping the **Edit** ![](../../.gitbook/assets/Edit.svg) button in the table row of the space you'd like to edit. Edit the field(s) you'd like to change, then click the **Save** <img src="../../.gitbook/assets/Icon Button.png" alt="" data-size="line">  button to save.

{% hint style="warning" %}
Changing a linked space's slug will change the space's canonical URL, and might result in broken links across your site.
{% endhint %}

To replace a linked space with a different space, click on the **More menu** ![](../../.gitbook/assets/3dots-vertical.svg)  in the space's table row and then click **Replace linked space**.

### Reordering linked spaces

Your site displays linked spaces in the order that they appear in your Site structure table. Spaces can be reordered by grabbing the **Drag handle** ![](../../.gitbook/assets/Dots-Drag.svg) and moving it up or down. Alternatively, you can press the **More menu** ![](../../.gitbook/assets/3dots-vertical.svg)  in the table row of the space you'd like to edit and choosing **Move up** or **Move down**. The changed order will be reflected on your site immediately.

### Setting default content

If you have multiple sections in your site, one section will be marked as the default. This section is shown when visitors arrive on your site, and is served from your site's root URL. Other sections each have a slug that is appended to the root URL.

If you have multiple variants within a section, one variant will be marked as the default. Like sections, the default variant is shown when visitors arrive on your site (or when they visit a section). Other variants each have a slug that is appended to the section's URL.

To set a space as default, click on the **More menu** ![](../../.gitbook/assets/3dots-vertical.svg) in the space's table row and then click **Set as default**.

{% hint style="info" %}
Setting a space as default removes its slug field, as it will be served from the section root instead. We will redirect the space's slug to the appropriate path, to ensure visitors keep seeing your content.
{% endhint %}

### Remove content from a site

To remove the content of a space from a site, click the **Settings** <picture><source srcset="../../.gitbook/assets/settings-dark.png" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/settings-light.png" alt="" data-size="line"></picture> button from your docs site dashboard, then scroll down to the **Site structure** section to find the content you want to remove. Open the **More menu** ![](../../.gitbook/assets/3dots-vertical.svg) next to the linked space you want to remove and select **Delete from site**. This will remove it from the published site, but will not delete the space or the content within.

