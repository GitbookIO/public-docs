---
description: >-
  Connect different context sources to GitBook, such as Intercom, Slack, email,
  and more
---

# Connecting a source

GitBook Agent can pull in context from different sources, including Intercom, Slack, email, and more. Connecting a source allows the Agent to build change requests based off of real-world context, such as email chains, Slack threads, or resolved Intercom conversations.

The context provided through different connectors will allow your team to work faster and more reliably, cutting down duplicated work of documenting something that may have been resolved in another platform.

### Connect a source

Head to your organization’s settings, and into the **GitBook Agent** section. From here, you’ll be able to configure the different connectors in order to successfully connect your desired tool.

Each connector works slightly differently, and may contain different functionality. See the section for your tool below to see how to configure and work with your desired tool.

<details>

<summary>Email</summary>

The email connector is a versatile connector that allows you to provide context to GitBook Agent **through a dedicated email address**.

There’s no configuration to use the email connector — it will work out of the box.

#### Add email threads to GitBook Agent

1. Add any email thread to the Agent by forwarding the email thread to the dedicated email address provided in your docs agent’s settings,

#### Use the email connector to connect 3rd party apps

The email connector is the most versatile way of providing context to GitBook. Using tools like [Zapier](https://zapier.com/) or [Relay.app](https://relay.app/), you’re able to connect thousands of 3rd party apps.

In either tool, set up a new workflow/connection, and make sure the output is sent to the dedicated email address provided in GitBook Agent’s settings.

</details>

<details>

<summary>Intercom</summary>

The Intercom connector allows GitBook Agent to pull in context from **resolved or closed conversations**.&#x20;

Any time a conversation is closed by your support team, the Intercom connector will send the full context of the conversation to your GitBook Agent, and the agent will use this context to generate issues (and ultimately topics), which are then used to generate an actionable change request that can be reviewed by your team.

#### Connect Intercom

1. In GitBook Agent’s settings, click into Intercom connector and authorize Intercom with your account.
2. Once signed in, GitBook Agent is ready to start analyzing your closed support tickets.

#### Add Intercom conversations to GitBook Agent

The Intercom connector works in the background — once it’s installed and configured, it will run in the background and add send and resolved or closed conversations to GitBook Agent automatically.

</details>

<details>

<summary>Slack</summary>

The Slack connector allows GitBook Agent to pull in context from **threads it’s tagged in**.

Once the Slack connector is called in a thread, it will analyze the context of the thread, and send the full context of the conversation to your GitBook Agent. The agent will then use this context to generate issues (and ultimately topics), which are then used to generate an actionable change request that can be reviewed by your team.

#### Connect Slack

1. In GitBook Agent’s settings, click into Slack connector and authorize Slack with your account.
2. Install the Slack bot into your organization’s workspace.

#### Add Slack threads to GitBook Agent

1. Call `@gitbook` inside of a thread that you would like to ingest.
2. Optionally add extra context that the Agent can use, such as:

```
@gitbook use this conversation to better document our API reference.
```

</details>
