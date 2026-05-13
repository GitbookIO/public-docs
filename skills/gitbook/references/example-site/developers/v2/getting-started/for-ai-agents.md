---
icon: robot
description: How AI agents and code copilots can navigate the Evolve docs and call the API directly.
---

# For AI agents

Evolve publishes structured indexes and a hosted MCP server so AI assistants can find what they need without spidering HTML. If you're building an agent that integrates with Evolve, or you're using a code copilot to write Evolve integrations, this page is the entry point.

## llms.txt and llms-full.txt

We follow the [llms.txt convention](https://llmstxt.org). Two files at the docs root:

| File | Contents | Best for |
| --- | --- | --- |
| [https://docs.evolve.com/llms.txt](https://gitbook.com) | Title, description, and a curated list of links to every section of the docs. | Agents that need a map of the docs to navigate by. |
| [https://docs.evolve.com/llms-full.txt](https://gitbook.com) | The complete content of every public page concatenated into one file. | Agents that want the full docs in their context window. |

Both are auto-generated from the same content as the rendered docs site, and refreshed on every publish. Cache for at most an hour.

### Using llms.txt

```
# Evolve API documentation

> The Evolve API lets you accept payments, verify identities, and run a marketplace platform.

## API references
- [Payments API](https://gitbook.com): charges, refunds, payouts
- [Identity API](https://gitbook.com): document and bank verification
- [Connect API](https://gitbook.com): connected accounts, transfers
- ...
```

The structured Markdown lets an agent decide what to fetch in detail without loading the whole site.

### Using llms-full.txt

For a single full-context dump, `llms-full.txt` concatenates every public page in the docs into one file (~2 MB plain text). Useful when an agent has the context budget to read everything, or for offline reference materials.

## MCP — call the Evolve API as an agent

The structured-text indexes above are about *reading* the docs. If you want an agent to *call the API* directly during a session — query a charge, refund a payment, look up a customer — Evolve runs an [MCP server](../mcp/README.md) that exposes the API as agent tools.

Connecting takes about a minute and works with Claude Desktop, Cursor, Continue, Cline, and any other MCP-aware client. See [MCP → Connecting an agent](../mcp/connecting-an-agent.md).

## Best practices for agent integrations

A few patterns we've seen work well — and a couple to avoid.

<details>

<summary>Use restricted keys for agent access</summary>

If an agent calls the API on behalf of an end user, scope the key to the operations the agent should be able to perform. A read-only restricted key is the right default for assistant-style integrations; a refund-only or charge-only key is right for narrower automations.

</details>

<details>

<summary>Pin the API version</summary>

Agents calling the API should pin `Evolve-Version` explicitly. Auto-default versions can shift under you if your account upgrades; explicit pinning gives the agent reproducible behavior.

</details>

<details>

<summary>Don't let the agent generate idempotency keys</summary>

The agent can request an operation, but the idempotency key should come from your code — generated once per logical operation and persisted before the call. Otherwise a re-run of the agent will produce duplicate operations.

</details>

<details>

<summary>Surface dry-run results to the user before committing</summary>

For destructive operations (refunds, account terminations, payout cancellations), have the agent show what it's about to do and require confirmation. The Evolve API has no built-in dry-run, so the agent should describe the operation in human language before calling.

</details>

## Discoverability extras

Beyond `llms.txt`, the docs also expose:

* **`/sitemap.xml`** — full URL list, for agents that prefer XML.
* **`/.well-known/ai-plugin.json`** — OpenAPI plugin manifest pointing at our specs.
* **OpenAPI specs** — published at predictable URLs:
  * <code class="expression">space.vars.docs_root</code>/openapi/payments.yaml
  * <code class="expression">space.vars.docs_root</code>/openapi/identity.yaml
  * <code class="expression">space.vars.docs_root</code>/openapi/connect.yaml

All four are kept in sync with the live API on every release.

## Related

* [MCP overview](../mcp/README.md) — the agent-callable side of Evolve.
* [Authentication](authentication.md) — restricted keys for scoped agent access.
* [API references](../payments-api/README.md) — for the agent to read.
