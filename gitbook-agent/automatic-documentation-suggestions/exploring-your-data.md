---
description: >-
  Explore how GitBook Agent works with your data, and see the output used to
  create change requests
---

# Exploring your data

Once GitBook Agent starts ingesting conversations, it will start to categorize your data into three categories:

1. **Conversations**: Raw data that the agent has indexed from your connectors.
2. **Issues**: Individual issues that have been identified within a conversation.
3. **Topics**: Groups of issues that are related to each other on a common topic.

All three are used by GitBook Agent to figure out the types of changes that might need to be made in your documentation to be improved. Below, you can find more information on how each one works.

{% hint style="info" %}
GitBook Agent categorizes data and makes proactive suggestions for your docs automatically. You don’t need to do anything with this data — it’s available for visibility.
{% endhint %}

### Conversations

Conversations are the raw data that is sent to GitBook Agent from your [connectors](connecting-a-source.md). The Agent analyzes them and assigns an impact score, which is added to the metadata from when the conversation was originally ingested.

Conversations are then split into issues, which are specific areas of improvement that are found within a conversation. A conversation may contain more than one issue.

You can view conversations by opening **Organization settings** > **GitBook Agent** > **Data Explorer** and choosing the **Conversations** tab.

### Issues

Issues are standalone data points that have been identified within a conversation. GitBook Agent assigns them an impact score, which is added to the metadata from when the data was ingested.&#x20;

You can view issues by opening **Organization settings** > **GitBook Agent** > **Data Explorer** and choosing the **Issues** tab.

Click the **Inspect** <picture><source srcset="../../.gitbook/assets/25_12_12_inspect_1.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_12_12_inspect_1.svg" alt=""></picture> button on an issue to read a summary, along with GitBook Agent’s analysis of it.

### Topics

Topics are groups of issues that are related to one another. By grouping issues together, GitBook Agent can create useful, context-driven change requests for your team.

The Agent will assign each topic an impact score, and show the number of issues and conversations the Agent used to form the topic. They’ll update automatically as new conversations and issues are processed.

Click **Inspect** <picture><source srcset="../../.gitbook/assets/25_12_12_inspect_1.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_12_12_inspect_1.svg" alt=""></picture> on any topic to see the issues used to form the topic, along with a log of GitBook Agent’s thinking to process those issues and create the topic.

This inspector screen also shows any change requests GitBook Agent has created based off of the topic — ready for [you and your team to review](../../collaboration/change-requests/change-requests-screen.md).

{% hint style="info" %}
## Disabling a topic

If a topic isn’t valuable, you can toggle the topic off from its inspector screen. Once disabled, the topic will no longer be used to create change requests for your documentation.
{% endhint %}
