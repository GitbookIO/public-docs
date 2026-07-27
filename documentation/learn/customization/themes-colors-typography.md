---
description: Set your site's theme, brand colors, and fonts.
---

# Themes, colors, and typography

## Title, icon, and logo

### Title

Set any title for your site. This only affects the title shown in published documentation — to change the title in the GitBook app itself, close the customize menu and edit it at the top of the section.

### Icon

Set an emoji, or upload your own icon — it's also used as your site's favicon. Like the title, this only affects the published site; edit the app's icon from within the section itself.

### Custom logo

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Replace both the title and icon with a custom logo, in separate light-mode and dark-mode versions.

{% hint style="info" %}
**Icon vs. logo:** the icon is a small (132×132px) image shown alongside your site title, doubling as the favicon. The logo is larger (600px+ wide recommended) and completely replaces both the icon and title.
{% endhint %}

## Themes

Themes set your published content's color scheme for light and dark mode. Your **primary color** and **tint** shape most of the interface.

* **Clean** — a modern theme with translucency and minimal styling. Primary color/tint affects links and highlighted elements. Available on all sites, and the default.
* **Muted** — lower contrast between elements, with a more pronounced background and some inverted elements. Available on all sites.
* **Bold** *(Premium & Ultimate)* — prominent colors and strong contrast; primary color/tint colors the header and other highlighted elements.
* **Gradient** *(Premium & Ultimate)* — a gradient background with splashes of color, driven by your primary color/tint.

## Colors

### Primary color

Affects highlighted interface items and navigation — links, the current page/section, breadcrumbs, and primary header buttons. GitBook automatically adjusts contrast for readability.

### Tint color

Subtly colors all text and icons across the site, including header links and the **Ask or search** bar — but not navigational elements like links and buttons, which always use the primary color.

GitBook suggests tint colors based on your primary color, or you can pick a fully custom one.

<details>

<summary>Using tint to set your background color</summary>

A tint that's very light or very dark, and close to neutral, becomes your site's exact background color instead of the default white or dark background — useful for a subtle off-white, warm-paper, or deep-dark feel.

{% hint style="info" %}
* The tint needs to be close to neutral — a strongly colored tint keeps the standard background and only tints accents.
* It needs to be clearly light or clearly dark — a mid-tone gray won't change the background.
* With the **Bold** theme, tint styles the header instead of the page background, so the background stays as-is.
{% endhint %}

</details>

### Semantic colors

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Applied to hint blocks in published content, and optionally to code blocks. Change each hint style's background color — changes only affect the published site, not the editor, where hints stay their standard colors.

### Code theme

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Changes the appearance of code and API blocks. Choose from:

* **Adaptive themes** — standard light/dark themes that use your site's color palette.
* **[Shiki](https://shiki.style/themes) themes** — 60+ presets in light and dark modes.

Set separate themes for light and dark mode — you can mix a dark code theme with light-mode docs, or vice versa. By default, your chosen theme applies to both code blocks and OpenAPI blocks; click **Customize per block type** to set a different theme for OpenAPI blocks.

## Modes

**Show mode toggle** — lets visitors manually switch between light and dark mode, shown at the bottom of any published page.

**Default mode** — the mode visitors see by default. If the toggle is enabled, they can switch; if disabled, they only see this mode.

{% hint style="info" %}
To change the theme within the GitBook app itself (not your published site), use the Settings menu at the bottom of the sidebar.
{% endhint %}

## Site styles

### Font family

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Choose a standard and monospace font family from a curated list.

{% hint style="info" %}
Monospace fonts apply to code blocks and OpenAPI blocks.
{% endhint %}

### Custom fonts

{% hint style="info" %}
Available on the Ultimate plan.
{% endhint %}

Upload your own standard and monospace fonts to match your brand's style guide — click **Add custom font**, and upload both regular and bold weights. GitBook currently supports `.woff` and `.woff2`; for other formats, contact `support@gitbook.com`.

### Icons

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

Set the weight and style of page icons, when you're using them.

### Corner style

Rounded or straight corners, to match your brand.

### Depth style

Applies to cards, buttons, and other elements with a shadow:

* **Subtle** — some shadow and elevation.
* **Flat** — no shadow or elevation.

### Link style

* **Default** — highlights the entire link in your primary or tint color.
* **Accent** — a colored underline, leaving the text color unchanged.

## Sidebar styles

### Background style

The sidebar container's background style — **Default** or **Filled** — colored from your selected theme.

### List style

The sidebar list and selected-item style — **Default**, **Pill**, or **Line**.
