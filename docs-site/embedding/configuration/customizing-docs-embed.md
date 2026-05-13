---
description: >-
  Customize the experience when embedding Docs Embed into your product or app by
  setting welcome messages, actions, and more
---

# Customizing the Embed

After [adding Docs Embed to your website or app](../implementation/), you can further customize the experience by adding actionable buttons to the sidebar, suggestions to nudge your users with contextual questions, tabs, and more.

### Customizing the button ([standalone](../implementation/script.md) only)

When using the [standalone script tag implementation](../implementation/script.md), you can customize the label and icon of the button that launches the embed widget.

{% hint style="info" %}
This button customization option is only available when using the [standalone script tag implementation](../implementation/script.md). For [React](../implementation/react.md) or [Node.js/NPM package](../implementation/nodejs.md) implementations, you'll need to create your own button to launch the embed.
{% endhint %}

```javascript
window.GitBook("configure", {
  button: {
    label: "Ask",
    icon: "assistant", // 'assistant' | 'sparkle' | 'help' | 'book'
  },
});
```

**Available icon options:**

* `assistant` - <i class="fa-gitbook-assistant">:gitbook-assistant:</i> Assistant icon (default)
* `sparkle` - <i class="fa-sparkle">:sparkle:</i> Sparkle icon
* `help` - <i class="fa-circle-question">:circle-question:</i> Help/question icon
* `book` - <i class="fa-book-open">:book-open:</i> Book icon

### Setting the color scheme

By default, the embed follows the iframe's CSS `color-scheme`. This lets it match your app theme or the browser preference automatically.

If you want to force a mode, pass `colorScheme` when you initialize the embed, build the frame URL, or render the React component. This is not part of `configure`.

{% tabs %}
{% tab title="Standalone script" %}
```javascript
window.GitBook(
  "init",
  { siteURL: "https://docs.company.com" },
  { colorScheme: "dark" }
);
```
{% endtab %}

{% tab title="Node.js/NPM" %}
```javascript
const iframeURL = gitbook.getFrameURL({
  colorScheme: "dark",
});
```
{% endtab %}

{% tab title="React" %}
```jsx
<GitBookFrame colorScheme="dark" />
```
{% endtab %}
{% endtabs %}

### Adding actions

Adding actions to the embed allows you to give users extra actions in the UI. Each action consists of a label, icon (from [Font Awesome](https://fontawesome.com/search?ip=brands%2Cclassic%2Cduotone)), and an `onClick` action that runs when the user clicks the action. Any actions you add will appear in the sidebar alongside tabs. Actions can control the Docs Embed itself or execute any code you'd like.

```javascript
window.GitBook("configure", {
  actions: [
    {
      label: "Contact Support",
      icon: "circle-question",
      onClick: () => {
        window.open("https://support.example.com", "_blank");
      },
    },
    {
      label: "Documentation",
      icon: "book",
      onClick: () => {
        window.open("https://docs.example.com", "_blank");
      },
    },
  ],
});
```

### Adding suggestions

You can add suggestions to the Assistant tab, which will show up as clickable prompts for your users to use when the Assistant loads.

```javascript
window.GitBook("configure", {
  suggestions: [
    "Help me get started with my new account",
    "How do I reset my password?",
    "What are your pricing plans?",
  ],
});
```

### Adding a greeting

Customize the welcome message displayed in the Assistant tab:

```javascript
window.GitBook("configure", {
  greeting: {
    title: "Welcome!",
    subtitle: "How can I help you today?",
  },
});
```

### Overriding the assistant name

Use `assistantName` to override the assistant name shown in the UI.

The value can contain up to 32 characters.

```javascript
window.GitBook("configure", {
  assistantName: "Support Copilot",
});
```

### Showing a close button

Use `closeButton` to display a close button inside the Assistant.

```javascript
window.GitBook("configure", {
  closeButton: true,
});
```

### Showing or hiding the trademark

Use `trademark` to show or hide the GitBook trademark in the embed UI — including the Docs Embed footer and Assistant branding.

```javascript
window.GitBook("configure", {
  trademark: false,
});
```

### Configuring tabs

Override which tabs are displayed. All tabs are enabled by default provided your site supports them. For example, if your site does not have the Assistant enabled, it will not be shown. If you set `tabs`, the embed shows only the tabs you list.

```javascript
window.GitBook("configure", {
  tabs: ["assistant", "search", "docs"], // Show all tabs
  // tabs: ["search", "docs"], // Show search and docs only
  // tabs: ['docs'], // Show only docs tab
});
```
