---
description: >-
  Our Zendesk connector can identify content gaps from support conversations, or
  surface support conversations through the assistant.
---

# Zendesk

## In GitBook Assistant

Conversations from Zendesk can be passed as context to [GitBook Assistant](../gitbook-ai-assistant.md).

## In change requests

GitBook Agent can [identify content gaps](../../gitbook-agent/automatic-docs-improvements.md) from resolved support conversations in Zendesk.

## What we store

* GitBook only indexes resolved conversations in Zendesk that have at least one reply from a human or AI support agent. We do not index open or unresolved conversations, and we do not index spam conversations.
* GitBook only stores the conversation, we do not store any metadata or user information.
* GitBook redacts sensitive information in the ticket before storage, we do not store any sensitive information in the conversation itself.

## How to connect

* Connecting to Zendesk requires the subdomain of the Zendesk application e.g. `gitbook.zendesk.com`&#x20;
* We also require an API key with read access to the conversations in Zendesk. You own this API and can control its scope and expiry as you wish.



