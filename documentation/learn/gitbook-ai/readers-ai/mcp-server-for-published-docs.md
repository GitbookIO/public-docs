---
description: Give readers an MCP server so their AI tools can query your published docs.
---

# MCP server for published docs

Every published GitBook site automatically includes a Model Context Protocol (MCP) server. AI tools can use it to read your published docs directly — this works with Claude, Claude Code, Cursor, Codex, VS Code, and other MCP clients.

{% hint style="info" %}
This is the reader-side MCP server, for querying *published content*. Looking to connect your own coding assistant to author GitBook content instead? See Build with AI → GitBook MCP → Connect your client — a different product.
{% endhint %}

### Choose the right endpoint

Your MCP server lives at your published site URL plus one of these endpoints:

| If your site is... | Use this URL | Example |
|---|---|---|
| Public, shared by share link with all published content exposed, or fully authenticated | `{docs-site-url}/~gitbook/mcp` | `https://gitbook.com/docs/~gitbook/mcp` |
| Partially authenticated, with some public or share-link content still exposed | `{docs-site-url}/~gitbook/mcp/auth` | `https://gitbook.com/docs/~gitbook/mcp/auth` |

For fully authenticated sites, clients sign in through MCP discovery and OAuth — see the [MCP authorization flow](https://modelcontextprotocol.io/docs/tutorials/security/authorization#the-authorization-flow-step-by-step).

{% hint style="info" %}
Opening this URL in a browser shows an error — use it in a tool that can make HTTP requests, like an AI assistant or IDE.
{% endhint %}

{% hint style="info" %}
**Page actions** must be enabled for the MCP server to work. Turning off **Site customization → Configure → Page actions** disables `~gitbook/mcp`, and the endpoint returns `404`. **Connect with MCP server** only controls whether the MCP link appears in the page actions menu — see [Social sharing and custom code](../../customization/social-sharing-and-custom-code.md#page-actions).
{% endhint %}

### Connect an AI tool

{% stepper %}
{% step %}
#### Find your MCP server URL

Start with your published docs URL, then add the endpoint from [above](#choose-the-right-endpoint). For example, `https://gitbook.com/docs` becomes `https://gitbook.com/docs/~gitbook/mcp`.
{% endstep %}

{% step %}
#### Add the server to your tool

Use the tab for your tool below, replacing `{docs-site-url}` with your published site URL. If your site uses the second endpoint, swap `/~gitbook/mcp` for `/~gitbook/mcp/auth`.
{% endstep %}

{% step %}
#### Ask a test question

Try one of the prompts in [Try it](#try-it) below — if the tool can search your docs and answer from them, the connection works.
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="Claude" %}
Works in Claude on the web and in Claude Desktop.

Open **Settings → Connectors**, click **Add custom connector**, and paste your MCP server URL:

```
https://gitbook.com/docs/~gitbook/mcp
```

If Claude doesn't show remote connectors, your current plan or rollout might not support them yet.
{% endtab %}

{% tab title="Claude Code" %}
```shell
claude mcp add --transport http my-docs https://gitbook.com/docs/~gitbook/mcp
```

Replace `my-docs` with any server name you want. If your site uses the authenticated public endpoint, swap the URL suffix for `/~gitbook/mcp/auth`.
{% endtab %}

{% tab title="Cursor" %}
Open **Settings → MCP**, click **Add new MCP server**, and paste `{docs-site-url}/~gitbook/mcp`.

Or add this to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "my-docs": {
      "url": "https://gitbook.com/docs/~gitbook/mcp"
    }
  }
}
```
{% endtab %}

{% tab title="Codex" %}
```shell
codex mcp add my-docs https://gitbook.com/docs/~gitbook/mcp
```

Or in `config.toml`:

```toml
[mcp_servers.my-docs]
url = "https://gitbook.com/docs/~gitbook/mcp"
```
{% endtab %}

{% tab title="VS Code (Copilot)" %}
In your `mcp.json`, add a server entry with HTTP transport:

```json
{
  "servers": {
    "my-docs": {
      "type": "http",
      "url": "https://gitbook.com/docs/~gitbook/mcp"
    }
  }
}
```
{% endtab %}
{% endtabs %}

### Try it

Paste one of these prompts into your assistant:

* `Using the my-docs MCP server, how do I set up authenticated access?`
* `Search my docs for everything about custom domains and summarize the steps.`
* `List the tools exposed by the my-docs MCP server. Then use them to find the page about page actions.`

For an agentic tool, you can also give it a setup prompt directly:

```
Add an MCP server named my-docs with HTTP transport at https://gitbook.com/docs/~gitbook/mcp. Then verify it connects by listing its available tools.
```

### Requirements

* Your site must be published — the MCP server exposes published content only.
* **Page actions** must be enabled, under **Site customization → Configure → Page actions**.
* Your tool must support MCP over HTTP.
* If your site uses [authenticated access](../../access/authenticated-access/README.md), your tool must support the [MCP authorization spec](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization).
* If your site uses share links, use the share-link site URL, then add the endpoint from [above](#choose-the-right-endpoint).
* GitBook supports HTTP transport only — `stdio` and `SSE` aren't supported.

### Add the MCP link to your site

In [Site customization](../../customization/README.md), open **Configure → Page actions**. Make sure **Page actions** is on, then turn on **Connect with MCP server** — this adds a copyable MCP link to the page actions menu. It doesn't change which endpoint your tool uses.

### Privacy and access

The MCP server gives read-only access to your published docs, using the endpoint from [above](#choose-the-right-endpoint). Hidden pages remain available through MCP — hiding a page only removes it from the published table of contents. It never exposes account data, analytics, or internal GitBook data, and serves only the latest published version — drafts and unpublished changes stay private.

### Troubleshooting

If a tool can't connect:

* Confirm your published site is reachable.
* Confirm the URL uses the correct endpoint from [above](#choose-the-right-endpoint).
* If the site uses authentication, use a client that supports the [MCP authorization spec](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization).
* If the tool needs `stdio` or `SSE`, it won't work with GitBook.

### Use MCP with authenticated sites

If your site uses [authenticated access](../../access/authenticated-access/README.md), the MCP server at `/~gitbook/mcp` uses the same authentication. MCP clients that support the [MCP authorization spec](https://modelcontextprotocol.io/docs/tutorials/security/authorization) — including Claude and Claude Code — connect automatically using OAuth and Dynamic Client Registration (DCR).

If your site uses share links instead, use the full share-link site URL, then add the endpoint from [above](#choose-the-right-endpoint). GitBook doesn't support share-link-only sites, or sites using visitor auth tokens passed as static headers, for MCP authentication.

{% stepper %}
{% step %}
#### Discover the OAuth server

During the MCP handshake, the client discovers your site's OAuth server.
{% endstep %}

{% step %}
#### Register a client with DCR

The client registers an OAuth client with Dynamic Client Registration — you don't need to create a client ID manually.
{% endstep %}

{% step %}
#### Sign in with your site's auth provider

The client redirects you to sign in with the same provider your docs site already uses.
{% endstep %}

{% step %}
#### Exchange the code for a token

After sign-in, the client exchanges the authorization code for an access token.
{% endstep %}

{% step %}
#### Reuse the token

The client sends that token with later MCP requests until it expires.
{% endstep %}
{% endstepper %}

This flow works with: [Auth0](../../access/authenticated-access/auth0.md), [Azure AD](../../access/authenticated-access/azure-ad.md), [Okta](../../access/authenticated-access/okta.md), [AWS Cognito](../../access/authenticated-access/aws-cognito.md), [OIDC](../../access/authenticated-access/oidc.md), and a [custom backend](../../access/authenticated-access/custom-backend.md) with a configured fallback URL.

{% hint style="warning" %}
MCP authentication doesn't support sites relying only on static visitor auth tokens in request headers — use one of the authenticated access backends above instead.
{% endhint %}

To set this up, start with [Authenticated access](../../access/authenticated-access/README.md).
