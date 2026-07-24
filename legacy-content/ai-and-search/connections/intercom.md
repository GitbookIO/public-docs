---
description: >-
  Our Intercom connector can identify content gaps from support conversations,
  or surface support conversations through the assistant.
---

# Intercom

## In GitBook Assistant

Conversations from Intercom can be passed as context to [GitBook Assistant](../gitbook-ai-assistant.md).

## In change requests

GitBook Agent can [identify content gaps](../../gitbook-agent/automatic-docs-improvements.md) from resolved support conversations in Intercom.

## What we store

* GitBook only indexes resolved conversations in Intercom that have at least one reply from a human or AI support agent. We do not index open or unresolved conversations, and we do not index spam conversations.
* GitBook only stores the conversation, we do not store any metadata or user information.
* GitBook redacts sensitive information in the ticket before storage, we do not store any sensitive information in the conversation itself.

## How to connect

* Connecting to Intercom requires an API key with read access to conversation. You own this API and can control its scope and expiry as you wish.



