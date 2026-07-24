---
name: gitbook-embed
description: Use this skill when the user wants to embed GitBook Assistant or the Docs Embed widget into a product, website, or app. Triggers include mentions of "GitBook Assistant embed", "embeddable assistant", "embed docs", "Docs Embed", or requests to add an AI chat widget powered by GitBook to a codebase. Covers all three implementation methods (script tag, NPM/Node.js, React) plus authentication, configuration, and custom tools.
---

# GitBook Docs Embed

The **Docs Embed** (also called the Embeddable Assistant) lets you embed GitBook's AI assistant and/or docs browser directly into any product or website. Users can ask questions or browse docs without leaving the app.

The embed has two tabs:
- **Assistant** — AI-powered chat (requires GitBook Assistant enabled on the site)
- **Docs** — browsable documentation

## Prerequisites

1. Docs site must be **published** (e.g., `https://docs.yourcompany.com`)
2. GitBook Assistant must be **enabled** on the site: Settings → AI & MCP
3. Get the embed script URL from: Settings → AI & MCP → Embed

---

## Implementation

Choose one method based on the user's stack.

### Method 1: Standalone Script Tag (quickest)

Best for plain HTML sites or any context where dropping in a `<script>` tag is easiest. Adds a floating button in the bottom-right corner automatically.

```html
<script src="https://docs.yourcompany.com/~gitbook/embed/script.js"></script>
<script>
  window.GitBook('init', { siteURL: 'https://docs.yourcompany.com' });
  window.GitBook('configure', {
    button: { label: 'Ask', icon: 'assistant' }, // icon: 'assistant' | 'sparkle' | 'help' | 'book'
    tabs: ['assistant', 'docs'],
    greeting: { title: 'Hi there!', subtitle: 'How can I help?' },
    suggestions: ['How do I get started?', 'What are your pricing plans?'],
    actions: [
      {
        icon: 'circle-question',
        label: 'Contact Support',
        onClick: () => window.open('https://support.yourcompany.com', '_blank'),
      },
    ],
  });
  window.GitBook('show');
</script>
```

**Script tag imperative API:**
```js
window.GitBook('show');              // Show the floating button
window.GitBook('hide');              // Hide it
window.GitBook('open');              // Open the embed panel
window.GitBook('close');             // Close it
window.GitBook('toggle');            // Toggle open/close
window.GitBook('navigateToPage', '/getting-started');  // Go to a docs page
window.GitBook('navigateToAssistant');                 // Switch to Assistant tab
window.GitBook('postUserMessage', 'How do I reset my password?'); // Send a chat message
window.GitBook('clearChat');         // Clear chat history
```

> **Common pitfalls:**
> - Script URL must use your real docs domain, not `docs.company.com`
> - Call `GitBook()` methods after the script loads (use `script.onload` if loading dynamically)
> - If docs require auth, pass `visitor.token` on init (see Authentication section)

---

### Method 2: NPM Package (Node.js / build-time)

Best for SSR, custom iframe placement, or full programmatic control.

```bash
npm install @gitbook/embed
```

```js
import { createGitBook } from '@gitbook/embed';

const gitbook = createGitBook({ siteURL: 'https://docs.yourcompany.com' });

// Create and mount iframe
const iframe = document.createElement('iframe');
iframe.src = gitbook.getFrameURL(); // pass { visitor: { token } } for auth
iframe.style.cssText = 'border:none; width:100%; height:600px;';
document.getElementById('gitbook-container').appendChild(iframe);

// Get frame client for programmatic control
const frame = gitbook.createFrame(iframe);

// Configure
frame.configure({
  tabs: ['assistant', 'docs'],
  greeting: { title: 'Hi there!', subtitle: 'How can I help?' },
  suggestions: ['How do I get started?'],
  actions: [
    { icon: 'circle-question', label: 'Contact Support', onClick: () => window.open('https://support.yourcompany.com') },
  ],
  tools: [/* custom tools */],
});

// Frame methods
frame.navigateToPage('/getting-started');
frame.navigateToAssistant();
frame.postUserMessage('How do I get started?');
frame.clearChat();

// Events
const unsubscribe = frame.on('navigate', (data) => console.log('Navigated to:', data.path));
frame.on('close', () => console.log('Frame closed'));
// Call unsubscribe() to remove the listener when done
```

> **Common pitfalls:**
> - `siteURL` is required and must match the published docs URL exactly
> - Call frame methods only after `createFrame()` completes
> - Unsubscribe event listeners to avoid memory leaks
> - `open()`, `close()`, `toggle()`, `destroy()` are **not** available in the NPM package

---

### Method 3: React Components

Best for React apps. Uses `GitBookProvider` + `GitBookFrame` components.

```bash
npm install @gitbook/embed
```

```tsx
import { GitBookProvider, GitBookFrame } from '@gitbook/embed/react';

function App() {
  return (
    <GitBookProvider siteURL="https://docs.yourcompany.com">
      <YourApp />
      <GitBookFrame
        tabs={['assistant', 'docs']}
        greeting={{ title: 'Hi there!', subtitle: 'How can I help?' }}
        suggestions={['How do I get started?']}
        actions={[
          { icon: 'circle-question', label: 'Contact Support', onClick: () => window.open('https://support.yourcompany.com') },
        ]}
        trademark={false} // hide GitBook branding
        // visitor={{ token: 'your-jwt-token', unsignedClaims: { userId: '123' } }} // for auth
        tools={[/* custom tools */]}
      />
    </GitBookProvider>
  );
}
```

**Programmatic control with `useGitBook` hook:**
```tsx
import { useGitBook } from '@gitbook/embed/react';

function HelpButton() {
  const gitbook = useGitBook();

  const handleClick = () => {
    const iframe = document.createElement('iframe');
    iframe.src = gitbook.getFrameURL();
    const frame = gitbook.createFrame(iframe);
    frame.navigateToAssistant();
    frame.postUserMessage('How do I get started?');
  };

  return <button onClick={handleClick}>Get Help</button>;
}
```

> **Common pitfalls:**
> - `GitBookFrame` must be inside `GitBookProvider`
> - In Next.js or other SSR frameworks, dynamically import the component: `const GitBookFrame = dynamic(() => import('@gitbook/embed/react').then(m => m.GitBookFrame), { ssr: false })`
> - `useGitBook()` must be called inside a child of `GitBookProvider`

---

## Authentication

If the docs site uses [Authenticated Access](https://gitbook.com/docs/publishing-documentation/authenticated-access), pass a signed JWT visitor token.

**Script tag:**
```html
<script src="https://docs.yourcompany.com/~gitbook/embed/script.js?jwt_token=YOUR_JWT"></script>
<script>
  window.GitBook('init', { siteURL: 'https://docs.yourcompany.com' }, { visitor: { token: 'YOUR_JWT' } });
  window.GitBook('show');
</script>
```

**NPM:**
```js
const iframe = document.createElement('iframe');
iframe.src = gitbook.getFrameURL({
  visitor: {
    token: 'YOUR_JWT',
    unsignedClaims: { userId: '123', plan: 'premium' }, // optional
  },
});
```

**React:**
```tsx
<GitBookFrame visitor={{ token: 'YOUR_JWT', unsignedClaims: { userId: '123' } }} />
```

**Cookie-based detection (script tag):**
```html
<script>
  (function () {
    function getCookie(name) {
      var value = '; ' + document.cookie;
      var parts = value.split('; ' + name + '=');
      if (parts.length === 2) return parts.pop().split(';').shift();
    }
    var token = getCookie('gitbook-visitor-token');
    if (!token) return;
    var script = document.createElement('script');
    script.src = 'https://docs.yourcompany.com/~gitbook/embed/script.js?jwt_token=' + encodeURIComponent(token);
    script.onload = function () {
      window.GitBook('init', { siteURL: 'https://docs.yourcompany.com' }, { visitor: { token: token } });
      window.GitBook('show');
    };
    document.head.appendChild(script);
  })();
</script>
```

> **Auth pitfalls:**
> - Cookie name is `gitbook-visitor-token` (not `gitbook-token`)
> - Cookies don't persist across domains — app and docs must share a domain/subdomain, or pass the token directly
> - Expired tokens cause auth errors; prompt users to re-authenticate

---

## Custom Tools

Custom tools let the GitBook Assistant call your product's APIs or trigger actions in your app.

```js
window.GitBook('configure', {
  tools: [
    {
      name: 'get_user_account',
      description: 'Fetch current user account details',
      inputSchema: {
        type: 'object',
        properties: {
          userId: { type: 'string', description: 'The user ID' },
        },
        required: ['userId'],
      },
      execute: async ({ userId }) => {
        const res = await fetch(`/api/users/${userId}`);
        return res.json();
      },
      // Optional: ask for user confirmation before running
      confirmation: {
        title: 'Fetch account?',
        message: 'The assistant wants to look up your account details.',
      },
    },
  ],
});
```

Tools follow the same schema as MCP/function-calling tools: `name`, `description`, `inputSchema` (JSON Schema), and an async `execute` function.

---

## Configuration Reference

All options can be passed to `window.GitBook('configure', {...})`, `frame.configure({...})`, or as props on `<GitBookFrame />`.

| Option | Type | Description |
|--------|------|-------------|
| `tabs` | `('assistant' \| 'docs')[]` | Which tabs to show. Defaults to site config. |
| `greeting` | `{ title: string, subtitle: string }` | Welcome message in the Assistant tab. |
| `suggestions` | `string[]` | Clickable prompts shown when Assistant loads. |
| `actions` | `{ icon: string, label: string, onClick: () => void }[]` | Sidebar buttons. Icons from Font Awesome. |
| `tools` | `Array<{ name, description, inputSchema, execute, confirmation? }>` | Custom AI tools for the Assistant. |
| `trademark` | `boolean` | Show/hide GitBook branding. |
| `button` | `{ label: string, icon: string }` | Standalone script only. Customize the launcher button. |
| `visitor` | `{ token?: string, unsignedClaims?: Record<string, unknown> }` | Auth token + custom claims for Adaptive Content. |

---

## Further Reading

- Full API reference & source: [github.com/GitbookIO/gitbook/tree/main/packages/embed](https://github.com/GitbookIO/gitbook/tree/main/packages/embed)
- Authenticated Access: [gitbook.com/docs/publishing-documentation/authenticated-access](https://gitbook.com/docs/publishing-documentation/authenticated-access)
- GitBook Assistant setup: [gitbook.com/docs/publishing-documentation/gitbook-ai-assistant](https://gitbook.com/docs/publishing-documentation/gitbook-ai-assistant)
