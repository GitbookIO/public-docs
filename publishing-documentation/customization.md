---
icon: palette
description: Create branded documentation with a custom logo, fonts, colors, links and more
---

# Site customization

{% hint style="info" %}
Certain customization features are available on [Premium and Ultimate site plans](https://www.gitbook.com/pricing).
{% endhint %}

You can customize the appearance of your published documentation, match the user interface to the language of your content, and more.

You can apply customizations to your entire docs site as a site-wide theme, or to individual variants and site sections.

<figure><img src="../.gitbook/assets/10_01_25_customized_site.svg" alt=""><figcaption><p>GitBook's own documentation is an example of a customized docs site.</p></figcaption></figure>

### General

Control how your content looks in the Customization tab of your site’s dashboard. The available options are:

<details>

<summary>Title, icon and logo</summary>

**Title**\
You can set any title you choose for your space. Note: this setting will only affect the title that displays _in the published documentation_. If you want to edit the title in the GitBook app, close the customize menu and edit it at the top of the space.

**Icon**\
You can set an emoji, or upload an icon of your own. Note: this setting will only affect the icon that displays _in the published documentation_ and it’ll also be used as the favicon for the page. If you want to edit the icon used within the GitBook app, close the customize section and click on the icon at the top of the space.

**Custom logo** <mark style="background-color:purple;">Premium & Ultimate</mark>\
You can replace _both_ the published space’s title and icon with a custom logo so that your documentation better reflects your own branding — and, you can upload two versions: one for light mode, and one for dark mode.

_What’s the difference between the icon and logo options?_\
The icon setting lets you upload a small, 132x132px image, which will appear _alongside_ your space title. The custom logo option lets you upload a larger image (we recommend at least 600px wide), which will completely replace any icon and title you’ve set.

</details>

<details>

<summary>Themes (for light &#x26; dark modes)</summary>

Themes let you customize the color scheme of your published content for both light and dark mode. While you can use any colors you like, it’s important to keep accessibility in mind and choose something with good contrast so your content is easy to read.

**Default theme**\
All spaces have access to this theme, where the header background color will be aligned with the background color for the rest of the space.

**Bold theme** <mark style="background-color:purple;">Premium & Ultimate</mark>\
The bold theme uses the primary color as the header background color.

**Contrast theme** <mark style="background-color:purple;">Premium & Ultimate</mark>\
The contrast theme has a dark header background color in light mode, and a light header background color in dark mode.

**Custom theme** <mark style="background-color:purple;">Premium & Ultimate</mark>\
The custom theme option lets you to set your own color preferences for the background color and link color in the header, in addition to choosing the primary color for light and dark mode.

**Tint color**\
Switch between a plain background and a subtly tinted background that either complements the primary color selected in your [theme](customization.md#themes-for-light-and-dark-modes), or matches a custom tint color of your choice.

</details>

<details>

<summary>Modes</summary>

**Show mode toggle**\
Enable this if you would like visitors to your published content to be able to manually toggle between light and dark mode. Readers can find the toggle at the bottom of any published page, both on larger screens and mobile devices.

**Default mode**\
Choose whether visitors to your published content will see it in light or dark mode initially. If **Show mode toggle** is enabled, they’ll be able to switch to the other option if they prefer. If **Show mode toggle** is disabled, they’ll only be able to see your content in the mode you choose here.

_Note: if you just want to change the theme within the GitBook app, you can do that from your **Settings**_ <picture><source srcset="../.gitbook/assets/settings_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/settings_icon_light.svg" alt=""></picture> _menu, which can be found at the bottom of the_ [_sidebar_](../resources/gitbook-ui.md#sidebar)_._

</details>

<details>

<summary>Site styles</summary>

**Font family** <mark style="background-color:purple;">Premium & Ultimate</mark>\
You can choose a font family for your published content from a list of popular options. GitBook currently doesn’t support uploading or linking custom fonts.

**Icons** <mark style="background-color:purple;">Premium & Ultimate</mark>\
When using page icons, you can set the weight and style of the displayed icons here.

**Corner style**\
Choose either a rounded or straight corner style, to help align your published GitBook content with your own brand’s styling preferences.

</details>

<details>

<summary>Sidebar styles</summary>

**Background style**\
Choose the background style for the sidebar container. The color is created from the color set in **Theme**.

**List style**\
Choose the sidebar list and selected items style.

</details>

### Layout

<details>

<summary>Header</summary>

**Navigation**\
Add header links to your site. You could use header links to point to important parts of your documentation, or perhaps to link back to your main website.

You can choose what type of appearance you would like your link to have, and can choose between a normal link, primary button, and secondary button.

When enabled, simply add a title and a URL for each link. We support two levels of header navigation, meaning that you can have sub-links that appear in a dropdown menu.

</details>

<details>

<summary>Pagination</summary>

Control the display of the previous and next buttons that appear at the bottom of each page in your space. You can additionally set this feature for [specific pages](../creating-content/content-structure/page.md).

</details>

<details>

<summary><strong>Footer</strong> <mark style="background-color:purple;">Premium &#x26; Ultimate</mark></summary>

Enable or disable a footer section for your space.

**Logo**\
Add your logo or another image in the footer.

**Copyright text**\
Add copyright information to your footer.

**Navigation**\
Add links in your footer, in multiple sections. Similar to the header, you can add a title and URL for each link. Make sure to also include a section title for each section you create.

</details>

### Configure

<details>

<summary>Localize user interface</summary>

You can select from a list of languages to localize the user interface of your published content. This will apply translations to the **non-custom** areas of the interface.

This setting will _not_ auto-translate your actual content, but can help with matching the user interface to the language that you are writing in.

Is there a language we don’t yet offer that you would like to see included in this list? [Let us know](https://github.com/GitbookIO/gitbook/issues), or [contribute your own translation](https://www.gitbook.com/solutions/open-source)!

</details>

<details>

<summary>Edit on GitHub/GitLab</summary>

If your space is connected to a Git repository, you can optionally show a link for your users to contribute to your documentation from your linked repository.

</details>

<details>

<summary>Privacy Policy</summary>

You can link to your own privacy policy to help visitors understand how your GitBook content uses cookies, and how you protect their privacy. If you choose not to set one, your site will default to [GitBook’s own privacy policy](https://policies.gitbook.com/privacy-and-security/statement/cookies).

</details>

### Customizing sites with multiple sections

<figure><img src="../.gitbook/assets/04_02_2025_site_customization.svg" alt=""><figcaption><p>The customization panel in GitBook.</p></figcaption></figure>

If you have a docs with with multiple sections, you can control the customization of each one individually.

Select the whole site or a specific site section using the drop-down menu at the top of the **Customization** panel.

* **Site-wide settings** – These automatically apply to all linked spaces.
* **Section specific settings** – If you’re using site sections, you’re can set section specific customization that will override the default site-wise setting.

{% hint style="warning" %}
Changes you make to specific site sections will override the site-wide customization settings, even if you change the site-wide setting again later.
{% endhint %}

### What counts as ‘Advanced customization’?

Every GitBook user can take advantage of basic customization options on their docs site. Pro or Enterprise plan users can also use advanced customization features to further tweak their docs to match their brand.

Advanced customization options include:

* **Custom logo** – Add a logo that replaces the emoji and title at the top of your docs site.
* **Icons** - Change the weight and style of page icons in your docs site.
* **Custom font** – Change the font of your docs to one of the built-in options.
* **Footer** – Add a custom logo, copyright text and navigation to a footer at the bottom of your documentation.
* **Bold, Contrast and Custom themes** – Customize the primary color of your docs, as well as setting the background color for your header and the links within it.

### What cannot be customized?

The options above provide lots of ways for you to customize your space, but there are a few things that you won’t be able to customize, regardless of [your chosen plan](../account-management/plans/).

1. It’s not possible to customize the layout of the elements on the page (However, it _is_ possible to [hide certain elements on specific pages](../creating-content/content-structure/page.md)).
2. It’s not possible to insert custom code (such as CSS, HTML or JS) directly into your GitBook site. We already integrate with a number of popular tools, and offer [rich embeds](../creating-content/blocks/embed-a-url.md) for many more.
3. It’s not possible to remove the small "Powered by GitBook" link that appears in published documentation.
