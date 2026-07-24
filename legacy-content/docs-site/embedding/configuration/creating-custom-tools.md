---
description: >-
  Connect GitBook Assistant to any tool you can call from your app — especially
  support workflows
---

# Connect to custom tools

Custom tools let the GitBook Assistant inside the [Docs Embed](../) run real actions.

You can connect it to _any_ tool your app can access. That includes your backend APIs, third-party SDKs, and internal systems.

If your app can call it, the Assistant can call it.

Common examples:

* Create or update support tickets on behalf of the user
*   Hand off to support by opening a support chat with a prefilled message

    <div data-gb-custom-block data-tag="hint" data-style="success" class="hint hint-success"><p><strong>Support handoff</strong> is a great way to get started with custom tools. It’s the fastest way to unblock users.</p></div>
* Trigger product actions (reset MFA, resend an invite, enable a feature flag)
* Look up account status in your backend
* Kick off workflows in tools like Jira, Linear, Slack, or Zendesk

{% hint style="info" %}
In addition to tools you define in the Embed config, the Assistant can also use any [MCP servers you set up](../../../publishing-documentation/mcp-servers-for-published-docs.md) in **Settings → AI & MCP**.
{% endhint %}

### Where tools run

The tool’s `execute` function runs in the same environment as your embed integration.

That usually means it runs in the user’s browser, inside your app.

So you can:

* Call your own backend endpoints
* Call any third-party SDK already loaded in your app (for example, Intercom)
* Open modals, deep links, or in-product UI

{% hint style="warning" %}
Avoid putting secrets in client-side code — call your backend instead.
{% endhint %}

### Add a tool

Define tools:

* Via `window.GitBook("configure", …)` for the [script tag](../implementation/script.md) implementation
* Via the `tools` prop for the [Node.js/NPM](../implementation/nodejs.md) package and [React](../implementation/react.md) components

{% hint style="info" %}
Tools aren’t the same as embed **actions**.

* Use **actions** for buttons the user clicks.
* Use tools when you want the Assistant to choose and run code.
{% endhint %}

#### Tool template (resend an invite email)

Let’s look at an example:

```javascript
window.GitBook("configure", {
  tools: [
    {
      // Register the tool with a name and description.
      name: "resend_invite",
      description:
        "Resend an invite email when the user can’t find it or says it expired.",

      // The input schema is data that can be accessed in the execute function.
      inputSchema: {
        type: "object",
        properties: {
          email: {
            type: "string",
            description:
              "The email address to resend the invite to. If unknown, ask the user first.",
          },
        },
        required: ["email"],
      },

      // An optional confirmation button that shows before the execute function is run.
      confirmation: { icon: "paper-plane", label: "Resend invite?" },

      // The execute function is the function that will be called when the tool is used.
      execute: async (input) => {
        const { email } = input;

        const result = await fetch("/api/invites/resend", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ email }),
        }).then((r) => r.json());

        return {
          // The output is passed back to the AI.
          output: {
            recipient: email,
            status: result.status ?? "success",
          },
          // The summary is shown to the user.
          summary: {
            icon: "check",
            text: "Resent the invite email.",
          },
        };
      },
    },
  ],
});
```

### How tools get used

Once you register tools, the Assistant can choose them automatically — based on the user’s question and your tool `description`.

If required fields are missing, the Assistant should ask follow-up questions.

If you add `confirmation`, the user must approve before the tool runs.

### Tool fields

* `name`: Unique identifier.
* `description`: The “when to use this” hint for the Assistant.
* `inputSchema`: JSON Schema for tool inputs.
* `confirmation` (optional): A confirmation button shown before the tool runs.
* `execute(input)`: Async function that runs the action.
  * Return `{ output, summary }`.
  * `output` goes back to the Assistant.
  * `summary` shows to the user.

#### Confirmation

Use `confirmation` when you want the user to approve an action. It helps prevent surprise side effects.

`confirmation` accepts:

* `label` (required): Button text.
* `icon` (optional): A [Font Awesome](https://fontawesome.com/search) icon name.

### Support workflow

Support is the highest-leverage use case for tools.

You can let the Assistant:

* Collect missing details
* Create a ticket in your system
* Open a human support channel with context prefilled

#### Template: open support chat with a prefilled message

Use this when you want a clean handoff to a human.

```javascript
window.GitBook("configure", {
  tools: [
    {
      name: "open_support_chat",
      description:
        "Open the support chat with a prefilled message so the user can contact support fast.",
      inputSchema: {
        type: "object",
        properties: {
          message: {
            type: "string",
            description:
              "The message to send to support. If missing, ask the user first.",
          },
        },
      },
      confirmation: { icon: "circle-question", label: "Open Support Chat" },
      execute: (input) => {
        // Close GitBook Assistant
        window.GitBook('close');
     
        // Examples:
        // - Intercom: Intercom('showNewMessage', input.message);
        // - Zendesk: zE('messenger', 'open');
        
        return {
          output: {
            status: "success",
          },
          summary: { icon: 'check', text: "Forwarded to support." },
        };
      },
    },
  ],
});
```

{% hint style="info" %}
Pair this with an always-visible **Contact Support** action in the embed sidebar. You can configure actions by following [Customizing the Embed](customizing-docs-embed.md).
{% endhint %}

### Next steps

* Need the full embed API surface? See [API Reference](reference.md).
* Want more UI controls (greeting, suggestions, actions)? See [Customizing the Embed](customizing-docs-embed.md).
