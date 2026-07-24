---
description: >-
  Our GitHub Issues connector can identify documentation improvements from
  issues on GitHub.
---

# GitHub Issues

## In GitBook Assistant

Issues from GitHub can be passed as context to [GitBook Assistant](../gitbook-ai-assistant.md).

## In change requests

GitBook Agent can [identify content gaps](../../gitbook-agent/automatic-docs-improvements.md) from resolved issues in GitHub.

## What we store

* GitBook only indexes resolved issues in GitHub. We do not index open or unresolved issues, and we do not index spam conversations.
* GitBook only stores the conversation. We do not store metadata or user information.
* GitBook redacts sensitive information in the issue before storage. We do not store sensitive information in the issue itself.

## How to connect

* Connecting to GitHub requires credentials with read access to issues in GitHub.
