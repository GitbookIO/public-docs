---
description: >-
  Add custom tools to GitBook Assistant to allow it to interact with your
  product, website, and more
---

# Creating custom tools

Custom tools in the Docs Embed allow you to let the Assistant intelligently dispatch actions in your product or on the web. For example, you can build a custom tool that instructs GitBook Assistant to call APIs, perform product actions, open other tools, and more.

{% hint style="info" %}
In addition to custom tools you define in your Docs Embed configuration, the Assistant will always have access to any [MCP servers you define](../../mcp-servers-for-published-docs.md) in your site's AI settings.
{% endhint %}

Tools can be defined via the `configure` method when using the script implementation or as props when using the NPM package/React components.

Let's look at an example:

```javascript
window.GitBook("configure", {
  tools: [
    {
      // Register the tool with a name and description.
      name: "create_ticket",
      description:
        "Create a ticket for the user. You MUST fill in the ticket_issue field.",

      // The input schema is data that can be accessed in the execute function.
      inputSchema: {
        type: "object",
        properties: {
          ticket_issue: {
            type: "string",
            description:
              "The issue to create the ticket for. If unknown, ask the user first.",
          },
        },
        required: ["ticket_issue"],
      },

      // An optional confirmation button that shows before the execute function is run.
      confirmation: { icon: "circle-question", label: "Create support ticket?" },

      // The execute function is the function that will be called when the tool is used.
      execute: async (input) => {
        const { ticket_issue } = input;

        // Create a ticket with the user's issue
        const ticket = await fetch("/api/tickets", {
          method: "POST",
          body: JSON.stringify({ issue: ticket_issue }),
        }).then((r) => r.json());

        return {
          // The output is passed back to the AI.
          output: {
            ticketId: ticket.id,
            status: "success",
          },
          // The summary is shown to the user.
          summary: `Created ticket #${ticket.id} for ${ticket_issue}`,
        };
      },
    },
  ],
});
```

#### How it works

Any tools provided to GitBook Assistant when configuring it will be available through AI — meaning the assistant is able to intelligently execute your tools when it fits the context.

In the example above, when the Assistant identifies that the user needs to create a support ticket, ask the user what the issue is, and then execute a function that logs a ticket.

<table><thead><tr><th width="163.39453125" valign="top">Key</th><th>Description</th></tr></thead><tbody><tr><td valign="top"><code>name</code></td><td>Unique tool identifier.</td></tr><tr><td valign="top"><code>description</code></td><td>Allows GitBook Assistant to know the context on when to use the tool being defined.</td></tr><tr><td valign="top"><code>inputSchema</code></td><td>JSON schema defining the tool's input parameters. Can be accessed in the <code>input</code> argument in the <code>execute</code> call.</td></tr><tr><td valign="top"><code>confirmation</code></td><td>An optional confirmation button that allows you to specify user interaction before firing the execute function. Format: <code>{ icon?: string, label: string }</code>.</td></tr><tr><td valign="top"><code>execute</code></td><td>The async function that runs when the tool is called. Must return <code>{ output: any, summary: string }</code>. The <code>output</code> is provided to the AI to continue working with (not shown to the user). The <code>summary</code> is the visual summary shown in the user's chat window.</td></tr></tbody></table>

