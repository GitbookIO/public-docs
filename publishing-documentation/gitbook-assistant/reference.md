---
if: visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Reference

The GitBook Assistant also exposes helper functions that further allow it to interact with your app.

### Main Functions

#### Show the widget

Display the GitBook widget if it has been hidden.

**Example:**

```js
window.GitBook('show');
```

#### Hide the widget

Hide the GitBook widget without unloading it.

**Example:**

```js
window.GitBook('hide');
```

#### Open the window

Open the GitBook assistant window.

**Example:**

```js
window.GitBook('open');
```

#### Close the window

Close the GitBook assistant window.

**Example:**

```js
window.GitBook('close');
```

#### Toggle the window

Toggle the GitBook assistant window open or closed.

**Example:**

```js
window.GitBook('toggle');
```

#### Unload the widget

Completely remove the GitBook widget from your site.

**Example:**

```js
window.GitBook('unload');
```

### Navigation Functions

#### `window.GitBook('navigateToPage', path)`

Navigate to a specific page within your GitBook docs by its path.

**Parameters:**

* `path` (string): The path to the page you want to navigate to

**Example:**

```javascript
// Navigate to the getting started guide
window.GitBook('navigateToPage', '/getting-started');

// Navigate to a specific API documentation page
window.GitBook('navigateToPage', '/api/authentication');

// Navigate to FAQ section
window.GitBook('navigateToPage', '/faq/billing');
```

#### `window.GitBook('navigateToAssistant')`

Navigate directly to the AI assistant interface.

**Example:**

```javascript
// Open the assistant chat
window.GitBook('navigateToAssistant');

// You might use this in response to a button click
document.getElementById('help-button').addEventListener('click', () => {
    window.GitBook('navigateToAssistant');
});
```

### Chat Functions

#### `window.GitBook('postUserMessage', message)`

Post a message to the chat as if the user typed it.

**Parameters:**

* `message` (string): The message to post to the chat

**Example:**

```javascript
// Send a predefined message
window.GitBook('postUserMessage', 'How do I reset my password?');

// Send a message based on user action
function askAboutBilling() {
    window.GitBook('postUserMessage', 'I have questions about my billing');
}

// Send a message with context
const userPlan = 'premium';
window.GitBook('postUserMessage', `I'm on the ${userPlan} plan and need help with advanced features`);
```

#### `window.GitBook('clearChat')`

Clear all messages from the current chat session.

**Example:**

```javascript
// Clear the chat
window.GitBook('clearChat');

// Clear chat and start fresh conversation
function startNewConversation() {
    window.GitBook('clearChat');
    window.GitBook('postUserMessage', 'Hello, I need help with a new issue');
}

// Clear chat when switching contexts
document.getElementById('new-topic').addEventListener('click', () => {
    window.GitBook('clearChat');
    window.GitBook('navigateToAssistant');
});
```

### Event Handling

#### `window.GitBook('on', event, listener)`

Register an event listener for GitBook events.

**Parameters:**

* `event` (string): The event name to listen for
* `listener` (function): The callback function to execute when the event occurs

**Example:**

```javascript
// Listen for page navigation
window.GitBook('on', 'navigate', (data) => {
    console.log('Navigated to:', data.path);
    // Update breadcrumbs or analytics
});

// Listen for tool usage
window.GitBook('on', 'tool_used', (data) => {
    console.log('Tool used:', data.toolName);
    // Log tool usage for analytics
});
```
