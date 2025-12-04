---
description: >-
  Customize the experience when embedding Docs Embed into your product or
  app by setting welcome messages, actions, and more
---

# Customizing Docs Embed

After adding Docs Embed to your website or app, you can further customize the experience by adding things like actionable buttons to the sidebar, suggestions to nudge your users with contextual questions, and more.

### Adding actions

Adding actions to the embed allows you to give users extra actions in the UI. You can add icons from [Font Awesome](https://fontawesome.com/), and any actions will appear in the sidebar alongside tabs once loaded.

**Note**: This was previously named `buttons`. Use `actions` instead, it has the same functionality.

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

You can also add suggestions to the Assistant tab, which will show up as clickable prompts for your users to use when the Assistant loads.

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
    subtitle: "How can I help you today?"
  },
});
```

### Configuring tabs

Override which tabs are displayed. By default, the embed shows tabs based on your site's configuration.

```javascript
window.GitBook("configure", {
  tabs: ['assistant', 'docs'], // Show both tabs
  // tabs: ['assistant'], // Show only assistant tab
  // tabs: ['docs'], // Show only docs tab
});
```

