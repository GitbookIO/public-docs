---
description: >-
  Add custom tools to GitBook Assistant to allow it to interact with your
  product, website, and more
if: >-
  visitor.claims.unsigned.bucket.EMBED_ASSISTANT_PANEL == true ||
  visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Creating custom tools for GitBook Assistant

Custom tools in GitBook Assistant allow you to dispatch web or product actions for different scenarios. For example, you can build a custom tool that instructs GitBook Assistant to call APIs, perform product actions, open other tools, and more.

Tools can be defined in the `configure` or `registerTool` call from `GitBook`.

Let's look at an example:

```javascript
window.GitBook.registerTool({
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
  },

  // An optional confirmation button that shows before the execute function is run.
  confirmation: { icon: "ticket", label: "Create ticket" },

  // The execute function is the function that will be called when the tool is used.
  execute: async (input) => {
    const { ticket_issue } = input;

    // Create a ticket with the user's issue
    const ticketId = await createTicket(ticket_issue);

    return {
      // The output is passed back to the AI.
      output: {
        ticketId: ticketId,
        status: "success",
      },
      // The summary is passed back to the user.
      summary: {
        icon: "ticket",
        text: `Created ticket for ${ticket_issue}`,
      },
    };
  },
});
```

#### How it works

Any tools provided to GitBook Assistant when configuring it will be available through AI — meaning the assistant is able to intelligently execute your tools when it fits the context.

In the example above, when the Assistant identifies that the user needs to create a support ticket, ask the user what the issue is, and then execute a function that logs a ticket.

<table><thead><tr><th width="163.39453125" valign="top">Key</th><th>Description</th></tr></thead><tbody><tr><td valign="top"><code>description</code></td><td>Allows GitBook Assistant to know the context on when to use the tool being defined.</td></tr><tr><td valign="top"><code>inputSchema</code></td><td>Define data you would like the tool to have access to (like email addresses or messages). Can be accessed in the <code>input</code> argument in the <code>execute</code> call.</td></tr><tr><td valign="top"><code>confirmation</code></td><td>An optional confirmation button that allows you to specify user interaction before firing the execute function.</td></tr><tr><td valign="top"><code>execute</code></td><td>The function that runs when the tool is called. Has access to an <code>input</code> argument that can contain user-input data defined in the <code>inputSchema</code>.</td></tr></tbody></table>
