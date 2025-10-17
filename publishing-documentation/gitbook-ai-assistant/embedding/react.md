---
description: >-
  Use prebuilt React components to embed GitBook Assistant in your React application
if: >-
  visitor.claims.unsigned.bucket.EMBED_ASSISTANT_PANEL == true ||
  visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Embedding with React

For React projects, GitBook provides prebuilt components that make embedding the Assistant simple and idiomatic. The components handle state management, context, and lifecycle automatically.

## Steps

1. **Install the package**

   Add `@gitbook/embed` to your React project:

   ```bash
   npm install @gitbook/embed
   ```

2. **Import the React components**

   Import the `GitBookProvider` and `GitBookAssistantFrame` components:

   ```jsx
   import {
     GitBookProvider,
     GitBookAssistantFrame,
   } from "@gitbook/embed/react";
   ```

3. **Wrap your app with GitBookProvider**

   Add the provider at the root of your component tree or where you need the Assistant:

   ```jsx
   function App() {
     return (
       <GitBookProvider siteURL="https://docs.company.com">
         <YourAppContent />
       </GitBookProvider>
     );
   }
   ```

4. **Add the AssistantFrame component**

   Place the frame component where you want the Assistant to appear:

   ```jsx
   function App() {
     return (
       <GitBookProvider siteURL="https://docs.company.com">
         <div className="app">
           <YourAppContent />
           <GitBookAssistantFrame />
         </div>
       </GitBookProvider>
     );
   }
   ```

5. **Customize the Assistant**

   Pass configuration props to the provider:

   ```jsx
   <GitBookProvider
     siteURL="https://docs.company.com"
     welcomeMessage="Welcome to our help center! How can we assist you today?"
     suggestions={[
       "How do I get started?",
       "What are the pricing plans?",
       "How do I reset my password?",
     ]}
     buttons={[
       {
         label: "Contact Support",
         icon: "envelope",
         onClick: () => {
           window.open("mailto:support@example.com", "_blank");
         },
       },
     ]}
   >
     <GitBookAssistantFrame />
   </GitBookProvider>
   ```

6. **Control the Assistant with the useGitBook hook**

   Use the `useGitBook` hook to interact with the Assistant programmatically:

   ```jsx
   import { useGitBook } from "@gitbook/embed/react";

   function HelpButton() {
     const gitbook = useGitBook();

     return <button onClick={() => gitbook.open()}>Open Help</button>;
   }
   ```

7. **Conditionally render the Assistant**

   Show the Assistant only when needed:

   ```jsx
   function App() {
     const [showAssistant, setShowAssistant] = useState(false);

     return (
       <GitBookProvider siteURL="https://docs.company.com">
         <button onClick={() => setShowAssistant(true)}>Get Help</button>
         {showAssistant && <GitBookAssistantFrame />}
       </GitBookProvider>
     );
   }
   ```

8. **Use with Next.js or server-side rendering**

   Dynamically import the components to avoid SSR issues:

   ```jsx
   import dynamic from "next/dynamic";

   const GitBookProvider = dynamic(
     () => import("@gitbook/embed/react").then((mod) => mod.GitBookProvider),
     { ssr: false }
   );

   const GitBookAssistantFrame = dynamic(
     () =>
       import("@gitbook/embed/react").then((mod) => mod.GitBookAssistantFrame),
     { ssr: false }
   );
   ```

## Props & Configuration

**GitBookProvider Props:**

| Prop             | Type        | Required | Default | Description                                                                                             |
| ---------------- | ----------- | -------- | ------- | ------------------------------------------------------------------------------------------------------- |
| `siteURL`        | `string`    | Yes      | N/A     | Your GitBook docs site URL (e.g., `https://docs.company.com`).                                          |
| `welcomeMessage` | `string`    | No       | `null`  | Custom welcome message shown when the Assistant opens.                                                  |
| `suggestions`    | `string[]`  | No       | `[]`    | Array of suggested questions displayed to users.                                                        |
| `buttons`        | `object[]`  | No       | `[]`    | Custom buttons in the Assistant header. Each button has `label`, `icon`, and `onClick` properties.      |
| `tools`          | `object[]`  | No       | `[]`    | Custom tools for the Assistant. See [Creating custom tools](../configuration/creating-custom-tools.md). |
| `children`       | `ReactNode` | Yes      | N/A     | Child components to render within the provider.                                                         |

**GitBookAssistantFrame Props:**

| Prop        | Type     | Required | Default | Description                                     |
| ----------- | -------- | -------- | ------- | ----------------------------------------------- |
| `className` | `string` | No       | `null`  | CSS class name to apply to the frame container. |
| `style`     | `object` | No       | `{}`    | Inline styles to apply to the frame container.  |

**useGitBook Hook Methods:**

| Method                     | Parameters        | Description                                   |
| -------------------------- | ----------------- | --------------------------------------------- |
| `open()`                   | None              | Open the Assistant panel.                     |
| `close()`                  | None              | Close the Assistant panel.                    |
| `toggle()`                 | None              | Toggle the panel open/closed.                 |
| `navigateToPage(path)`     | `path: string`    | Navigate to a specific docs page.             |
| `navigateToAssistant()`    | None              | Navigate directly to the Assistant interface. |
| `postUserMessage(message)` | `message: string` | Send a message as the user.                   |
| `clearChat()`              | None              | Clear all chat messages.                      |

## Common pitfalls

- **Not wrapping with GitBookProvider** – The `GitBookAssistantFrame` requires a parent `GitBookProvider` to function.
- **Using with SSR without dynamic import** – The component uses browser APIs and must be dynamically imported in Next.js or other SSR frameworks.
- **siteURL not matching published docs** – Ensure the `siteURL` prop matches your live docs site URL exactly.
- **Calling useGitBook outside provider** – The `useGitBook` hook must be used within a component that's a child of `GitBookProvider`.
- **Multiple providers in the tree** – Avoid nesting multiple `GitBookProvider` instances, as this can cause context conflicts.
