---
description: Build on Evolve — APIs, SDKs, webhooks, and AI-agent access for every product.
icon: code
cover: .gitbook/assets/developers-cover.png
coverY: 0
layout:
  width: wide
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Developers

{% columns %}
{% column width="50%" %}
Build with Evolve. The Developers space is the source of truth for APIs, SDKs, webhooks, and the agent integrations across all three products — [Payments](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/), [Identity](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/), and [Connect](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/).

**Looking for product workflows and concepts?** Those live in the product spaces — this space is the technical reference.
{% endcolumn %}

{% column width="50%" %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

This space demonstrates **variants** — three Git-Synced spaces (`v1`, `v2`, `v3`) appear as a single dropdown in the top bar. Switch between them to see how the Payments API differs across versions. The Reference pages are **auto-rendered from OpenAPI specs** in `developers/openapi/v2/`. Code samples on the Quickstart and Authentication pages use the **tabs block** for Node, Python, Go, Ruby, and cURL.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

## Pick your path

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-rocket" style="color:$primary;">:rocket:</i></h4></td><td><strong>Quickstart</strong></td><td>Make your first API call in under five minutes.</td><td><a href="getting-started/quickstart.md">quickstart.md</a></td></tr><tr><td><h4><i class="fa-key" style="color:$primary;">:key:</i></h4></td><td><strong>Authentication</strong></td><td>Keys, scopes, and signature verification.</td><td><a href="getting-started/authentication.md">authentication.md</a></td></tr><tr><td><h4><i class="fa-cubes" style="color:$primary;">:cubes:</i></h4></td><td><strong>SDKs</strong></td><td>Node, Python, Go, Ruby — official and idiomatic.</td><td><a href="getting-started/sdks.md">sdks.md</a></td></tr><tr><td><h4><i class="fa-list-ul" style="color:$primary;">:list-ul:</i></h4></td><td><strong>Conventions</strong></td><td>Errors, idempotency, pagination, rate limits.</td><td><a href="getting-started/conventions.md">conventions.md</a></td></tr></tbody></table>

## API references

Each product has its own auto-generated reference. Endpoints, parameters, response shapes, and an interactive **Test it** panel for every operation.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-credit-card" style="color:$primary;">:credit-card:</i></h4></td><td><strong>Payments API</strong></td><td>Charges, refunds, payouts, balance.</td><td><a href="payments-api/">payments-api</a></td></tr><tr><td><h4><i class="fa-id-card" style="color:$primary;">:id-card:</i></h4></td><td><strong>Identity API</strong></td><td>Verification sessions, documents, bank checks.</td><td><a href="identity-api/">identity-api</a></td></tr><tr><td><h4><i class="fa-circles-overlap" style="color:$primary;">:circles-overlap:</i></h4></td><td><strong>Connect API</strong></td><td>Connected accounts, transfers, checkout sessions.</td><td><a href="connect-api/">connect-api</a></td></tr><tr><td><h4><i class="fa-bolt" style="color:$primary;">:bolt:</i></h4></td><td><strong>Webhooks</strong></td><td>Event catalog and signature verification.</td><td><a href="webhooks/">webhooks</a></td></tr></tbody></table>

## For AI agents

Evolve publishes structured indexes for AI agents and code copilots — `llms.txt` and `llms-full.txt` — so an agent landing on these docs can navigate efficiently or load the whole content set into context. We also expose Evolve itself as an [MCP server](mcp/) so an agent can call the API directly during a session.

<a href="getting-started/for-ai-agents.md" class="button secondary">Agent integration guide</a> <a href="mcp/" class="button secondary">MCP server</a>

## Synced with GitHub

These docs are bidirectionally synced with the [evolve-pay/docs](https://github.com/GitbookIO/evolve-demo) repository. Edits in the GitBook editor flow back to GitHub as commits; changes pushed to the repo (including PRs from contributors) propagate to the published docs after merge. Contribute via PR or via the **Edit in GitHub** badge in the page header.

## Conventions at a glance

A short version of what's covered in detail under [Conventions](getting-started/conventions.md):

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><h3><i class="fa-globe" style="color:$primary;">:globe:</i> <strong>Base URLs</strong></h3></td><td>Live: <code class="expression">space.vars.api_live</code><br>Test: <code class="expression">space.vars.api_test</code></td></tr><tr><td><h3><i class="fa-tag" style="color:$primary;">:tag:</i> <strong>Versioning</strong></h3></td><td>Date-pinned via the <code>Evolve-Version</code> header. Default: <code class="expression">space.vars.api_version</code>. Major shape changes ship as variants — <code>v1</code>, <code>v2</code>, <code>v3</code>.</td></tr><tr><td><h3><i class="fa-list" style="color:$primary;">:list:</i> <strong>Pagination</strong></h3></td><td>Cursor-based. 100 per page default, 1000 max. <code>has_more</code> and <code>next_cursor</code> on every list.</td></tr><tr><td><h3><i class="fa-gauge-high" style="color:$primary;">:gauge-high:</i> <strong>Rate limits</strong></h3></td><td>500 requests/second on Growth, custom on Enterprise. <code>X-RateLimit-*</code> headers on every response.</td></tr></tbody></table>

## Get help

{% columns %}
{% column width="50%" %}
#### Talk to support

For account-specific questions, integration help, or production incidents, open a ticket from the dashboard.

<a href="https://gitbook.com" class="button primary">Open a ticket</a>
{% endcolumn %}

{% column width="50%" %}
#### Status and changelog

Real-time platform status and the running list of API changes.

<a href="https://gitbook.com" class="button secondary">Status page</a> <a href="https://app.gitbook.com/s/ErQsbFsgm6eg9BApdmPl/" class="button secondary">Changelog</a>
{% endcolumn %}
{% endcolumns %}
