# Collection customization

![](../../.gitbook/assets/Customize.png)

Customizing a collection allows you to set top-level customizations that spaces within the collection can inherit. This is useful if you want to manage top-level customizations, letting you change customization options without having to change the settings for every space individually.

Customizing your collection lets you control the branding, presentation and extra features of your space's public content.

{% hint style="info" %}
**Good to know:** most customization settings apply to your **public content**. This keeps your writing experience and in-app GitBook content consistent, while allowing you to control the output to a degree.
{% endhint %}

## Presentation

Presentation customizations let you tweak how your collection's basics will appear publicly:

### Published title & icon

You can override the icon and title that your visitors will see when they access your public content. This lets you give your collection an 'internal' (in-app) title and an 'external', or public title. The same applies to the collection icon.

{% hint style="info" %}
**Good to know:** It's quite common to use longer, or more specific, titles in published content. Changing your presentation settings allows you to do so, without worrying about having long, idiosyncratic collection titles in the GitBook app.
{% endhint %}

### Localize user interface

You can select from a list of languages to localize the user interface of your public content. This will apply translations to the **non-custom** areas of your public content interface. It won't do anything spicy like auto-translate your actual content, but if you're writing content in a certain language, it's always good to have the surrounding UI reflect that.

![](../../.gitbook/assets/Localize.png)

{% hint style="info" %}
**Good to know:** We're constantly making efforts to support further localized languages. [Give us a shout](https://www.gitbook.com/contact/contact-support) if you have a suggestion.
{% endhint %}

## Logos and social

You can upload a custom social preview image for your space. This will set the space's `og:image` to your uploaded image, and it'll show when the space's link is shared to any platform or product that supports OpenGraph images.

You can also replace the space's title entirely with a custom logo. This lets you keep your brand running through your docs.

{% hint style="info" %}
**Good to know:** Changing the space's logo will replace the icon **and** the title of the space with the entered logo. If you want to keep the space title visible, you can upload a square logo as the space's [published icon](collection-customization.md#published-title-and-icon).
{% endhint %}

## Collection publish mode

This lets you control how your collection will be published, and set any default space.

### Publish mode

Publish mode will determine how your published collection is presented. Currently, only one mode is supported: variants. You can learn more about variants in the [collection visibility](../../getting-started/publishing/collection-publishing.md#collections-as-variants) section of these docs.

{% hint style="info" %}
**Good to know:** we're actively working on new ways to publish collections, so while it might seem strange to only have one option here, in the future there'll be other ways to display your published content!
{% endhint %}

### Default space

Variants work by rendering a space with a dropdown in the sidebar, allowing you to switch quickly between other variants. To make this possible, a primary space needs to be selected. This space will render when the collection URL is accessed directly.

If you're using variants to document multiple versions of an API, for example, you might set your default space to your latest API version, let's say, 'Version 3' as an example. When you access the collection's URL, it'll render the Version 3 space, with a dropdown to switch between any other included spaces (e.g. Version2, Version 1, Legacy, etc.)

To set a default space within a collection, open the collection page in GitBook. Next to the title of the collection, open the collection context menu and select 'Customize collection'. Under the 'Collection publish mode' section, use the 'Default space' option to select a primary variant within that collection.

![](<../../.gitbook/assets/Default Space.png>)

## Theming

Theming lets you customize the primary colour, heading theme, and font family of your public content.

{% hint style="info" %}
**Good to know:** When theming, you'll be able to see a preview of any changes you make. This can be useful when deciding e.g. which header theme or primary colour you want to use.
{% endhint %}

### Primary colour

The primary colour of your public content will be applied to things like links, hover states, and buttons. This colour change will only apply to your **published** content.

{% hint style="info" %}
**Good to know:** Accessibility is important! While you can set your primary colour to pretty much anything you like, try to keep things accessible and choose a colour that'll have good contrast when used as a text link.
{% endhint %}

### Heading theme

You can choose between a number of heading themes for your public content:

The **None** theme will show no header, instead placing the space's icon and title (or logo, if you've overwritten it) in the table of contents. This is great for minimal docs, or docs where you don't need a persistent header.

The **Light** header theme will show a white header and dark text.

The **Bold** header theme will set the header background to your primary color, and show light-colored text.

The **Dark** header theme will show a dark header, with light text.

### Font family

You can customize the font family of your public content from a list of predefined options.

{% hint style="info" %}
**Good to know:** GitBook doesn't support uploading or linking of custom fonts. If you think we're missing a typeface that works wonderfully for headers, body copy, and captions, [give us a shout](https://www.gitbook.com/contact/contact-support).
{% endhint %}

## Header links

You can add links to your header, with each link having a URL and a text label. This is useful if you want to link to specific parts of your documentation, or back to pages of your main site, directly in the header of your docs.

## Public content features

You can enable a number of features for your public content, depending on what plan you're on.

![](<../../.gitbook/assets/Privacy Policy.png>)

### PDF Export

PDF Export allows your readers to export your space as a PDF.

### Page rating

Page rating allows your readers to give simple feedback on any pages of your space, and will show a feedback section at the bottom of each page. You can track the feedback results in the Activity section of the space.

### Privacy policy

Enabling the privacy policy option lets you override the privacy policy link in the public content cookie banner.
