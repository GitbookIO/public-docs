---
description: >-
  Learn how to add the Docs Embed widget to any website or web app using a
  single script tag
---

# Script tag

The simplest integration method for embedding GitBook Assistant into your website or app is a standalone script that you include in your HTML. Each GitBook docs site provides a ready to use embed script that loads the widget automatically and connects it to your docs. This page tells you how to do that.

No SDK, build step, or framework integration is required. Just include the script and the widget appears on your page.

## Get started

{% stepper %}
{% step %}
### Copy your embed script URL

Navigate to your docs site in the GitBook app, navigate to the **Settings** tab and then to **AI & MCP** and copy the embed script URL.

You can also build it manually:

```
https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js
```

Replace your `YOUR_DOCS_DOMAIN` with your real docs site’s domain.
{% endstep %}

{% step %}
### Add the script to your HTML

Add the following tag in your page HTML. Put it inside `<head>` or just before `</body>`.

```html
<script src="https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js"></script>
<script>window.GitBook('show');</script>
```
{% endstep %}

{% step %}
### If your docs require authentication

If your docs [are behind auth](../../authenticated-access/), the script must include a signed JWT token.

Append it as a query parameter:

```html
<script src="https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js?jwt_token=YOUR_TOKEN"></script>
```
{% endstep %}

{% step %}
### Verify

Reload your page.

The widget should appear in the bottom right corner.
{% endstep %}
{% endstepper %}

### Optionally configure the embed

You can customize the widget before displaying it. Call `configure` after loading the script and before calling `window.GitBook('show')`.

```html
<script src="https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js"></script>
<script>
  window.GitBook('configure', {
    button: {
      label: 'Ask',
      icon: 'assistant' // assistant | sparkle | help | book
    },
    tabs: ['assistant', 'docs'],
    actions: [
      {
        icon: 'circle-question',
        label: 'Contact support',
        onClick: () => window.open('https://support.example.com', '_blank')
      }
    ],
    greeting: {
      title: 'Welcome',
      subtitle: 'How can I help?'
    },
    suggestions: [
      'What is GitBook?',
      'How do I get started?'
    ]
  });

  window.GitBook('show');
</script>
```

Using this method, you can customize the:

* Button label and icon
* Visible tabs inside the widget
* Custom action buttons
* Greeting title and subtitle
* Suggested prompts shown to users.

### Control widget visibility

You can control visibility and state at runtime through the API.

```html
<script>
  // Make the widget visible
  window.GitBook('show');

  // Remove the widget from the page
  window.GitBook('hide');

  // Open the widget panel
  window.GitBook('open');

  // Close the widget panel
  window.GitBook('close');

  // Toggle open or closed
  window.GitBook('toggle');
</script>
```

This is useful when you want to connect the widget to your own UI triggers.

### Navigate and interact programmatically

You can drive the widget from your code to navigate, switch tabs, or send messages.

```html
<script>
  // Open a specific docs page inside the widget
  window.GitBook('navigateToPage', '/getting-started');

  // Switch to the assistant tab
  window.GitBook('navigateToAssistant');

  // Send a user message to the assistant
  window.GitBook('postUserMessage', 'How do I get started?');

  // Clear the current chat history
  window.GitBook('clearChat');
</script>
```

Typical uses for this functionality include:

* Adding a deep link to a docs page from your app
* Pre-filling a question
* Resetting the conversation between flows

### Load the embed script dynamically

If you only want to load the widget conditionally, or you need to attach an auth token at runtime, inject the script programmatically.

```html
<script>
  function loadGitBookEmbed() {
    var token = "" // Fill it with your JWT token if your site requires an auth
    var script = document.createElement('script');
    script.src = 'https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js'
      + token ? '?jwt_token=' + encodeURIComponent(token) : ';
    script.async = true;
    script.onload = function () {
      window.GitBook('show');
    };
    document.head.appendChild(script);
  }

  loadGitBookEmbed();
</script>
```

Use this pattern when the widget should load only after user action or feature flags

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

{% hint style="info" %}
**Note:** This option is only available when using the standalone script tag implementation. For React or Node.js implementations, you'll need to create your own button to trigger the embed.
{% endhint %}

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
