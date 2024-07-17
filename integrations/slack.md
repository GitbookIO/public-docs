---
description: >-
  The GitBook integration for Slack lets you curate knowledge into your
  knowledge base, right from the source
cover: ../.gitbook/assets/Slack (1).png
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

# Slack (beta)

The GitBook Slack integration helps you collect, review, and share information to and from your company’s knowledge base. With a set of commands you can run within your Slack Workspace, it’s easy to add or use information that’s useful for your team.

GitBook AI will summarize information that you or your team add to your knowledge base, turning a series of messages into a context-rich document. And when you or a colleague need to learn more about something, you can ask GitBook AI and get a plain-text summary, with all the background needed to dive in deeper.

{% hint style="warning" %}
GitBook AI & the Slack integration are available as part of the Pro plan and Enterprise plan. To find out more, [visit our pricing page](https://www.gitbook.com/pricing).
{% endhint %}

### Installation & Configuration

You can install the Slack integration right from the [integrations page](https://app.gitbook.com/integrations/slack) in GitBook.

After installing the Slack integration to GitBook, you’ll see a prompt to authorize your user account and install the Slack bot into your organization’s Slack workspace.

After installing the integration into your Slack workspace, you can use the included Slack commands, or invite the GitBook Slack bot to the channels you’d like to interact with it in, and tag it to ask a question. See the [FAQs](slack.md#faqs) at the bottom to learn more about where you can use the GitBook Slack bot.

{% hint style="info" %}
You need to be a [workspace owner or workspace admin](https://slack.com/intl/en-gb/help/articles/360018112273-Types-of-roles-in-Slack) in Slack to install the GitBook Slack bot into your team’s workspace.&#x20;
{% endhint %}

{% hint style="info" %}
**If you had installed the GitBook Slack integration prior to October 7th 2023, you’ll need to uninstall and reinstall the integration to get the latest version.**
{% endhint %}

### Adding information to your knowledge base

You can add information to your team’s knowledge base by calling the GitBook Slack bot. You can invoke the bot in different ways, in both public or private channels.

#### How to add information using the GitBook Slack bot

Calling `@GitBook save` from within thread will summarize context and data from that thread into your team’s knowledge base as [a snippet](../snippets-and-insights/snippets-beta.md).&#x20;

{% hint style="info" %}
Calling the GitBook bot will work **from any thread** within a public channel or private channel. In a private channel, make sure to invite the GitBook bot in order for it to work.
{% endhint %}

#### How to add information using the Slack shortcut

You can also add data to your team’s knowledge base using Slack shortcuts. Simply click the **More actions** button from a thread in Slack, click **More message shortcuts…**, and search for the GitBook bot. You can call the shortcut from any message in a thread — the GitBook bot will save the entire thread.

### How to summon GitBook knowledge within Slack

As well as saving information to your team’s knowledge base, you can also recall anything from your knowledge base from within Slack, while you work.&#x20;

#### Using the GitBook Slack command

Calling `/gitbook [question]` will allow you to get a **private**, AI-generated response to your question, based on the information in your team’s knowledge base.&#x20;

The answer in Slack will only be visible to you — which is useful if you need a quick bit of context on something without polluting your team’s channel.&#x20;

After GitBook returns your answer, you’ll have the option to share your answer to the channel, if you think the answer is helpful for others.

{% hint style="info" %}
The Slack command will only work in public channels, private channels, and direct messages. **It will not work inside of a thread.**
{% endhint %}

#### Using the GitBook Slack bot

You can call the GitBook Slack bot directly with `@GitBook [question]` to receive a **public** answer in any channel or thread.

After asking your question in a channel or thread, everyone that has access to that channel will be able to see it and the answer.

{% hint style="info" %}
Calling the GitBook Slack bot will only work in public channels, private channels, and threads. It will not work inside of a direct message.
{% endhint %}

#### Messaging the GitBook Slack bot directly&#x20;

You can also ask questions to the GitBook Slack bot in a direct message. After starting a direct message with the GitBook Slack bot, simply ask your question. GitBook AI will generate and return an answer privately in seconds.

### FAQs

<details>

<summary>Why isn’t the <code>/gitbook [question]</code> or <code>@GitBook save</code> command working in Slack?</summary>

When interacting with the GitBook Slack integration, there are a few things to keep in mind:

* The `/gitbook [question]` command does not work in threads. It will only work in public and private channels or direct messages.
* The `@GitBook save` command does not work in top-level channels or direct messages. It will only work inside threads in public or private channels.

</details>

<details>

<summary>How do permissions work with the Slack integration?</summary>

The Slack integration does not take into account individual user permissions in GitBook. This is because there is no direct link or tie between a Slack user and a GitBook user. However, when you set up the Slack integration you can specify which spaces it has access to, which can help mitigate any security risks if you have sensitive content.

</details>
