---
description: Escape hatch to the GitBook API when MCP tools don't cover what you need.
---

# Drop to the API

GitBook MCP and the CLI both wrap the same underlying GitBook API — they cover the common, everyday operations well, but neither exposes every capability of the API. When you need something more specific — a custom integration, a bespoke automation, or an operation that isn't modeled as an MCP tool or CLI command yet — drop down to the raw API directly.

{% hint style="info" %}
This page covers *when* to reach for the API instead of MCP or the CLI. For the endpoints themselves, see Developers → API.
{% endhint %}

### When this makes sense

* You're building a custom integration or internal tool that needs to call GitBook programmatically, outside of an agent session.
* You need an operation that MCP doesn't expose as a tool and the CLI doesn't expose as a command.
* You're building your own agent or product on top of GitBook — see [Build your own agent on GitBook](build-your-own-agent-on-gitbook.md).

### Authenticating

The API uses the same personal access tokens as the CLI and MCP's non-OAuth path — create one from your [developer settings](https://app.gitbook.com/account/developer) and send it as a bearer token:

```http
Authorization: Bearer <YOUR_TOKEN>
```

If you already have a token from setting up the CLI or an MCP client, you can reuse it here rather than creating a new one.
