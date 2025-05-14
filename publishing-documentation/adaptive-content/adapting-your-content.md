---
description: Tailor your content for different users.
---

# Adapting your content

After setting up your authentication method, you’ll be able to use the data to adapt the content in your site for different users.

Adaptive content works in the following ways:

* Hiding or showing pages
* Hiding or showing site variants
* Hiding or showing site sections

{% hint style="info" %}
We are currently working on more ways to use adaptive content and the claims you send to GitBook, such as adaptive blocks and UI.
{% endhint %}

### Working with the condition editor

The condition editor is where you’ll set the conditions for showing or hiding a page, variant, or section. After opening the condition editor, you’ll be able to type a condition that will run against visitors to your site.&#x20;

#### Example

The data you pass through your users to GitBook is attached to an object called `visitor.claims`.&#x20;

Let’s take a look at an example if we want to write a conditional statement to **only show a page for users who are part of a beta program** you might define.

```javascript
visitor.claims.isBetaUser == true
```

The condition above means that any user who matches this claim (i.e. `isBetaUser` is `true` in the user’s claim), will be able to see and access the page. Any user who does not match this claim (including visitors without any claims set), will not be able to see or access the page.

The condition editor also comes built in with autocomplete, which suggests claims or attributes that have been found on previous visitors to your site, helping you craft the conditional statement for your pages, variants, or sections.

You can combine multiple claims into the condition editor to match specific users by using the `&&` or `||` operator. You can read more about operators [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#binary_logical_operators).

### Conditional pages

To launch the condition editor for a page, head to the actions menu <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt=""></picture> next to a page, and click “**Add condition**”. You can also launch the condition editor from a [page’s options](../../resources/gitbook-ui.md#page-options).

You can see which pages in your space have conditions set if the page has a page condition icon <picture><source srcset="../../.gitbook/assets/page-condition - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/page-condition.svg" alt=""></picture> next to it.

### Conditional variants

To launch the condition editor for a variant, head to the actions menu <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt=""></picture> next to a variant, and click “**Add condition**”.

You can see which variants in your docs have conditions set if the variant has a page condition icon <picture><source srcset="../../.gitbook/assets/page-condition - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/page-condition.svg" alt=""></picture> next to it.

### Conditional sections

To launch the condition editor for a section, head to the actions menu <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt=""></picture> next to a section, and click “**Add condition**”.

You can see which sections in your docs have conditions set if the section has a page condition icon <picture><source srcset="../../.gitbook/assets/page-condition - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/page-condition.svg" alt=""></picture> next to it.

