---
icon: rectangle-history
description: "Publish multiple versions of your documentation in a single site —\_ideal for language localization, product versions, and more."
---

# Content variants

You can publish multiple versions of the same documentation as part of a single docs site. These variations will be available to the end users via the space switcher in the top-left corner of the published site.

{% embed url="https://www.youtube.com/watch?v=Pj7mrFArOWY" %}

### Why publish multiple spaces on one site?

A site with multiple spaces is useful if you need to group together the content of your spaces — such as if you’re documenting multiple versions of an API (v1, v2, v3, etc.), or documenting your content in different languages.

The spaces you link can contain any content, but it is recommended to use variants as _variations of the same content_. If the spaces you link are semantically different from each other, consider adding them as [site sections](site-sections.md) instead.

<figure><img src="../../.gitbook/assets/variants (1).png" alt=""><figcaption><p>Multiple spaces published through a single GitBook docs site.</p></figcaption></figure>

### Adding a variant to your docs site

From your docs site’s dashboard, click the **Settings** <picture><source srcset="../../.gitbook/assets/settings-dark.png" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/settings-light.png" alt="" data-size="line"></picture> button, then scroll down to the **Site structure** section. Here you can see all the content of your site.

To add a variant, click the **Add variant** button in the section you'd like to add to, then choose a space to link. The new variant is then added to the list of variants within the chosen section and will be available to visitors in the variant dropdown on your site.

<figure><img src="../../.gitbook/assets/Site structure full.png" alt=""><figcaption></figcaption></figure>

### Changing a variant

You can change the name and slug of each of your linked spaces by tapping the ![](../../.gitbook/assets/Edit.svg) **Edit** button in the table row of the space you'd like to edit. Edit the field(s) you'd like to change, then click the <img src="../../.gitbook/assets/Icon Button.png" alt="" data-size="line"> **Save** button to save.

{% hint style="warning" %}
Changing a linked space's slug will change the space's canonical URL, and might result in broken links across your site.
{% endhint %}

To replace a linked space with a different space, click on the ![](../../.gitbook/assets/3dots-vertical.svg) **More** menu in the space's table row and then click **Replace linked space**.

### Reordering variants

Your site displays variants in the order that they appear in your Site structure table. Variants can be reordered by grabbing the **Drag handle** ![](../../.gitbook/assets/Dots-Drag.svg) and moving it up or down. Alternatively, you can press the **More menu** ![](../../.gitbook/assets/3dots-vertical.svg)  in the table row of the space you'd like to edit and choosing **Move up** or **Move down**. The changed order will be reflected on your site immediately.

### Setting a default variant

If you have multiple variants within a section, one variant will be marked as the default. This variant is shown when visitors arrive on your site (or when they visit a section). Other variants each have a slug that is appended to the site's URL.

To set a variant as default, click on the **More menu** ![](../../.gitbook/assets/3dots-vertical.svg) in the space's table row and then click **Set as default**.

{% hint style="info" %}
Setting a space as default removes its slug field, as it will be served from the section root instead. We will redirect the space's slug to the appropriate path, to ensure visitors keep seeing your content.
{% endhint %}

### Remove a variant from a site

To remove the content of a space from a site, click the **Settings** <picture><source srcset="../../.gitbook/assets/settings-dark.png" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/settings-light.png" alt="" data-size="line"></picture> button from your docs site dashboard, then scroll down to the **Site structure** table to find the content you want to remove. Open the **More menu** ![](../../.gitbook/assets/3dots-vertical.svg) next to the linked space you want to remove and select **Delete from site**. This will remove it from the published site, but will not delete the space or the content within.

