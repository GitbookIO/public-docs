---
description: >-
  Learn how GitBook Agent works in the background to keep your documentation
  up-to-date
icon: message-pen
---

# Automatic documentation suggestions

{% hint style="info" %}
#### This feature is currently in early access

Head to **Organization Settings → GitBook Agent** to request access.
{% endhint %}

GitBook Agent can [connect to the same signals](connecting-a-source.md) your team uses to understand both your product and what your users need: support conversations, Slack threads, GitHub issues, and more.

With this context, the Agent can proactively identify gaps, propose updates and generate docs changes automatically.&#x20;

GitBook Agent is trained on your organization’s content, meaning it has the context of your team’s writing style, structure, and tone-of-voice. And you can [add custom instructions](./#add-custom-instructions) for the Agent to follow — more on that below.

{% stepper %}
{% step %}
### Connect a source

To allow GitBook Agent to suggest automatic docs improvements, you’ll first need to [connect a source](connecting-a-source.md).&#x20;

After you connect one or more sources, the Agent will start working in the background to collect and analyze your data.
{% endstep %}

{% step %}
### Explore how GitBook Agent analyzes your data

After connecting a source, GitBook Agent will categorize that contextual information into conversations, issues, and topics.

It uses these in combination to suggest automatic improvements to your docs, which are opened as change requests.

To review the data GitBook Agent analyzes, head to your organization’s settings, then open the [**Data explorer** tab](exploring-your-data.md) in the **GitBook Agent** section.
{% endstep %}

{% step %}
### Review change requests made by GitBook Agent

As more data flows in, GitBook Agent will have enough context to start making suggestions — by opening new [change requests](../../collaboration/change-requests/) in the relevant spaces.

You can edit change requests opened by GitBook Agent just like any other change request — and anyone on your team can review them, as long as they have the right [permissions](../../account-management/member-management/permissions-and-inheritance.md).&#x20;

You can also [request a review from GitBook Agent](../review-change-requests-with-gitbook-agent.md) to have it analyze the changes it has suggested.
{% endstep %}

{% step %}
### Collaborate with GitBook Agent on changes

GitBook Agent can also act as a writing partner, allowing you to plan, write, re-write, or update anything within a change request.

When reviewing a change request from the [change requests screen](../../collaboration/change-requests/change-requests-screen.md), opening GitBook Agent will allow you to chat with it directly to make changes in the context of the change request you’re working on.&#x20;

You can also add [comments](../../collaboration/comments.md) to specific blocks, and tag @gitbook to ask GitBook Agent to make a change.
{% endstep %}
{% endstepper %}

### Add or remove published sites for GitBook Agent to modify

By default, GitBook Agent will have access to create change requests in any of your published docs sites. In the GitBook Agent’s settings screen, you can choose which sites to which you’d like the Agent to make suggested changes.

### Add custom instructions for GitBook Agent

To [add custom instructions for GitBook Agent](../what-is-gitbook-agent.md#add-a-style-guide-and-custom-instructions) to follow, open your organization’s settings and choose the **GitBook Agent** page in the sidebar.

From here you’re able to write custom instructions the Agent will use any time it’s preparing, analyzing, and generating change requests for your docs sites.
