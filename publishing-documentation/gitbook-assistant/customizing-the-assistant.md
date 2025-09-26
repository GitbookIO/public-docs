---
if: visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Customizing the assistant

After adding the assistant to your website or app, you can further customize the experience by adding things like a welcome message, actionable buttons to the header, and suggestions to nudge your users with contextual questions.

### Adding a welcome message

To add a welcome message, you can use the `welcomeMessage` key when initializing the GitBook Assistant.

```javascript
window.GitBook('configure', {
    welcomeMessage: "Welcome to our help center! How can we assist you today?",
}
```

### Adding buttons

Adding buttons to the assistant allows you to give users extra actions in the UI of the assistant. You can add icons from [Font Awesome](https://fontawesome.com/), and any buttons will appear in the assistant’s header once loaded.

```javascript
window.GitBook('configure', {
    buttons: [
        { 
            label: 'Contact Support', 
            icon: 'envelope', 
            onClick: () => { 
                window.open('mailto:support@example.com', '_blank');
            } 
        },
        { 
            label: 'Documentation', 
            icon: 'book', 
            onClick: () => { 
                window.open('https://docs.example.com', '_blank');
            } 
        }
    ],
}
```

### Adding suggestions

You can also add suggestions to the assistant, which will show up as clickable prompts for your users to use when the assistant loads.

```javascript
window.GitBook('configure', {
    suggestions: [
        'Help me get started with my new account',
        'How do I reset my password?',
        'What are your pricing plans?'
    ],
}
```
