---
description: Add your own tools the embedded Assistant can call.
---

# Custom tools for the Assistant

Custom tools let GitBook Assistant inside the [Docs Embed](../README.md) run real actions. Connect it to any tool your app can access — backend APIs, third-party SDKs, internal systems. If your app can call it, the Assistant can call it.

Common examples:

* Create or update support tickets on behalf of the user.
* Hand off to support by opening a support chat with a prefilled message — a great way to get started with custom tools, and the fastest way to unblock users.
* Trigger product actions (reset MFA, resend an invite, enable a feature flag).
* Look up account status in your backend.
* Kick off workflows in tools like Jira, Linear, Slack, or Zendesk.

{% hint style="info" %}
Beyond tools you define in the embed config, the Assistant can also use any [MCP servers you've set up](../../gitbook-ai/readers-ai/mcp-server-for-published-docs.md) in **Settings → AI & MCP**.
{% endhint %}

### Where tools run

A tool's `execute` function runs in the same environment as your embed integration — usually the user's browser, inside your app. So you can call your own backend endpoints, call any third-party SDK already loaded in your app (e.g. Intercom), or open modals, deep links, or in-product UI.

{% hint style="warning" %}
Avoid putting secrets in client-side code — call your backend instead.
{% endhint %}

### Add a tool

Define tools via `window.GitBook("configure", ...)` for the script tag implementation, or via the `tools` prop for Node.js/NPM and React — see [Install the embed](../install-the-embed.md).

#### Tool template: resend an invite email

```javascript
window.GitBook("configure", {
  tools: [
    {
      // Register the tool with a name and description.
      name: "resend_invite",
      description:
        "Resend an invite email when the user can't find it or says it expired.",

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

Once registered, the Assistant chooses tools automatically based on the user's question and your tool's `description`. If required fields are missing, it should ask follow-up questions. If you add `confirmation`, the user must approve before the tool runs.

### Tool fields

* `name` — unique identifier.
* `description` — the "when to use this" hint for the Assistant.
* `inputSchema` — JSON Schema for tool inputs.
* `confirmation` *(optional)* — a confirmation button shown before the tool runs. Accepts `label` (required) and `icon` (optional, a Font Awesome icon name).
* `execute(input)` — async function that runs the action, returning `{ output, summary }`: `output` goes back to the Assistant, `summary` is shown to the user.

Use `confirmation` when you want the user to approve an action first, to prevent surprise side effects.

### Support workflow

Support is the highest-leverage use case for tools — let the Assistant collect missing details, create a ticket in your system, or open a human support channel with context prefilled.

#### Template: open support chat with a prefilled message

Use this for a clean handoff to a human:

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
Pair this with an always-visible **Contact Support** action in the embed sidebar — see [Adding actions](README.md#adding-actions).
{% endhint %}
