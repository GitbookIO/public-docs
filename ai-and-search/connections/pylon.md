---
description: >-
  Our Pylon connector can identify content gaps from support conversations, or
  surface support conversations through the assistant.
---

# Pylon

## In GitBook Assistant

Conversations from Pylon can be passed as context to [GitBook Assistant](../gitbook-ai-assistant.md).

## In Change Requests

GitBook Agent can [identify content gaps](../../gitbook-agent/identifying-content-gaps.md) from resolved support conversations in Pylon.

## What we store

* GitBook only indexes resolved conversations in Pylon that have at least one reply from a human or AI support agent. We do not index open or unresolved conversations, and we do not index spam conversations.
* GitBook only stores the conversation. We do not store metadata or user information.
* GitBook redacts sensitive information in the conversation before storage. We do not store sensitive information in the conversation itself.

## How to connect

* Connecting to Pylon requires credentials with read access to conversations in Pylon.
