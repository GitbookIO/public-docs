---
description: >-
  Connect an AI agent to Evolve via Model Context Protocol — query the API, take
  actions, get docs context.
icon: plug
---

# Overview

Evolve runs a hosted [Model Context Protocol](https://modelcontextprotocol.io) server that exposes the Evolve API as a set of tools an AI agent can call directly. Connect once and your agent — Claude Desktop, Cursor, Continue, Cline, or any MCP-aware client — can read your account, look up customers, refund payments, and inspect verification sessions during a conversation.

This is for the _interactive_ side of agent integrations. For agents that just need to read the docs, see [llms.txt and llms-full.txt](../getting-started/for-ai-agents.md).

## What MCP gives you

When connected, your agent can:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-magnifying-glass" style="color:$primary;">:magnifying-glass:</i></h4></td><td><strong>Look things up</strong></td><td>Find a customer, charge, payout, or verification by id, email, or amount.</td><td></td></tr><tr><td><h4><i class="fa-bolt-lightning" style="color:$primary;">:bolt-lightning:</i></h4></td><td><strong>Take actions</strong></td><td>Issue refunds, capture authorizations, retry failed payouts, replay webhooks.</td><td></td></tr><tr><td><h4><i class="fa-book-open" style="color:$primary;">:book-open:</i></h4></td><td><strong>Pull context from the docs</strong></td><td>The same docs you're reading, queryable by the agent for grounded answers.</td><td></td></tr></tbody></table>

## What it doesn't do

* **It's not autonomous.** The agent calls tools on your behalf, with your approval (most clients prompt before each tool call). Evolve doesn't run an agent of its own.
* **It's not a replacement for the API.** Production code should call the API directly with an SDK. MCP is for human-in-the-loop debugging, customer support, and assistant-style workflows.
* **It doesn't bypass your security.** Tools are scoped to the API key you connect with. A read-only key gives the agent read-only abilities, full stop.

## Quick example — what a session looks like

A support agent in Claude Desktop, after connecting Evolve via MCP:

> **You:** Customer at jordan@acme.com is asking why their last payment failed. What happened?
>
> **Claude:** \[Calls `evolve_search_customers` tool] Found one match — `cus_4n2P3qR5sT6uV`. Their most recent payment was `ch_8f2K3pL9qX` for $128.00 on April 28, which **failed with `card_declined` (decline\_code: insufficient\_funds)**. The card was the one they used successfully twice before. Want me to draft an email asking them to try another card?

The agent did two things: searched for the customer, then retrieved the failed charge — without you leaving the chat or opening the dashboard.

## Connect

Setup takes about a minute, no install required.

<a href="connecting-an-agent.md" class="button primary">Set it up</a>

## Available tools

The MCP server exposes one tool per common operation. The full list is at [Connecting an agent → Available tools](connecting-an-agent.md#available-tools); a representative slice:

| Tool                              | What it does                                               |
| --------------------------------- | ---------------------------------------------------------- |
| `evolve_search_customers`         | Find a customer by id, email, or metadata.                 |
| `evolve_get_charge`               | Fetch a charge by id, with full timeline.                  |
| `evolve_create_refund`            | Issue a refund (full or partial).                          |
| `evolve_get_verification_session` | Inspect an Identity verification result.                   |
| `evolve_search_docs`              | Query the public Evolve docs and get back ranked snippets. |

## Security and permissions

The MCP server authenticates with an Evolve API key. We strongly recommend a [restricted key](../getting-started/authentication.md#restricted-keys) scoped to the minimum permissions the agent needs.

For interactive support work, a typical scoping:

* **Read** on charges, customers, refunds, payouts, verifications.
* **Write** on refunds (so the agent can issue them with your approval).
* **No write** on anything else (no creating charges, no creating connected accounts, no rolling keys).

Every tool call is logged to your [audit log](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/compliance/audit-logs) just like a regular API call, with a special `actor_type: mcp_session` so you can filter for agent activity.

## Related

* [Connecting an agent](connecting-an-agent.md) — step-by-step setup for Claude, Cursor, and others.
* [For AI agents](../getting-started/for-ai-agents.md) — the docs-side companion (`llms.txt`).
* [Authentication → Restricted keys](../getting-started/authentication.md#restricted-keys) — scoping access.
