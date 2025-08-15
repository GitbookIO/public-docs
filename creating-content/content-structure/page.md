---
description: "Add pages, page groups or external links —\_and learn about the options you have on each page"
---

# Pages

A page is the place where you can add, edit and embed content. Pages always live inside a [space](space.md), allowing you to group related content and create different sections for the topics or areas you’re covering.

When publishing your documentation, each space will be its own [docs site](../../publishing-documentation/publish-a-docs-site/) or [site section](../../publishing-documentation/site-structure/site-sections.md), and the pages inside the space will all appear on that site.

### Table of contents

You can create as many pages as you need in a space. They’re all visible on the left sidebar of your screen in your space’s [table of contents](../../resources/gitbook-ui.md#table-of-contents). The table of content will appear in the same place when you publish your space, unless [you choose to hide it](page.md#page-options).

### Create a new page

When in [live edit](../../collaboration/live-edits.md) mode or in a [change request](../../collaboration/change-requests.md), you can create a new page by clicking **Add new...** > **Page** at the bottom of your table of contents. Alternatively, you can hover between pages in the table of contents and click the **+** icon that appears.

<figure><img src="../../.gitbook/assets/04_02_25_page.svg" alt="A GitBook screenshot showing an empty page listed in the table of contents"><figcaption><p>An empty page in GitBook. You can see it listed in the table of contents on the left-hand side.</p></figcaption></figure>

### Can’t see the option to create a new page?

{% hint style="warning" %}
If [live edits](../../collaboration/live-edits.md) are disabled for your space, you’ll need to create or edit a [change request](../../collaboration/change-requests.md). Once you’re in a change request, the **New page** button (which allows you to create pages, page groups and links) will be available in the table of contents.

Alternatively, you may not have the correct [permissions](../../account-management/member-management/permissions-and-inheritance.md) to edit a page.
{% endhint %}

### Organizing your content

There are three ways to organize your content in the table of contents:

#### Pages

A page has a title, and optional description, and an area where you can write and add any kind of content.‌

You can nest pages by dragging and dropping a page below an other in the table of contents. Doing this creates a **subpage**.

{% hint style="info" %}
**Tip:** There’s no limit to page nesting, but we’d recommend you avoid more than three levels of nesting to avoid an overly-complex navigation.
{% endhint %}

When you change the title of a page, the page’s slug (the part at the very end of the URL, e.g. `/hello-world`) will also change — unless you’ve manually set the page’s slug previously.

You can change the title and the slug of a page at any time by clicking opening the page’s **Action menu** <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture> and choosing **Rename**.

#### Page groups

With page groups, you can bring pages together into sections that cover related content.

You can create a new page group by clicking **Add new...** > **Group** at the bottom of your table of contents.

Page groups can only live at the **top level** of the table of contents. You cannot nest page groups inside page groups.

To change the title and slug of a page group, click the **Action menu** icon <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture> next to the group title in the table of contents and choose **Rename**.

#### External links <a href="#external-links" id="external-links"></a>

You can also add links to your table of contents. Clicking them will take people directly to the linked content.

Create new external link by clicking **Add new...** > **External link** at the bottom of your table of contents.

### Page icons and emojis

To improve visibility for readers when skimming your table of contents, you can add an optional icon or emoji to individual pages. The icon or emoji will appear in the table of contents, and next to the title at the top of the page.

To add an icon or emoji, click the **Add icon** button when hovering the page title, or the emoji button to the left of the title.

### Page options

In the **Page options** menu you can customize the look and feel of a selected page within a space, and control its visibility.

**Layout**

You can open the **Page options** <picture><source srcset="../../.gitbook/assets/options_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/options_icon_light.svg" alt="The Page options menu icon in GitBook"></picture> menu or change a page’s cover by hovering over the page title. You’ll see the buttons appear just above the page title.

In the **Page options** side panel, you can select how each page is displayed to those who visit your **published** content. There are three layout presets to choose from, or you can create a custom layout.

Each layout preset will toggle on or off each of the following parts of the page:

* Page title
* Page description
* Table of contents
* Page outline
* Next/previous links

#### Visibility

You can decide which pages you would like to show/hide in your published documentation, while also deciding if you would like the page to be indexed in your published doc’s search, and/or indexed by search engines.

You can hide a page or group of pages from your site's table of contents by opening the page’s **Actions menu** <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture> and toggling **Hide page**.

If hidden the following will appear in the front matter of the markdown file when using Git Sync:

<pre class="language-markdown" data-title="page.md"><code class="lang-markdown">---
hidden: true
<strong>---
</strong></code></pre>

### Page covers

You can also set a page cover for each page of your documentation. When you click the **Page cover** <picture><source srcset="../../.gitbook/assets/image_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/image_icon_light.svg" alt="The Page cover icon in GitBook"></picture> option, a default cover will be added immediately. From here, you can:

*   **Change the cover image**

    Hover over the page cover and click **Change cover**, then select or upload an image. Based on how we currently display page covers, 1990x480 pixels is the ideal size.
*   **Reposition the cover image**

    Hover over the page cover and open the **Actions menu** <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture>. Click **Reposition**, then drag the image as you wish and click **Save**.
* **Remove the cover image**\
  Hover over the page cover and open the **Actions menu** <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture>, then click **Remove**.
* **Full width and hero width**\
  You can change the style of your page cover to span the full width of your screen or just the width of your content. Hover over the page cover and open the **Actions menu** <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture>, then choose your preferred option from the menu.
