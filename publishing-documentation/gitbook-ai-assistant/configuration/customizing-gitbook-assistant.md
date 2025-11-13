---
description: >-
  Customize the experience when embedding GitBook Assistant into your product or
  app by setting welcome messages, buttons, and more
---

# Customizing the Assistant

After adding the Assistant to your website or app, you can further customize the experience by adding things like actionable buttons to the header, suggestions to nudge your users with contextual questions, and more.

### Adding buttons

Adding buttons to the Assistant allows you to give users extra actions in the UI of the Assistant. You can add icons from [Font Awesome](https://fontawesome.com/), and any buttons will appear in the Assistant's header once loaded.

```javascript
window.GitBook("configure", {
  buttons: [
    {
      label: "Contact Support",
      icon: "envelope",
      onClick: () => {
        window.open("mailto:support@example.com", "_blank");
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

You can also add suggestions to GitBook Assistant, which will show up as clickable prompts for your users to use when the Assistant loads.

```javascript
window.GitBook("configure", {
  suggestions: [
    "Help me get started with my new account",
    "How do I reset my password?",
    "What are your pricing plans?",
  ],
});
```
