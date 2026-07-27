---
description: Organize one site into sections (tabs) and variants (versions or languages).
---

# Site sections and variants

{% hint style="info" %}
Sections are available on the Ultimate plan.
{% endhint %}

The content on your site lives in its [sections](../../creating-content/content-structure.md) — add one or as many as you like, and GitBook publishes each one and handles navigation between them.

Content in your site serves one of two roles:

* **Sections** split your site into distinct parts — ideal for separate products, or catering to both end users and developers with tailored content. Sections appear as tabs at the top of your site.
* **Content variants** publish multiple versions of the same content — ideal for localization, or documenting multiple product versions (v1, v2, v3). Variants appear in a dropdown on your site.

{% hint style="info" %}
**Sections or variants?** Use sections for semantically different parts of your docs. Use variants for variations of the *same* content — translations, or historical versions of the same product.
{% endhint %}

### Section groups

Keep sections together in a group under a single heading — groups appear as a dropdown in your site's nav, useful for adding hierarchy. Sections in a group can carry an optional description, shown below the section title in the dropdown.

To create one, click the arrow next to **New section** and choose **New section group**. Name the group, then add sections to it — existing ones, or new content.

If your site supports multiple languages, you can also translate section group titles, section titles, and descriptions — see [Multilingual sections](multilingual-sections.md).

## Managing your site structure

Managing your site's structure also manages its top navigation bar, letting readers jump between sections and groups. Open the structure editor from **Site structure**, under **General** in the site sidebar — it shows all your site's content, divided into sections and variants. A new site starts with a single section and a single variant, holding the content from setup.

The following applies to both sections and variants unless noted otherwise.

### Adding content

To add a **section**, click **Add section** underneath the table and choose the content to add — it appears as a new tab at the top of your site.

To add a **variant**, click **Add variant** within the section you want it in, and choose the content — it appears in that section's variant dropdown.

Either way, GitBook generates a name and slug from the content's title.

### Editing

Click the **Edit** button in a section's or variant's table row to open a modal where you can change its name and slug (sections can also have an icon). Click **Save** to apply, or **Delete** to remove it entirely.

{% hint style="info" %}
Changing a slug changes its canonical URL — GitBook automatically redirects the old URL to the new one. You can also [manually create redirects](../create-redirects.md).
{% endhint %}

To replace a section's or variant's content, delete it via **Edit** → **Delete**, then re-add it with **Add section** or **Add variant**.

### Reordering

Sections and variants display in the order they appear in the **Site structure** table. Drag the handle in a row to reorder — changes apply immediately. You can also use the keyboard: select an item with the space bar, move it with the arrow keys, and confirm with the space bar again.

### Setting default content

One section is always marked **Default** — shown when visitors arrive, served from your site's root URL. Other sections get a slug appended to the root URL. The same applies to variants within a section: one default, shown on arrival, others appended to the section's URL.

To set an item as default, open its **Actions menu** and click **Set as default**.

{% hint style="info" %}
Setting content as default removes its slug field, since it's served from the section root instead — GitBook redirects the old slug to keep visitors landing correctly.
{% endhint %}

### Removing content

Open the structure editor, find the section or variant, open its **Actions menu**, and choose **Remove**.

{% hint style="success" %}
Removing content from your site removes it from the published site, but doesn't delete the underlying content — find it in [the GitBook interface's "All content" section](../../../resources/the-gitbook-interface.md).
{% endhint %}
