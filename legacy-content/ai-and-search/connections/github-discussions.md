---
description: >-
  Our GitHub Discussions connector can identify documentation improvements from
  discussions happening on GitHub.
---

# GitHub Discussions

## In GitBook Assistant

Discussions from GitHub can be passed as context to [GitBook Assistant](../gitbook-ai-assistant.md).

## In change requests

GitBook Agent can [identify content gaps](../../gitbook-agent/automatic-docs-improvements.md) from resolved discussions in GitHub.

## What we store

* GitBook only indexes resolved conversations in GitHub that have at least one reply. We do not index unresolved discussions, and we do not index spam discussions.
* GitBook only stores the discussion. We do not store metadata or user information.
* GitBook redacts sensitive information in the conversation before storage. We do not store sensitive information in the conversation itself.

## How to connect

* Connecting to GitHub requires credentials with read access to discussions.

