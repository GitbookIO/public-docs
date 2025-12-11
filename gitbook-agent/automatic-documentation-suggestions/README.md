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

GitBook Agent works in the background of your GitBook organization, consuming ingested data from [connected sources](connecting-a-source.md) to continuously update and refine your documentation.

GitBook Agent is trained on your organization’s content, meaning it has the context of your team’s writing style, structure, and tone-of-voice. You can also [add custom instructions](./#add-custom-instructions) for your docs agent to follow in your docs agent’s settings.

{% stepper %}
{% step %}
### Connect a source

To allow GitBook Agent to suggest automatic docs improvements, you’ll first need to [connect a source](connecting-a-source.md).&#x20;

After you connect one or more sources, GitBook Agent will start working in the background to collect and analyze your data.
{% endstep %}

{% step %}
### Explore how GitBook Agent analyzes your data

After connecting a source, GitBook Agent will categorize conversations, context, and more into conversations, issues, and topics.

It uses these in combination to suggest automatic improvements to your docs, which are opened as change requests.

To review the data GitBook Agent analyzes, head to the [data explorer tab](exploring-your-data.md) in your docs agent’s settings.
{% endstep %}

{% step %}
### Review change requests made by GitBook Agent

As more data flow in, GitBook Agent will have enough context to start making suggestions. Suggestions are made in the form of [change requests](../../collaboration/change-requests/).&#x20;

Change requests opened by GitBook Agent can be edited like a normal change request, and can be reviewed by anyone on your team with the right [permissions](../../account-management/member-management/permissions-and-inheritance.md).&#x20;

You can also [request a review from GitBook Agent](../review-change-requests-with-gitbook-agent.md) to have it analyze the changes it has suggested.
{% endstep %}

{% step %}
### Collaborate with GitBook Agent on changes

GitBook Agent can also act as a writing partner, allowing you to plan, write, re-write, or update anything within a change request.

When reviewing a change request from the [change requests screen](../../collaboration/change-requests/change-requests-screen.md), opening GitBook Agent will allow you to chat with it directly to make changes in the context of the change request you’re working on.&#x20;
{% endstep %}
{% endstepper %}

### Add or remove published sites for GitBook Agent to modify

By default, GitBook Agent will have access to create change requests in any of your published docs. In your docs agent’s settings, you’re able to toggle on/off the sites you’d like your docs agent to have access to.

### Add custom instructions for GitBook Agent

To add more custom instructions for GitBook Agent to follow, open your organization’s settings and choose the **GitBook Agent** page in the sidebar..

From here you’re able to write custom instructions the Agent will use any time it’s preparing, analyzing, and generating change requests for your docs sites.
