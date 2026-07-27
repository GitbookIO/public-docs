---
description: Reference for the Docs Embed API.
---

# Embed API reference

The Docs Embed exposes different APIs depending on your [integration method](install-the-embed.md). This reference covers every available method across all three.

## Method comparison

| Method | Standalone Script | NPM Package | React Components |
|---|---|---|---|
| **Initialize** | `GitBook('init', options, frameOptions)` | `createGitBook(options)` | `<GitBookProvider siteURL="...">` |
| **Color scheme override** | `GitBook('init', options, { colorScheme })` | `client.getFrameURL({ colorScheme })` | `<GitBookFrame colorScheme="..." />` |
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

See [Customize the embed](customize-the-embed/README.md) for what each configuration setting does.

## Standalone script API

### `GitBook('init', options, frameOptions)`

Initialize the widget with a site URL and optional authenticated access.

* `options`: `{ siteURL: string }` — your GitBook docs site URL.
* `frameOptions` *(optional)*: `{ visitor?: { token?: string, unsignedClaims?: Record<string, unknown> }, colorScheme?: 'light' | 'dark' }`.

```javascript
window.GitBook('init',
  { siteURL: 'https://docs.company.com' },
  { visitor: { token: 'your-jwt-token' }, colorScheme: 'dark' }
);
```

When omitted, `colorScheme` follows the iframe's CSS `color-scheme`.

### Widget control

* `GitBook("show")` — display the widget if hidden.
* `GitBook("hide")` — hide the widget without unloading it.
* `GitBook("open")` — open the embed window.
* `GitBook("close")` — close the embed window.
* `GitBook("toggle")` — toggle the embed window open or closed.
* `GitBook("unload")` — completely remove the widget from your site.

### Navigation

* `GitBook('navigateToPage', path)` — navigate to a page by path.

  ```javascript
  window.GitBook("navigateToPage", "/getting-started");
  window.GitBook("navigateToPage", "/api/authentication");
  ```

* `GitBook('navigateToAssistant')` — switch to the Assistant tab.

  ```javascript
  document.getElementById("help-button").addEventListener("click", () => {
    window.GitBook("navigateToAssistant");
  });
  ```

### Chat

* `GitBook('postUserMessage', message)` — post a message to the chat as if the user typed it.

  ```javascript
  window.GitBook("postUserMessage", "How do I reset my password?");
  ```

* `GitBook('clearChat')` — clear all messages from the current chat session.

  ```javascript
  window.GitBook("clearChat");
  window.GitBook("postUserMessage", "Hello, I need help with a new issue");
  ```

### Configuration

* `GitBook('configure', settings)` — configure the embed. See [Customize the embed](customize-the-embed/README.md) for available settings.

  ```javascript
  window.GitBook('configure', {
    trademark: false,
    tabs: ['assistant', 'search', 'docs'],
    actions: [
      {
        icon: 'circle-question',
        label: 'Contact Support',
        onClick: () => window.open('https://support.example.com', '_blank')
      }
    ],
    greeting: { title: 'Welcome!', subtitle: 'How can I help?' },
    assistantName: 'Support Copilot',
    closeButton: true,
    suggestions: ['What is GitBook?', 'How do I get started?']
  });
  ```

## NPM package API

### `createGitBook(options)`

Create a GitBook client instance. `options`: `{ siteURL: string }`. Returns a `GitBookClient`.

```javascript
import { createGitBook } from '@gitbook/embed';

const gitbook = createGitBook({
  siteURL: 'https://docs.company.com'
});
```

### `client.getFrameURL(options)`

Get the iframe URL with optional authenticated access. `options` *(optional)*: `{ visitor?: { token?: string, unsignedClaims?: Record<string, unknown> }, colorScheme?: 'light' | 'dark' }`. Returns a `string`.

```javascript
const iframeURL = gitbook.getFrameURL({
  colorScheme: 'dark',
  visitor: {
    token: 'your-jwt-token',
    unsignedClaims: { userId: '123', plan: 'premium' }
  }
});
```

### `client.createFrame(iframe)`

Create a frame client to communicate with the iframe. `iframe`: `HTMLIFrameElement`. Returns a `GitBookFrameClient`.

```javascript
const iframe = document.createElement('iframe');
iframe.src = gitbook.getFrameURL();
const frame = gitbook.createFrame(iframe);
```

### Frame client methods

* `frame.navigateToPage(path: string)` — navigate to a page in the docs tab.
* `frame.navigateToAssistant()` — switch to the assistant tab.
* `frame.postUserMessage(message: string)` — post a message to the chat.
* `frame.clearChat()` — clear chat history.
* `frame.configure(settings)` — configure the embed. See [Customize the embed](customize-the-embed/README.md).
* `frame.on(event: string, listener: Function)` — register an event listener. Returns an unsubscribe function.

  ```javascript
  const unsubscribe = frame.on('close', () => {
    console.log('Frame closed');
  });

  // Later, unsubscribe
  unsubscribe();
  ```

## React components API

See [Install the embed](install-the-embed.md#react) for `<GitBookProvider>` and `<GitBookFrame>` setup.

**`GitBookProvider` props:**

| Prop | Type | Required | Description |
|---|---|---|---|
| `siteURL` | `string` | Yes | Your GitBook docs site URL. |
| `children` | `ReactNode` | Yes | Child components to render within the provider. |

**`GitBookFrame` props** (in addition to the settings in [Customize the embed](customize-the-embed/README.md)):

| Prop | Type | Default | Description |
|---|---|---|---|
| `className` | `string` | `null` | CSS class name for the frame container. |
| `style` | `object` | `{}` | Inline styles for the frame container. |
| `colorScheme` | `'light' \| 'dark'` | Inherits from CSS `color-scheme` | Override the embed color scheme. |
| `assistantName` | `string` | `null` | Override the assistant name shown in the UI. |
| `closeButton` | `boolean` | `null` | Display a close button inside the Assistant. |
| `visitor` | `object` | `{}` | Authenticated access options. |

**`useGitBook()` hook** returns a `GitBookClient` with:

* `getFrameURL(options?: { visitor?, colorScheme? })` → `string`
* `createFrame(iframe: HTMLIFrameElement)` → `GitBookFrameClient`, which provides `navigateToPage()`, `navigateToAssistant()`, `postUserMessage()`, `clearChat()`, `configure()`, and `on()`.
