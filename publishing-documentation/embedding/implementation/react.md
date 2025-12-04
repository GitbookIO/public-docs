---
description: >-
  Use prebuilt React components to add the Docs Embed to your React
  application
---

# React

For React projects, GitBook provides prebuilt components that make embedding your docs simple and idiomatic. The components handle state management, context, and lifecycle automatically.

## Steps

{% stepper %}
{% step %}
### Install the package

Add `@gitbook/embed` to your React project:

```bash
npm install @gitbook/embed
```

For the complete API reference and source code, see the [`@gitbook/embed` package on GitHub](https://github.com/GitbookIO/gitbook/tree/main/packages/embed).
{% endstep %}

{% step %}
### Import the React components

Import the `GitBookProvider` and `GitBookFrame` components:

```jsx
import {
  GitBookProvider,
  GitBookFrame,
} from "@gitbook/embed/react";
```
{% endstep %}

{% step %}
### Wrap your app with GitBookProvider

Add the provider at the root of your component tree or where you need the embed:

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
### Add the GitBookFrame component

Place the frame component where you want the embed to appear:

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
{% endstep %}

{% step %}
### Customize the embed

Pass configuration props to the frame component:

```jsx
<GitBookProvider siteURL="https://docs.company.com">
  <GitBookFrame
    tabs={['assistant', 'docs']}
    greeting={{ title: 'Welcome!', subtitle: 'How can I help?' }}
    suggestions={['What is GitBook?', 'How do I get started?']}
    actions={[
      {
        icon: 'circle-question',
        label: 'Contact Support',
        onClick: () => window.open('https://support.example.com', '_blank')
      }
    ]}
    tools={[/* ... */]}
    visitor={{
      token: 'your-jwt-token',
      unsignedClaims: { userId: '123' }
    }}
  />
</GitBookProvider>
```
{% endstep %}

{% step %}
### Control the embed with the useGitBook hook

Use the `useGitBook` hook to interact with the embed programmatically:

```jsx
import { useGitBook } from "@gitbook/embed/react";

function HelpButton() {
  const gitbook = useGitBook();
  const frameURL = gitbook.getFrameURL({ visitor: { token: '...' } });
  
  const handleNavigate = () => {
    const iframe = document.createElement('iframe');
    iframe.src = frameURL;
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
### Conditionally render the embed

Show the embed only when needed:

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
### Use with Next.js or server-side rendering

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

## Props & Configuration

**GitBookProvider Props:**

| Prop       | Type        | Required | Default | Description                                                      |
| ---------- | ----------- | -------- | ------- | ---------------------------------------------------------------- |
| `siteURL`  | `string`    | Yes      | N/A     | Your GitBook docs site URL (e.g., `https://docs.company.com`).   |
| `children` | `ReactNode` | Yes      | N/A     | Child components to render within the provider.                  |

**GitBookFrame Props:**

All configuration options can be passed as props to `<GitBookFrame>`. See the Configuration section below for available options.

| Prop        | Type     | Required | Default | Description                                     |
| ---------- | -------- | -------- | ------- | ----------------------------------------------- |
| `className` | `string` | No       | `null`  | CSS class name to apply to the frame container. |
| `style`     | `object` | No       | `{}`    | Inline styles to apply to the frame container.  |
| `visitor`   | `object` | No       | `{}`    | Authenticated access options (see below).       |

**useGitBook Hook:**

Returns a `GitBookClient` instance with the following methods:

- `getFrameURL(options?: { visitor?: {...} })` → `string` - Get the iframe URL
- `createFrame(iframe: HTMLIFrameElement)` → `GitBookFrameClient` - Create a frame client

The frame client provides:
- `navigateToPage(path: string)` → `void`
- `navigateToAssistant()` → `void`
- `postUserMessage(message: string)` → `void`
- `clearChat()` → `void`
- `configure(settings: {...})` → `void`
- `on(event: string, listener: Function)` → `() => void`

## Configuration Options

Configuration options are available as props on `<GitBookFrame>`:

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

Used for [Adaptive Content](../../adaptive-content/README.md) and [Authenticated Access](../../authenticated-access/README.md).

- **Type**: `{ token?: string, unsignedClaims?: Record<string, unknown> }`

## Common pitfalls

* **Not wrapping with GitBookProvider** – The `GitBookFrame` requires a parent `GitBookProvider` to function.
* **Using with SSR without dynamic import** – The component uses browser APIs and must be dynamically imported in Next.js or other SSR frameworks.
* **siteURL not matching published docs** – Ensure the `siteURL` prop matches your live docs site URL exactly.
* **Calling useGitBook outside provider** – The `useGitBook` hook must be used within a component that's a child of `GitBookProvider`.
* **Multiple providers in the tree** – Avoid nesting multiple `GitBookProvider` instances, as this can cause context conflicts.
* **Using old component names** – The component is now `GitBookFrame`, not `GitBookAssistantFrame`.

