---
description: >-
  The GitBook integration for Slack lets you curate knowledge into your
  knowledge base, right from the source
cover: ../../.gitbook/assets/Slack (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Slack

{% hint style="warning" %}
This integration is currently in beta. See our [beta information](./) for more info and learn how to gain access.
{% endhint %}

The GitBook Slack integration helps you collect, review, and share information to and from your company’s knowledge base. With a set of commands you can run within your Slack Workspace, it’s easy to add or use information that’s useful for your team.

GitBook AI will summarize information that you or your team add to your knowledge base, turning a series of messages into a context-rich document. And when you or a colleague need to learn more about something, you can ask GitBook AI and get a plain-text summary, with all the background needed to dive in deeper.

### Installation & Configuration

The Slack integration is currently in closed beta. Once accepted to the beta, you’ll be able to install the Slack integration from the home screen in the GitBook app.

After installing the integration into your organization’s Slack workspace, you can use the included Slack commands, or invite the GitBook Slackbot to the channels you’d like to interact with it in, and tag it to ask a question.

{% hint style="info" %}
You may need to be an admin or a workspace administrator to install the GitBook Slackbot into your team.&#x20;
{% endhint %}

### Adding information to your knowledge base

You can add information to your team’s knowledge base by calling the GitBook Slackbot. You can invoke the bot in different ways, in both public or private channels.

#### How to add information using the GitBook Slackbot

Calling `@gitbook save` from within thread will summarize context and data from that thread into your team’s knowledge base.&#x20;

{% hint style="info" %}
Calling the GitBook bot will work from any thread within a public channel, private channel, or direct message.
{% endhint %}

#### How to add information using the Slack shortcut

You can also add data to your team’s knowledge base using Slack shortcuts. Simply click the **More actions** button from a thread in Slack, click **More message shortcuts…**, and search for the GitBook bot. You can call the shortcut from any message in a thread — the GitBook bot will save the entire thread.

{% hint style="info" %}
Calling the GitBook bot will work from any thread within a public channel, private channel, or direct message.
{% endhint %}

### How to summon GitBook knowledge from Slack

As well as saving information to your team’s knowledge base, you can also recall anything from your knowledge base from within Slack, while you work.&#x20;

#### Using the GitBook Slack command

Calling `/gitbook [question]` will allow you to get a **private** AI generated response to your question, based on the information in your team’s knowledge base.&#x20;

The answer in Slack will only be visible to you — which is useful if you need a quick bit of context on something without polluting your team’s Slack channel.&#x20;

After GitBook returns your answer, you’ll have the option to share your answer to the channel, if you think the answer is helpful for others.

{% hint style="info" %}
The Slack command will only work in public channels, private channels, and direct messages. It will not work inside of a thread.
{% endhint %}

#### Using the GitBook Slackbot

You can call the GitBook Slackbot directly to ask a question, and receive a **public** answer in any channel or thread.

After asking your question in a channel or thread, everyone that has access to that channel will be able to see it and the answer.

{% hint style="info" %}
Calling the GitBook Slackbot will only work in public channels, private channels, and threads. It will not work inside of a direct message.
{% endhint %}

#### Messaging the GitBook Slackbot directly&#x20;

You can also ask questions directly to the GitBook Slackbot in a direct message. After starting a direct message with the GitBook Slackbot, simply ask your question. GitBook AI will generate and return an answer privately in seconds.

### FAQs

<details>

<summary>Why isn’t the <code>/gitbook question</code> or <code>@gitbook save</code> command working in Slack?</summary>

When interacting with the GitBook Slack integration, there are a few things to keep in mind:

* The `/gitbook question` command does not work in threads. It will only work in public and private channels or direct messages.
* The `@gitbook save` command does not work in top-level channels or direct messages. It will only work inside threads.

</details>
