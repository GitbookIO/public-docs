---
description: >-
  Integrate Docs Embed using the NPM package for full application-level
  control
---

# Node.js/NPM

If you need more control and want to work at the application level, you can install the GitBook embed package from npm. This approach is ideal for server-side rendering, build-time integration, or custom iframe management.

## Steps

1.  **Install the package**

    Add `@gitbook/embed` to your project:

    ```bash
    npm install @gitbook/embed
    ```

    For the complete API reference and source code, see the [`@gitbook/embed` package on GitHub](https://github.com/GitbookIO/gitbook/tree/main/packages/embed).

2.  **Import the package**

    In your application code, import the `createGitBook` function:

    ```javascript
    import { createGitBook } from "@gitbook/embed";
    ```

    Or using CommonJS:

    ```javascript
    const { createGitBook } = require("@gitbook/embed");
    ```
3.  **Initialize GitBook**

    Create a GitBook instance with your docs site URL:

    ```javascript
    const gitbook = createGitBook({
      siteURL: "https://docs.company.com",
    });
    ```
4.  **Create an iframe**

    Generate an iframe element and set its source to the embed URL:

    ```javascript
    const iframe = document.createElement("iframe");
    iframe.src = gitbook.getFrameURL({
      visitor: {
        token: 'your-jwt-token', // Optional: for Adaptive Content or Authenticated Access
        unsignedClaims: { // Optional: custom claims for dynamic expressions
          userId: '123',
          plan: 'premium'
        }
      }
    });
    iframe.id = "gitbook-embed-container";
    iframe.style.border = "none";
    iframe.style.width = "100%";
    iframe.style.height = "600px";
    ```
5.  **Attach the frame**

    Create a GitBook frame instance and mount it to your page:

    ```javascript
    const frame = gitbook.createFrame(iframe);
    document.getElementById("gitbook-embed-container").appendChild(iframe);
    ```
6.  **Control the embed programmatically**

    Use the frame instance to interact with the embed:

    ```javascript
    // Navigate to a specific page in the docs tab
    frame.navigateToPage("/getting-started");

    // Switch to the assistant tab
    frame.navigateToAssistant();

    // Post a message to the chat
    frame.postUserMessage("How do I get started?");

    // Clear chat history
    frame.clearChat();
    ```
7.  **Configure the embed**

    Configure the embed with customization options:

    ```javascript
    frame.configure({
      tabs: ['assistant', 'docs'],
      actions: [
        {
          icon: 'circle-question',
          label: 'Contact Support',
          onClick: () => window.open('https://support.example.com', '_blank')
        }
      ],
      greeting: { title: 'Welcome!', subtitle: 'How can I help?' },
      suggestions: ['What is GitBook?', 'How do I get started?'],
      tools: [/* ... */]
    });
    ```
8.  **Listen to events**

    Register event listeners to respond to embed events:

    ```javascript
    frame.on('close', () => {
      console.log('Frame closed');
    });

    // Unsubscribe when done
    const unsubscribe = frame.on('navigate', (data) => {
      console.log('Navigated to:', data.path);
    });
    ```

## API Reference

### Client Factory

- `createGitBook(options: { siteURL: string })` → `GitBookClient`
- `client.getFrameURL(options?: { visitor?: {...} })` → `string` - Get the iframe URL with optional authenticated access
- `client.createFrame(iframe: HTMLIFrameElement)` → `GitBookFrameClient` - Create a frame client to communicate with the iframe

### Frame Client Methods

- `frame.navigateToPage(path: string)` → `void` - Navigate to a specific page in the docs tab
- `frame.navigateToAssistant()` → `void` - Switch to the assistant tab
- `frame.postUserMessage(message: string)` → `void` - Post a message to the chat
- `frame.clearChat()` → `void` - Clear chat history
- `frame.configure(settings: Partial<GitBookEmbeddableConfiguration>)` → `void` - Configure the embed
- `frame.on(event: string, listener: Function)` → `() => void` - Register event listener (returns unsubscribe function)

## Configuration Options

Configuration options are available via `frame.configure({...})`:

### `tabs`

Override which tabs are displayed. Defaults to your site's configuration.

- **Type**: `('assistant' | 'docs')[]`

### `actions`

Custom action buttons rendered in the sidebar alongside tabs. Each action button triggers a callback when clicked.

**Note**: This was previously named `buttons`. Use `actions` instead.

- **Type**: `Array<{ icon: string, label: string, onClick: () => void }>`

### `greeting`

Welcome message displayed in the Assistant tab.

- **Type**: `{ title: string, subtitle: string }`

### `suggestions`

Suggested questions displayed in the Assistant welcome screen.

- **Type**: `string[]`

### `tools`

Custom AI tools to extend the Assistant. See [Creating custom tools](../configuration/creating-custom-tools.md) for details.

- **Type**: `Array<{ name: string, description: string, inputSchema: object, execute: Function, confirmation?: {...} }>`

### `visitor` (Authenticated Access)

Pass to `getFrameURL({ visitor: {...} })`. Used for [Adaptive Content](../../adaptive-content/README.md) and [Authenticated Access](../../authenticated-access/README.md).

- **Type**: `{ token?: string, unsignedClaims?: Record<string, unknown> }`

## Common pitfalls

* **Forgetting to install the package** – Run `npm install @gitbook/embed` before importing.
* **Missing siteURL** – The `siteURL` option is required and must match your published docs site.
* **iFrame not rendering** – Ensure the parent container has sufficient width/height for the iframe to display.
* **Frame methods called before initialization** – Wait until `createFrame()` completes before calling frame methods.
* **Not unsubscribing from events** – Remember to call the unsubscribe function returned by `frame.on()` to prevent memory leaks.
* **Using old API methods** – Methods like `open()`, `close()`, `toggle()`, and `destroy()` are not available in the NPM package. Use the frame client methods instead.

