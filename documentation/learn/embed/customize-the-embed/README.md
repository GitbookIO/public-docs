---
description: Configure the embed's behavior and extend the Assistant with custom tools.
---

# Customize the embed and add custom tools

After [installing the embed](../install-the-embed.md), customize its behavior with configuration options — available via `GitBook("configure", {...})` (script tag), the `tools`/other props on `<GitBookFrame>` (React), or `frame.configure({...})` (NPM). Where syntax differs by method, it's called out below.

### Configuring tabs

Override which tabs are displayed. All tabs are enabled by default, provided your site supports them — for example, if Assistant isn't enabled for your site, it won't show even if listed. If you set `tabs`, the embed shows only the tabs you list.

```javascript
window.GitBook("configure", {
  tabs: ["assistant", "search", "docs"], // Show all tabs
  // tabs: ["search", "docs"], // Show search and docs only
  // tabs: ['docs'], // Show only docs tab
});
```

### Customizing the button (standalone script only)

{% hint style="info" %}
Button customization is only available with the standalone script tag. For React or Node.js/NPM, create your own button to launch the embed.
{% endhint %}

```javascript
window.GitBook("configure", {
  button: {
    label: "Ask",
    icon: "assistant", // 'assistant' | 'sparkle' | 'help' | 'book'
  },
});
```

Available icons: `assistant` (default), `sparkle`, `help`, `book`.

### Setting the color scheme

By default, the embed follows the iframe's CSS `color-scheme`, matching your app theme or browser preference automatically. To force a mode, pass `colorScheme` when you initialize the embed, build the frame URL, or render the React component — this is not part of `configure`.

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

Actions add extra buttons to the sidebar alongside tabs, each with a label, a [Font Awesome](https://fontawesome.com/search) icon, and an `onClick` callback. Actions can control the embed itself or run any code you want.

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

{% hint style="info" %}
This option was previously named `buttons` — use `actions` instead. Actions aren't the same as [custom tools](custom-tools-for-the-assistant.md): use actions for buttons the user clicks, and tools when you want the Assistant itself to choose and run code.
{% endhint %}

### Adding suggestions

Suggestions show as clickable prompts when the Assistant tab loads:

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

Customize the Assistant tab's welcome message:

```javascript
window.GitBook("configure", {
  greeting: {
    title: "Welcome!",
    subtitle: "How can I help you today?",
  },
});
```

### Overriding the assistant name

`assistantName` overrides the assistant name shown in the UI (up to 32 characters):

```javascript
window.GitBook("configure", {
  assistantName: "Support Copilot",
});
```

### Showing a close button

`closeButton` displays a close button inside the Assistant:

```javascript
window.GitBook("configure", {
  closeButton: true,
});
```

### Showing or hiding the trademark

`trademark` shows or hides the GitBook trademark in the embed UI, including the footer and Assistant branding (default `true`):

```javascript
window.GitBook("configure", {
  trademark: false,
});
```

### Custom tools

`tools` extends the Assistant with actions it can run in your product — see [Custom tools for the Assistant](custom-tools-for-the-assistant.md).

### Authenticated access

`visitor` passes a signed token (and optional unsigned claims) for [adaptive content](../../access/adaptive-content-concepts.md) or [authenticated access](../../access/authenticated-access/README.md) — see [Authenticate the embed](../authenticate-the-embed.md).

For the complete method and prop reference across all three integration methods, see the [Embed API reference](../embed-api-reference.md).
