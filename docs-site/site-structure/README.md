---
description: Add structure to your published documentation using sections and variants
icon: window-restore
---

# Site structure

The content on your site lives in its [sections](../../creating-content/content-structure/space.md). You can add one or multiple sections. GitBook will publish each one and handle the navigation between them.

## Content types

Content in your site can serve as one of two different content types, which determine how GitBook treats it and shows it to visitors.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden><select></select></th><th data-hidden data-card-cover-dark data-type="image">Cover image (dark)</th></tr></thead><tbody><tr><td><strong>Sections</strong></td><td>Split your site into distinct parts — ideal for multiple products or parts of your organization.</td><td><a href="../../.gitbook/assets/25_08_29_site_sections.svg">25_08_29_site_sections.svg</a></td><td><a href="../../.gitbook/assets/25_12_10_site_sections_1.png">25_12_10_site_sections_1.png</a></td><td><a href="site-sections.md">site-sections.md</a></td><td></td><td><a href="../../.gitbook/assets/25_12_10_site_sections.png">25_12_10_site_sections.png</a></td></tr><tr><td><strong>Content variants</strong></td><td>Publish multiple versions of the same content — ideal for localization, versioning, and more.</td><td><a href="../../.gitbook/assets/25_08_29_content_variants.svg">25_08_29_content_variants.svg</a></td><td><a href="../../.gitbook/assets/25_12_10_content_variants_1.png">25_12_10_content_variants_1.png</a></td><td><a href="variants.md">variants.md</a></td><td></td><td><a href="../../.gitbook/assets/25_12_10_content_variants.png">25_12_10_content_variants.png</a></td></tr></tbody></table>

## Managing your site structure

By managing the structure of your site, you can also manage your site’s top navigation bar. This navigation bar allows users to jump to different sections and groups.

Open the structure editor from **Site structure**, under **General** in the site sidebar. Here you can see all the content of your site, divided into sections and variants.

Your site starts out with a single section with your site's name and a single variant with the content you created during your site's set-up.

<figure><img src="../../.gitbook/assets/25_12_10_structure_light.png" alt="A GitBook screenshot showing a docs site&#x27;s structure"><figcaption><p>The structure of a published docs site.</p></figcaption></figure>

### Adding a section to your docs site

To add a [section](site-sections.md), click the **Add section** button underneath the table and choose the content to add. The new section is then added to the table and will be available to visitors as a tab at the top of your site.

To add a [variant](variants.md), click the **Add variant** button in the section you’d like to add to, then choose the content to add. The new variant is then added to the list of variants within the chosen section and will be available to visitors in the variant dropdown on your site.

When you add content — as a variant or a section — a name and slug will be generated based on its title.

### Changing sections or variants

<div data-full-width="false"><figure><img src="../../.gitbook/assets/25_12_10_edit_variant_light.png" alt="A GitBook screenshot showing how to edit a variant"><figcaption><p>Update a site section or variant.</p></figcaption></figure></div>

You can change the name and slug of each of your sections and variants by clicking the **Edit** <picture><source srcset="../../.gitbook/assets/25_01_10_edit_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_edit_icon_light.svg" alt="The Edit icon in GitBook"></picture> button in the table row of the item you’d like to edit. This will open a modal. Edit the field(s) you’d like to change, then click the **Save** button to save.

{% hint style="info" %}
Changing a section's slug will change its canonical URL. GitBook will create an automatic redirect from the old URL to the new one. You can also [manually create redirects](../../publishing-documentation/site-redirects.md).
{% endhint %}

To replace a section or variant, first delete it by clicking its **Edit** <picture><source srcset="../../.gitbook/assets/25_01_10_edit_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_edit_icon_light.svg" alt="The Edit icon in GitBook"></picture> button, then click the **Delete** button in the lower left of the modal. Once the item is deleted, click the **Add section** or **Add variant** button to add it again.

### Reordering sections or variants

Your site displays sections and variants in the order that they appear in your **Site structure** table. They can be reordered by grabbing the **Drag handle** <picture><source srcset="../../.gitbook/assets/25_01_10_options_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_options_light.svg" alt="The Options menu icon in GitBook"></picture> and moving it up or down. The changed order will be reflected on your site immediately.

You can also use the keyboard to select and move content. Select a section or variant with the space bar, then use the arrow keys to move it up or down. Hit the space bar again to confirm the new position.

### Setting default content

If you have multiple sections in your site, one section will be marked as **Default**. This section is shown when visitors arrive on your site, and is served from your site’s root URL. Other sections each have a slug that is appended to the root URL.

If you have multiple variants within a section, one variant will be marked as the default. Like sections, the default variant is shown when visitors arrive on your site, or when they visit a section. Other variants each have a slug that’s appended to the section’s URL.

To set a section or variant as default, click on the **Actions menu** <picture><source srcset="../../.gitbook/assets/25_01_10_actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture> in its table row and then click **Set as default**.

{% hint style="info" %}
Setting content as default removes its slug field, as it will be served from the section root instead. GitBook redirects the old slug to the appropriate path, to ensure visitors keep seeing your content.
{% endhint %}

### Remove content from a site

To remove a section or variant from a site, open the structure editor from **Site structure**, under **General** in the site sidebar, and find the content you want to remove.

Open the **Actions menu** <picture><source srcset="../../.gitbook/assets/25_01_10_actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_01_10_actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture> for the content you want to remove and choose **Remove**.

{% hint style="success" %}
Removing content from your site will remove it from the published site, but **will not delete the content itself** — you can still find it in [All content](../../creating-content/all-content.md).
{% endhint %}
