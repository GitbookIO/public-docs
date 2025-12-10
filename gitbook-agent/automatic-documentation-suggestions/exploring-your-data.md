---
description: >-
  Explore how GitBook Agent works with your data, and see the output used to
  create change requests
---

# Exploring your data

Once GitBook Agent starts ingesting conversations, it will start to categorize your data in 3 separate categories:

1. **Conversations**: Raw data that the agent has indexed from your connectors.
2. **Issues**: Standalone issues that have been identified in a conversation.
3. **Topics**: Groups of issues that are related to each other on a common topic.

All 3 are used by GitBook Agent to figure out the types of changes that might need to be made in your documentation to be improved. Below, you can find more information on how each one works.

### Conversations

Conversations are the raw data that is sent to your docs agent from your [connectors](connecting-a-source.md). They are analyzed by GitBook Agent, and assigned an impact score, and contain metadata on when the conversation was originally ingested.

Conversations are then split into issues, which are specific areas of improvement that are found within a conversation. A conversation can have more than one issue.

They are shown in the conversations tab in your docs agent’s data explorer.

### Issues

Issues are standalone issues that have been identified within a conversation. They are assigned an impact score, and contain metadata on when it was originally ingested. Opening the actions button allows you to read more about GitBook Agent’s analysis of the issue, and provides a summary of the issue.

They are shown in the issues tab in your docs agent’s data explorer.

### Topics

Topics are groups of issues related to each other on a common topic. They group multiple issues together in order for your docs agent to create meaningful, and impactful change requests you and your team can collaborate on.

They are assigned an impact score, and show the number of issues and conversations your docs agent used to form the topic. They can be updated as new conversations and issues are processed.

Opening a topic’s actions allows you to see context on the issues used to form the topic, along with logs your docs agent has processed to come up with the topic.

Additionally, you’re able to see any change requests your docs agent has created based off of the topic. Head to [reviewing change requests](../../collaboration/change-requests/change-requests-screen.md) to learn more about working with change requests created by your docs agent.

You can also toggle on/off a topic for any topics that might not be valuable, preventing them from being used to create change requests for your documentation.
