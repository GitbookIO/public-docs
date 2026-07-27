---
description: Install the Docs Embed with a script tag, Node.js, or React.
---

# Install the embed

Choose the integration method that matches your setup. If your docs use [authenticated access](authenticate-the-embed.md), follow those steps alongside whichever method you pick here.

{% tabs %}
{% tab title="Script tag" %}
The simplest way to add the embed — no SDK, build step, or framework integration required.

{% stepper %}
{% step %}
#### Copy your embed script URL

In the GitBook app, go to your docs site's **Settings → AI & MCP** and copy the embed script URL, or build it manually:

```
https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js
```
{% endstep %}

{% step %}
#### Add the script to your HTML

Add this inside `<head>` or just before `</body>`:

```html
<script src="https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js"></script>
<script>window.GitBook('show');</script>
```
{% endstep %}

{% step %}
#### If your docs require authentication

Append a signed JWT token as a query parameter:

```html
<script src="https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js?jwt_token=YOUR_TOKEN"></script>
```

See [Authenticate the embed](authenticate-the-embed.md) for how to obtain this token.
{% endstep %}

{% step %}
#### Verify

Reload your page — the widget should appear in the bottom-right corner.
{% endstep %}
{% endstepper %}

Once loaded, you can control it at runtime:

```html
<script>
  window.GitBook('show');   // Make the widget visible
  window.GitBook('hide');   // Remove the widget from the page
  window.GitBook('open');   // Open the widget panel
  window.GitBook('close');  // Close the widget panel
  window.GitBook('toggle'); // Toggle open or closed
</script>
```

Or drive it programmatically:

```html
<script>
  window.GitBook('navigateToPage', '/getting-started'); // Open a specific docs page
  window.GitBook('navigateToAssistant');                // Switch to the assistant tab
  window.GitBook('postUserMessage', 'How do I get started?'); // Send a message
  window.GitBook('clearChat');                          // Clear chat history
</script>
```

If you need to load the script conditionally (after user action, or a feature flag), inject it dynamically instead of hardcoding the tag:

```html
<script>
  function loadGitBookEmbed() {
    var token = "" // Fill it with your JWT token if your site requires an auth
    var script = document.createElement('script');
    script.src = 'https://YOUR_DOCS_DOMAIN/~gitbook/embed/script.js'
      + (token ? '?jwt_token=' + encodeURIComponent(token) : '');
    script.async = true;
    script.onload = function () {
      window.GitBook('show');
    };
    document.head.appendChild(script);
  }

  loadGitBookEmbed();
</script>
```

See [Customize the embed](customize-the-embed/README.md) to configure the button, tabs, greeting, and more, and the [API reference](embed-api-reference.md) for every available method.

**Common pitfalls:** using the example `docs.company.com` instead of your real domain; calling `GitBook(...)` before the script has loaded (wrap calls in `script.onload`, or place them after the tag); missing `visitor.token` on authenticated docs; a Content Security Policy that blocks your GitBook domain; z-index conflicts hiding the widget; forgetting to call `GitBook('init', ...)` before other methods, if you're using it.
{% endtab %}

{% tab title="Node.js/NPM" %}
Install the embed package from npm for application-level control — ideal for server-side rendering, build-time integration, or custom iframe management.

{% stepper %}
{% step %}
#### Install the package

```bash
npm install @gitbook/embed
```
{% endstep %}

{% step %}
#### Import it

```javascript
import { createGitBook } from "@gitbook/embed";
```

Or with CommonJS: `const { createGitBook } = require("@gitbook/embed");`
{% endstep %}

{% step %}
#### Initialize GitBook

```javascript
const gitbook = createGitBook({
  siteURL: "https://docs.company.com",
});
```
{% endstep %}

{% step %}
#### Create an iframe

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
iframe.allow = "clipboard-write";
```

{% hint style="info" %}
If you use the Assistant tab, set `allow="clipboard-write"` on the iframe — the NPM package leaves iframe setup to you (the script tag implementation adds this automatically).
{% endhint %}
{% endstep %}

{% step %}
#### Attach the frame

```javascript
const frame = gitbook.createFrame(iframe);
document.getElementById("gitbook-embed-container").appendChild(iframe);
```
{% endstep %}

{% step %}
#### Control it programmatically

```javascript
frame.navigateToPage("/getting-started"); // Navigate to a specific page
frame.navigateToAssistant();              // Switch to the assistant tab
frame.postUserMessage("How do I get started?"); // Post a message to the chat
frame.clearChat();                        // Clear chat history
```
{% endstep %}

{% step %}
#### Listen to events

```javascript
frame.on('close', () => {
  console.log('Frame closed');
});

// Unsubscribe when done
const unsubscribe = frame.on('navigate', (data) => {
  console.log('Navigated to:', data.path);
});
```
{% endstep %}
{% endstepper %}

See [Customize the embed](customize-the-embed/README.md) for `frame.configure(...)` options, and the [API reference](embed-api-reference.md) for the full client and frame API.

**Common pitfalls:** forgetting `npm install @gitbook/embed` before importing; a missing or mismatched `siteURL`; an iframe container without enough width/height; calling frame methods before `createFrame()` completes; not unsubscribing from `frame.on()` listeners (memory leaks); reaching for `open()`/`close()`/`toggle()`/`destroy()` — those are script-tag-only, use the frame client methods instead.
{% endtab %}

{% tab title="React" %}
Prebuilt React components handle state, context, and lifecycle for you.

{% stepper %}
{% step %}
#### Install the package

```bash
npm install @gitbook/embed
```
{% endstep %}

{% step %}
#### Import the components

```jsx
import {
  GitBookProvider,
  GitBookFrame,
} from "@gitbook/embed/react";
```
{% endstep %}

{% step %}
#### Wrap your app with GitBookProvider

```jsx
function App() {
  return (
    <GitBookProvider siteURL="https://docs.company.com">
      <YourAppContent />
    </GitBookProvider>
  );
}
```
{% endstep %}

{% step %}
#### Add the GitBookFrame component

```jsx
function App() {
  return (
    <GitBookProvider siteURL="https://docs.company.com">
      <div className="app">
        <YourAppContent />
        <GitBookFrame
          visitor={{
            token: 'your-jwt-token', // Optional: for Adaptive Content or Authenticated Access
            unsignedClaims: { userId: '123' } // Optional: custom claims for dynamic expressions
          }}
        />
      </div>
    </GitBookProvider>
  );
}
```

{% hint style="info" %}
If you use the Assistant tab, set `allow="clipboard-write"` on the iframe that renders the embed — React integrations leave iframe setup to your app (the script tag implementation adds this automatically).
{% endhint %}
{% endstep %}

{% step %}
#### Control it with the useGitBook hook

```jsx
import { useGitBook } from "@gitbook/embed/react";

function HelpButton() {
  const gitbook = useGitBook();
  const frameURL = gitbook.getFrameURL({ visitor: { token: '...' } });

  const handleNavigate = () => {
    const iframe = document.createElement('iframe');
    iframe.src = frameURL;
    iframe.allow = 'clipboard-write';
    const frame = gitbook.createFrame(iframe);
    frame.navigateToPage('/getting-started');
    frame.navigateToAssistant();
    frame.postUserMessage('How do I get started?');
  };

  return <button onClick={handleNavigate}>Get Help</button>;
}
```
{% endstep %}

{% step %}
#### Conditionally render the embed

```jsx
function App() {
  const [showEmbed, setShowEmbed] = useState(false);

  return (
    <GitBookProvider siteURL="https://docs.company.com">
      <button onClick={() => setShowEmbed(true)}>Get Help</button>
      {showEmbed && <GitBookFrame />}
    </GitBookProvider>
  );
}
```
{% endstep %}

{% step %}
#### Use with Next.js or other SSR frameworks

Dynamically import the components to avoid SSR issues:

```jsx
import dynamic from "next/dynamic";

const GitBookProvider = dynamic(
  () => import("@gitbook/embed/react").then((mod) => mod.GitBookProvider),
  { ssr: false }
);

const GitBookFrame = dynamic(
  () => import("@gitbook/embed/react").then((mod) => mod.GitBookFrame),
  { ssr: false }
);
```
{% endstep %}
{% endstepper %}

See [Customize the embed](customize-the-embed/README.md) for the full list of `<GitBookFrame>` props, and the [API reference](embed-api-reference.md) for the `useGitBook` hook's methods.

**Common pitfalls:** rendering `<GitBookFrame>` without a parent `<GitBookProvider>`; skipping dynamic import under SSR; a `siteURL` that doesn't match your live docs site exactly; calling `useGitBook()` outside a `GitBookProvider`; nesting multiple providers (context conflicts); looking for `GitBookAssistantFrame` — the component is now `GitBookFrame`.
{% endtab %}
{% endtabs %}
