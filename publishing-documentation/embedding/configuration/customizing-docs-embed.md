---
description: >-
  Customize the experience when embedding Docs Embed into your product or
  app by setting welcome messages, actions, and more
---

# Customizing Docs Embed

After [adding Docs Embed to your website or app](../implementation/README.md), you can further customize the experience by adding things like actionable buttons to the sidebar, suggestions to nudge your users with contextual questions, and more.

### Customizing the button (standalone only)

When using the standalone script tag implementation, you can customize the label and icon of the button that launches the embed widget.

```javascript
window.GitBook("configure", {
  button: {
    label: "Ask",
    icon: "assistant", // 'assistant' | 'sparkle' | 'help' | 'book'
  },
});
```

**Available icon options:**
- `assistant` - <i class="fa-gitbook-assistant">:gitbook-assistant:</i> Assistant icon (default)
- `sparkle` - <i class="fa-sparkle">:sparkle:</i> Sparkle icon
- `help` - <i class="fa-circle-question">:circle-question:</i> Help/question icon
- `book` - <i class="fa-book-open">:book-open:</i> Book icon

**Note:** This option is only available when using the standalone script tag implementation. For React or Node.js implementations, you'll need to create your own button to trigger the embed.

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

### Configuring tabs

Override which tabs are displayed. By default, the embed shows tabs based on your site's configuration.

```javascript
window.GitBook("configure", {
  tabs: ["assistant", "docs"], // Show both tabs
  // tabs: ['assistant'], // Show only assistant tab
  // tabs: ['docs'], // Show only docs tab
});
```
