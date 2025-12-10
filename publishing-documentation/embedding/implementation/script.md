---
description: Add Docs Embed to any website with a simple script tag
---

# Script tag

The quickest way to add Docs Embed to your website or app is by adding it through a "standalone" script tag. Every docs site in GitBook includes a ready-to-use script for embedding your docs as a widget.

## Steps

{% stepper %}
{% step %}
#### Get your embed script URL

Navigate to your docs site's **Settings** → **AI & MCP** tab and copy the script URL, or use the script at `https://docs.company.com/~gitbook/embed/script.js` (replace `docs.company.com` with your actual docs site URL).
{% endstep %}

{% step %}
#### Add the script tag to your HTML

Place this code in your HTML `<head>` or before the closing `</body>` tag:

```html
<script src="https://docs.company.com/~gitbook/embed/script.js"></script>
<script>
  // Initialize with Authenticated Access (optional)
  window.GitBook('init', 
    { siteURL: 'https://docs.company.com' },
    { visitor: { token: 'your-jwt-token' } }
  );
  window.GitBook('show');
</script>
```
{% endstep %}

{% step %}
#### Replace the docs URL

Update `docs.company.com` with your actual docs site URL.
{% endstep %}

{% step %}
#### Test the widget

Load your page. The embed widget should appear in the bottom-right corner.
{% endstep %}

{% step %}
#### Optionally configure the embed

Add customization options before calling `show()`:

```html
<script src="https://docs.company.com/~gitbook/embed/script.js"></script>
<script>
  window.GitBook('init', { siteURL: 'https://docs.company.com' });
  
  window.GitBook('configure', {
    button: {
      label: 'Ask',
      icon: 'assistant' // 'assistant' | 'sparkle' | 'help' | 'book'
    },
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
  
  window.GitBook('show');
</script>
```
{% endstep %}

{% step %}
#### Control widget visibility

Use the API to show, hide, open, or close the embed:

```html
<script>
  // Show the widget
  window.GitBook("show");

  // Hide the widget
  window.GitBook("hide");

  // Open the embed window
  window.GitBook("open");

  // Close the embed window
  window.GitBook("close");

  // Toggle the embed window
  window.GitBook("toggle");
</script>
```
{% endstep %}

{% step %}
#### Navigate and interact programmatically

Use the API to navigate to pages, switch tabs, or post messages:

```html
<script>
  // Navigate to a specific page in the docs tab
  window.GitBook('navigateToPage', '/getting-started');

  // Switch to the assistant tab
  window.GitBook('navigateToAssistant');

  // Post a message to the chat
  window.GitBook('postUserMessage', 'How do I get started?');

  // Clear chat history
  window.GitBook('clearChat');
</script>
```
{% endstep %}

{% step %}
#### Load dynamically (optional)

For authenticated docs or conditional loading, inject the script at runtime:

```html
<script>
  function loadGitBookEmbed() {
    var script = document.createElement("script");
    script.src = "https://docs.company.com/~gitbook/embed/script.js";
    script.async = true;
    script.onload = function () {
      window.GitBook('init', { siteURL: 'https://docs.company.com' });
      window.GitBook("show");
    };
    document.head.appendChild(script);
  }

  // Load when ready
  loadGitBookEmbed();
</script>
```
{% endstep %}

{% step %}
#### Verify the setup

Open your browser console and type `window.GitBook` to confirm the API is available.
{% endstep %}
{% endstepper %}

## API Reference

### Initialization

* `GitBook('init', options: { siteURL: string }, frameOptions?: { visitor?: {...} })` - Initialize widget with site URL and optional authenticated access

### Widget Control

* `GitBook('show')` - Show widget button
* `GitBook('hide')` - Hide widget button
* `GitBook('open')` - Open widget window
* `GitBook('close')` - Close widget window
* `GitBook('toggle')` - Toggle widget window

### Navigation

* `GitBook('navigateToPage', path: string)` - Navigate to a specific page in the docs tab
* `GitBook('navigateToAssistant')` - Navigate to the assistant tab

### Chat

* `GitBook('postUserMessage', message: string)` - Post a message to the chat
* `GitBook('clearChat')` - Clear chat history

### Configuration

* `GitBook('configure', settings: {...})` - Configure widget settings (see Configuration section below)
* `GitBook('unload')` - Completely remove the widget from the page

## Configuration Options

Configuration options are available via `GitBook('configure', {...})`:

### `tabs`

Override which tabs are displayed. Defaults to your site's configuration.

* **Type**: `('assistant' | 'docs')[]`
* **Options**:
  * `['assistant', 'docs']` - Show both tabs
  * `['assistant']` - Show only the assistant tab
  * `['docs']` - Show only the docs tab

### `actions`

Custom action buttons rendered in the sidebar alongside tabs. Each action button triggers a callback when clicked.

**Note**: This was previously named `buttons`. Use `actions` instead.

* **Type**: `Array<{ icon: string, label: string, onClick: () => void }>`
* **Properties**:
  * `icon`: `string` - Icon name. Any [FontAwesome icon](https://fontawesome.com/search) is supported
  * `label`: `string` - Button label text
  * `onClick`: `() => void | Promise<void>` - Callback function when clicked

### `greeting`

Welcome message displayed in the Assistant tab.

* **Type**: `{ title: string, subtitle: string }`

### `suggestions`

Suggested questions displayed in the Assistant welcome screen.

* **Type**: `string[]`

### `tools`

Custom AI tools to extend the Assistant. See [Creating custom tools](../configuration/creating-custom-tools.md) for details.

* **Type**: `Array<{ name: string, description: string, inputSchema: object, execute: Function, confirmation?: {...} }>`

### `button`

Configure the widget button that launches the embed (standalone script only). This allows you to customize the label and icon of the button that appears in the bottom-right corner of your page.

* **Type**: `{ label: string, icon: 'assistant' | 'sparkle' | 'help' | 'book' }`
* **Properties**:
  * `label`: `string` - The text displayed on the button
  * `icon`: `'assistant' | 'sparkle' | 'help' | 'book'` - The icon displayed on the button
    * `assistant` - <i class="fa-gitbook-assistant">:gitbook-assistant:</i> Assistant icon
    * `sparkle` - <i class="fa-sparkle">:sparkle:</i> Sparkle icon
    * `help` - <i class="fa-circle-question">:circle-question:</i> Help/question icon
    * `book` - <i class="fa-book-open">:book-open:</i> Book icon

**Example:**

```javascript
window.GitBook('configure', {
  button: {
    label: 'Ask',
    icon: 'assistant'
  }
});
```

**Note:** This option is only available when using the standalone script tag implementation. For React or Node.js implementations, you'll need to create your own button to trigger the embed.

### `visitor` (Authenticated Access)

Pass when initializing with `GitBook('init', options, frameOptions)`. Used for [Adaptive Content](../../adaptive-content/) and [Authenticated Access](../../authenticated-access/).

* **Type**: `{ token?: string, unsignedClaims?: Record<string, unknown> }`
* **Properties**:
  * `token`: `string` (optional) - Signed JWT token
  * `unsignedClaims`: `Record<string, unknown>` (optional) - Unsigned claims for dynamic expressions

## Common pitfalls

* **Script URL is incorrect** – Ensure you're using your actual docs URL, not the example `docs.company.com`.
* **Calling GitBook before script loads** – Wrap API calls in `script.onload` or place them after the script tag.
* **Authenticated docs not accessible** – If your docs require sign-in, you must provide the `visitor.token` when initializing. See [Using with authenticated docs](../authentication/using-with-authenticated-docs.md).
* **CORS or CSP errors** – Ensure your site's Content Security Policy allows loading scripts and iframes from your GitBook domain.
* **Widget not visible** – Check z-index conflicts with other elements on your page. The widget uses a high z-index by default.
* **Forgetting to initialize** – Make sure to call `GitBook('init', { siteURL: '...' })` before using other methods.
