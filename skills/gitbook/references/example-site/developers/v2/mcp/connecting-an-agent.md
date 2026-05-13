---
icon: plug-circle-bolt
description: Step-by-step setup for Claude Desktop, Cursor, Continue, Cline, and any MCP-aware client.
---

# Connecting an agent

Setup is the same for every MCP client — point it at Evolve's MCP server URL and provide an API key. The specifics of where to put that config differ per client.

## The Evolve MCP server URL

```
https://mcp.evolve.com
```

The server speaks the Streamable HTTP transport (the standard MCP HTTP transport since spec version 2025-03-26). Use a restricted API key for the agent — see [Security](README.md#security-and-permissions).

{% hint style="info" %}
**Test mode:** point at `https://mcp.test.evolve.com` and use an `sk_test_` key. The set of available tools is identical; the data they return is from your test environment.
{% endhint %}

## Connect from Claude Desktop

Open `~/Library/Application Support/Claude/claude_desktop_config.json` (or **Settings → Developer → Edit Config**) and add:

```json
{
  "mcpServers": {
    "evolve": {
      "url": "https://mcp.evolve.com",
      "headers": {
        "Authorization": "Bearer rk_live_..."
      }
    }
  }
}
```

Restart Claude Desktop. The Evolve tools appear in the new-chat tool picker as `evolve__*`.

## Connect from Cursor

In Cursor's **Settings → MCP**, add a new server:

* **Name:** `evolve`
* **Type:** `http`
* **URL:** `https://mcp.evolve.com`
* **Headers:** `Authorization: Bearer rk_live_...`

Cursor's agent panel will pick the tools up automatically.

## Connect from Continue

In `~/.continue/config.json`:

```json
{
  "mcpServers": [
    {
      "name": "evolve",
      "url": "https://mcp.evolve.com",
      "headers": {
        "Authorization": "Bearer rk_live_..."
      }
    }
  ]
}
```

## Connect from Cline (VS Code)

Open the Cline panel, click the MCP icon, **Configure MCP servers**:

```json
{
  "mcpServers": {
    "evolve": {
      "url": "https://mcp.evolve.com",
      "headers": { "Authorization": "Bearer rk_live_..." }
    }
  }
}
```

## Verifying the connection

After connecting, ask the agent:

> List the tools you have for Evolve.

You should see something like:

```
- evolve_search_customers
- evolve_get_charge
- evolve_create_refund
- evolve_get_verification_session
- evolve_search_docs
- ...
```

If the list is empty, the most common causes are a typo in the URL, a missing/expired API key, or the client not having loaded the new config (restart usually fixes this).

## Available tools

A non-exhaustive list of what the server exposes today. Each tool has typed parameters that mirror the corresponding API endpoint.

### Read tools

| Tool | Description |
| --- | --- |
| `evolve_search_customers` | Find a customer by id, email, or metadata key/value. |
| `evolve_get_customer` | Retrieve a customer by id, including saved payment methods. |
| `evolve_search_charges` | Search charges by customer, amount range, status, or time. |
| `evolve_get_charge` | Retrieve a charge by id with the full event timeline. |
| `evolve_search_refunds` | Search refunds. |
| `evolve_get_payout` | Retrieve a payout including its line items. |
| `evolve_get_balance` | Current available, pending, and reserved balance per currency. |
| `evolve_get_verification_session` | Retrieve an Identity verification session and its check results. |
| `evolve_get_connected_account` | Retrieve a Connect connected account. |
| `evolve_search_docs` | Query the public docs and return ranked text snippets. |
| `evolve_get_event` | Retrieve a webhook event by id, with delivery history. |

### Write tools (gated by key permissions)

| Tool | Description |
| --- | --- |
| `evolve_create_refund` | Issue a refund (full or partial) against a charge. |
| `evolve_capture_charge` | Capture an authorized charge. |
| `evolve_void_charge` | Void an authorized charge before capture. |
| `evolve_replay_webhook_event` | Replay a webhook event to its endpoint. |
| `evolve_pause_webhook_endpoint` | Pause a webhook endpoint. |

If a tool isn't in your key's scope, it shows up in the list with a `[restricted]` tag and the agent can see it exists but gets a permission error if it tries to call it.

## Approval and confirmation

Every MCP-aware client we've tested prompts the human before each tool call. We strongly recommend keeping that on for write tools — the audit log will show every call, but a "the agent decided to refund $5,000" surprise is not the discovery you want.

For read-only tools, most teams turn off the approval prompt to keep flow smooth. That's safe.

## Tool-call audit log

Every MCP tool call is logged to your audit log just like a regular API call. Filter by `actor_type: mcp_session` to see only agent activity:

* The session id (one per MCP connection).
* The tool name and the parameters it was called with.
* The user who's signed into the MCP client (where the client supports passing this).
* The response.

This is the trail your security team will want for any non-trivial agent-driven work.

## Limits

* **Per-session rate limit:** 60 tool calls per minute. Burst above that and the next tool call returns a friendly error suggesting the agent slow down.
* **Per-tool rate limits** apply on top of the per-session limit, mirroring the API rate limits.
* **Session lifetime:** 8 hours, after which the agent reconnects automatically.

## Troubleshooting

<details>

<summary>"The tool returns a 401"</summary>

API key missing, wrong, or revoked. Check the `Authorization` header in your client config; rotate the key if you suspect leakage.

</details>

<details>

<summary>"The agent calls a tool but says it timed out"</summary>

The MCP server has a 30-second per-tool timeout. Some search tools (especially `evolve_search_docs`) can be slow on cold cache. Retry usually works.

</details>

<details>

<summary>"I want to expose only specific tools to the agent"</summary>

Use a restricted API key scoped to just the resources you want accessible. The MCP server reflects the key's permissions automatically — tools the key can't perform don't appear in the list.

</details>

## Related

* [MCP overview](README.md) — what MCP gives you.
* [Authentication → Restricted keys](../getting-started/authentication.md#restricted-keys) — scoping the key.
* [For AI agents](../getting-started/for-ai-agents.md) — the docs-reading companion.
