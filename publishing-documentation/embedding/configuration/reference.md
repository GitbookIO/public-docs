---
description: >-
  Learn more about the methods available to use when working with Docs Embed
  programmatically
---

# API Reference

Docs Embed provides different APIs depending on how you integrate it. This reference covers all available methods across integration methods.

## Method Comparison

| Method | Standalone Script | NPM Package | React Components |
|--------|------------------|-------------|------------------|
| **Initialize** | `GitBook('init', options, frameOptions)` | `createGitBook(options)` | `<GitBookProvider siteURL="...">` |
| **Get frame URL** | ❌ (handled internally) | `client.getFrameURL(options)` | `useGitBook().getFrameURL(options)` |
| **Create frame client** | ❌ (handled internally) | `client.createFrame(iframe)` | `useGitBook().createFrame(iframe)` |
| **Show/Hide widget** | `GitBook('show')` / `GitBook('hide')` | ❌ | ❌ |
| **Open/Close window** | `GitBook('open')` / `GitBook('close')` / `GitBook('toggle')` | ❌ | ❌ |
| **Navigate to page** | `GitBook('navigateToPage', path)` | `frame.navigateToPage(path)` | Via frame client |
| **Navigate to assistant** | `GitBook('navigateToAssistant')` | `frame.navigateToAssistant()` | Via frame client |
| **Post message** | `GitBook('postUserMessage', message)` | `frame.postUserMessage(message)` | Via frame client |
| **Clear chat** | `GitBook('clearChat')` | `frame.clearChat()` | Via frame client |
| **Configure** | `GitBook('configure', settings)` | `frame.configure(settings)` | Props on `<GitBookFrame>` |
| **Event listeners** | ❌ | `frame.on(event, listener)` | Via frame client |
| **Unload** | `GitBook('unload')` | ❌ | ❌ |

## Standalone Script API

### Initialization

#### `GitBook('init', options, frameOptions)`

Initialize the widget with site URL and optional authenticated access.

**Parameters:**

- `options`: `{ siteURL: string }` - Your GitBook docs site URL
- `frameOptions`: `{ visitor?: { token?: string, unsignedClaims?: Record<string, unknown> } }` (optional) - Authenticated access options

**Example:**

```javascript
window.GitBook('init', 
  { siteURL: 'https://docs.company.com' },
  { visitor: { token: 'your-jwt-token' } }
);
```

### Widget Control

#### Show the widget

Display the GitBook widget if it has been hidden.

**Example:**

```js
window.GitBook("show");
```

#### Hide the widget

Hide the GitBook widget without unloading it.

**Example:**

```js
window.GitBook("hide");
```

#### Open the window

Open the Docs Embed window.

**Example:**

```js
window.GitBook("open");
```

#### Close the window

Close the Docs Embed window.

**Example:**

```js
window.GitBook("close");
```

#### Toggle the window

Toggle the Docs Embed window open or closed.

**Example:**

```js
window.GitBook("toggle");
```

#### Unload the widget

Completely remove the GitBook widget from your site.

**Example:**

```js
window.GitBook("unload");
```

### Navigation

#### `GitBook('navigateToPage', path)`

Navigate to a specific page within your GitBook docs by its path.

**Parameters:**

- `path` (string): The path to the page you want to navigate to

**Example:**

```javascript
// Navigate to the getting started guide
window.GitBook("navigateToPage", "/getting-started");

// Navigate to a specific API documentation page
window.GitBook("navigateToPage", "/api/authentication");

// Navigate to FAQ section
window.GitBook("navigateToPage", "/faq/billing");
```

#### `GitBook('navigateToAssistant')`

Navigate directly to the Assistant tab.

**Example:**

```javascript
// Switch to the assistant tab
window.GitBook("navigateToAssistant");

// You might use this in response to a button click
document.getElementById("help-button").addEventListener("click", () => {
  window.GitBook("navigateToAssistant");
});
```

### Chat

#### `GitBook('postUserMessage', message)`

Post a message to the chat as if the user typed it.

**Parameters:**

- `message` (string): The message to post to the chat

**Example:**

```javascript
// Send a predefined message
window.GitBook("postUserMessage", "How do I reset my password?");

// Send a message based on user action
function askAboutBilling() {
  window.GitBook("postUserMessage", "I have questions about my billing");
}

// Send a message with context
const userPlan = "premium";
window.GitBook(
  "postUserMessage",
  `I'm on the ${userPlan} plan and need help with advanced features`
);
```

#### `GitBook('clearChat')`

Clear all messages from the current chat session.

**Example:**

```javascript
// Clear the chat
window.GitBook("clearChat");

// Clear chat and start fresh conversation
function startNewConversation() {
  window.GitBook("clearChat");
  window.GitBook("postUserMessage", "Hello, I need help with a new issue");
}

// Clear chat when switching contexts
document.getElementById("new-topic").addEventListener("click", () => {
  window.GitBook("clearChat");
  window.GitBook("navigateToAssistant");
});
```

### Configuration

#### `GitBook('configure', settings)`

Configure the embed with customization options. See the [Configuration section](../implementation/script.md#configuration-options) for available options.

**Example:**

```javascript
window.GitBook('configure', {
  tabs: ['assistant', 'docs'],
  actions: [
    {
      icon: 'circle-question',
      label: 'Contact Support',
      onClick: () => window.open('https://support.example.com', '_blank')
    }
  ],
  greeting: { title: 'Welcome!', subtitle: 'How can I help?' },
  suggestions: ['What is GitBook?', 'How do I get started?']
});
```

## NPM Package API

### Client Factory

#### `createGitBook(options)`

Create a GitBook client instance.

**Parameters:**

- `options`: `{ siteURL: string }` - Your GitBook docs site URL

**Returns:** `GitBookClient`

**Example:**

```javascript
import { createGitBook } from '@gitbook/embed';

const gitbook = createGitBook({
  siteURL: 'https://docs.company.com'
});
```

#### `client.getFrameURL(options)`

Get the iframe URL with optional authenticated access.

**Parameters:**

- `options`: `{ visitor?: { token?: string, unsignedClaims?: Record<string, unknown> } }` (optional)

**Returns:** `string`

**Example:**

```javascript
const iframeURL = gitbook.getFrameURL({
  visitor: {
    token: 'your-jwt-token',
    unsignedClaims: { userId: '123', plan: 'premium' }
  }
});
```

#### `client.createFrame(iframe)`

Create a frame client to communicate with the iframe.

**Parameters:**

- `iframe`: `HTMLIFrameElement` - The iframe element

**Returns:** `GitBookFrameClient`

**Example:**

```javascript
const iframe = document.createElement('iframe');
iframe.src = gitbook.getFrameURL();
const frame = gitbook.createFrame(iframe);
```

### Frame Client Methods

#### `frame.navigateToPage(path)`

Navigate to a specific page in the docs tab.

**Parameters:**

- `path`: `string` - The path to the page

#### `frame.navigateToAssistant()`

Switch to the assistant tab.

#### `frame.postUserMessage(message)`

Post a message to the chat.

**Parameters:**

- `message`: `string` - The message to post

#### `frame.clearChat()`

Clear chat history.

#### `frame.configure(settings)`

Configure the embed. See the [Configuration section](../implementation/nodejs.md#configuration-options) for available options.

#### `frame.on(event, listener)`

Register an event listener.

**Parameters:**

- `event`: `string` - The event name
- `listener`: `Function` - The callback function

**Returns:** `() => void` - Unsubscribe function

**Example:**

```javascript
const unsubscribe = frame.on('close', () => {
  console.log('Frame closed');
});

// Later, unsubscribe
unsubscribe();
```

## React Components API

See the [React integration guide](../implementation/react.md) for component props and the `useGitBook` hook API.

