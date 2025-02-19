---
description: "Display information more dynamically with a set of cards —\_with or without images"
---

# Cards

You can use cards to create a visually pleasing page layout, combining text and images in a grid. They’re ideal for building landing pages or displaying any other content in a non-linear way.

You can adjust [switch between medium or large cards](cards.md#card-size) and link them to the relevant resources.

### Example of a card

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>GitBook homepage</strong></td><td>Visit our website and find out more about GitBook.</td><td><a href="https://www.gitbook.com/">https://www.gitbook.com/</a></td><td><a href="../../.gitbook/assets/card_gitbook_website.svg">card_gitbook_website.svg</a></td></tr><tr><td><strong>Developer docs</strong></td><td>Build you own GitBook integration!</td><td><a href="https://developer.gitbook.com/">https://developer.gitbook.com/</a></td><td><a href="../../.gitbook/assets/card_developer_docs.svg">card_developer_docs.svg</a></td></tr><tr><td><strong>Sign up to GitBook</strong></td><td>Click here to get started for free.</td><td><a href="https://app.gitbook.com/join">https://app.gitbook.com/join</a></td><td><a href="../../.gitbook/assets/card_gitbook_signup.svg">card_gitbook_signup.svg</a></td></tr></tbody></table>

### Adding links <a href="#adding-links-and-images-to-your-cards" id="adding-links-and-images-to-your-cards"></a>

Hover over a card and open its **Options menu** <picture><source srcset="../../.gitbook/assets/options_menu_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/options_menu_icon_light.svg" alt=""></picture>. Here you can add a target link, so users can jump directly to a location when they click the card.

{% hint style="success" %}
When creating cards, we recommend you use **target links instead of hyperlinks**. With a target link, your readers can click anywhere on the card to access the linked URL.
{% endhint %}

### Adding images

Hover over a card and open its **Options menu** <picture><source srcset="../../.gitbook/assets/options_menu_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/options_menu_icon_light.svg" alt=""></picture>. Here you can add a cover image to your card. Alternatively, just click the **Add cover image** option on the card itself.

This will open the **Select file** modal. Here you can drag and drop a new image into this, or use an image file you’ve previously uploaded to your space.

#### Choosing the right image size

GitBook will automatically crop landscape images to a 16:9 ratio on desktop and mobile. If the images you upload are portrait or have a 1:1 ratio, they will be cropped to 16:9 on desktop and display as square or portrait on mobile.

<figure><img src="../../.gitbook/assets/13_02_25_cards_desktop.svg" alt=""><figcaption><p>On desktop, all card images will display in a landscape 16:9 ratio, regardless of their dimensions. We recommend using the same dimensions for consistency.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/13_02_25_cards_mobile.svg" alt=""><figcaption><p>On mobile, square or portrait images will displayed as shown on the left. Landscape images will be displayed as shown on the right.</p></figcaption></figure>

To keep things consistent across desktop and mobile, we recommend uploading all the images for your cards in a 16:9 format (e.g. 1920px x 1080px).

If you want your cards to adapt their layout depending on the screen size, we’d recommend uploading images with a 1:1 ratio, and the content of your image centered.

### Changing the size of cards

You can select the card size by opening the **Options menu** <picture><source srcset="../../.gitbook/assets/options_menu_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/options_menu_icon_light.svg" alt=""></picture> to the left of your card block. The **Medium** option creates three cards in one horizontal line, while the **Large** option shows two larger cards on each line.

{% hint style="info" %}
You can make card blocks [span the full width of your window](./#full-width-blocks) by clicking on the **Options menu** <picture><source srcset="../../.gitbook/assets/options_menu_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/options_menu_icon_light.svg" alt="" data-size="line"></picture> next to the block and choosing **Full width**.
{% endhint %}
