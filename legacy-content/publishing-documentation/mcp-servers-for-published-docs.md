---
description: >-
  Docs published on GitBook automatically generate an MCP server you can hook up
  to external tools
icon: mcp
---

# MCP servers for published docs

Every published GitBook site automatically includes a Model Context Protocol (MCP) server.

AI tools can use it to read your published docs directly. This works with Claude, Claude Code, Cursor, Codex, VS Code, and other MCP clients.

### Choose the right endpoint <a href="#choose-the-right-endpoint" id="choose-the-right-endpoint"></a>

Your MCP server lives at your published site URL plus one of these endpoints:

| If your site is...                                                                      | Use this URL                        | Example                                      |
| --------------------------------------------------------------------------------------- | ----------------------------------- | -------------------------------------------- |
| Public, shared by share link with all published content exposed, or fully authenticated | `{docs-site-url}/~gitbook/mcp`      | `https://gitbook.com/docs/~gitbook/mcp`      |
| Partially authenticated, with some public or share-link content still exposed           | `{docs-site-url}/~gitbook/mcp/auth` | `https://gitbook.com/docs/~gitbook/mcp/auth` |

For fully authenticated sites, clients sign in through MCP discovery and OAuth. For more detail, see the [MCP authorization flow](https://modelcontextprotocol.io/docs/tutorials/security/authorization#the-authorization-flow-step-by-step).

{% hint style="info" %}
If you open this URL in a browser, you’ll see an error. Use it in a tool that can make HTTP requests, such as an AI assistant or IDE.
{% endhint %}

{% hint style="info" %}
**Page actions** must be enabled for the MCP server to work. If you turn off **Site customization** → **Page actions**, GitBook disables `~gitbook/mcp` and the endpoint returns `404`. **Connect with MCP server** only controls whether the MCP link appears in the page actions menu.
{% endhint %}

### Connect an AI tool

{% stepper %}
{% step %}
#### Find your MCP server URL

Start with your published docs URL. Then add the endpoint from [Choose the right endpoint](mcp-servers-for-published-docs.md#choose-the-right-endpoint).

For example, if your docs site is `https://gitbook.com/docs`, your MCP server URL is `https://gitbook.com/docs/~gitbook/mcp`.
{% endstep %}

{% step %}
#### Add the server to your tool

Use the tab for your tool below. Replace `{docs-site-url}` with your own published site URL.

If your site uses the second endpoint, swap `/~gitbook/mcp` for `/~gitbook/mcp/auth`.
{% endstep %}

{% step %}
#### Ask a test question

Run one of the prompts in [Try it](mcp-servers-for-published-docs.md#try-it). If the tool can search your docs and answer from them, the connection works.
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="Claude" %}
These steps work in Claude on the web and in Claude Desktop.

Open **Settings** → **Connectors**.

Click **Add custom connector**. Then paste your MCP server URL, such as `{docs-site-url}/~gitbook/mcp`.

Example:

```
https://gitbook.com/docs/~gitbook/mcp
```

If Claude doesn’t show remote connectors, your current plan or rollout might not support them yet.
{% endtab %}

{% tab title="Claude Code" %}
Run this command in your terminal:

```shell
claude mcp add --transport http my-docs https://gitbook.com/docs/~gitbook/mcp
```

Replace `my-docs` with any server name you want.

If your site uses the authenticated public endpoint, replace the URL suffix with `/~gitbook/mcp/auth`.
{% endtab %}

{% tab title="Cursor" %}
Open **Settings** → **MCP**.

Click **Add new MCP server**. Then paste `{docs-site-url}/~gitbook/mcp`.

You can also add this file in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "my-docs": {
      "url": "https://gitbook.com/docs/~gitbook/mcp"
    }
  }
}
```

Replace `my-docs` with your own server name if you want.
{% endtab %}

{% tab title="Codex" %}
Use the `codex mcp add` command, or add the server to your `config.toml`.

Command example:

```shell
codex mcp add my-docs https://gitbook.com/docs/~gitbook/mcp
```

Config example:

```toml
[mcp_servers.my-docs]
url = "https://gitbook.com/docs/~gitbook/mcp"
```

Replace `my-docs` with your own server name if you want.
{% endtab %}

{% tab title="VS Code (Copilot)" %}
Open your `mcp.json` file. Then add a server entry with HTTP transport:

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

Replace `my-docs` with your own server name if you want.
{% endtab %}
{% endtabs %}

### Try it <a href="#try-it" id="try-it"></a>

Paste one of these prompts into your assistant:

* `Using the my-docs MCP server, how do I set up authenticated access?`
* `Search my docs for everything about custom domains and summarize the steps.`
* `List the tools exposed by the my-docs MCP server. Then use them to find the page about page actions.`

If you use an agentic tool, you can also give it this setup prompt:

```
Add an MCP server named my-docs with HTTP transport at https://gitbook.com/docs/~gitbook/mcp. Then verify it connects by listing its available tools.
```

### Requirements

To use an MCP server:

* Your site must be published. The MCP server exposes published content only.
* **Page actions** must be enabled in **Site customization** → **Page actions**.
* Your tool must support MCP over HTTP.
* If your site uses [authenticated access](../site-access/authenticated-access/), your tool must support the [MCP authorization spec](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization).
* If your site uses share links, use the share-link site URL, then add the endpoint from [Choose the right endpoint](mcp-servers-for-published-docs.md#choose-the-right-endpoint).
* GitBook supports HTTP transport only. `stdio` and `SSE` aren’t supported.

In the **Page actions** section of your [Customization](../docs-site/customization/) settings, you can enable the **Connect with MCP server** option. This lets visitors copy your site's MCP server URL from [the Page actions menu](../docs-site/customization/extra-configuration.md#page-actions).

### Add the MCP link to your site

In [Site customization](../docs-site/customization/), open [Page actions](../docs-site/customization/extra-configuration.md#page-actions). Make sure **Page actions** is turned on. Then turn on **Connect with MCP server**.

This adds a copyable MCP link to the page actions menu. It doesn’t change which endpoint your tool uses.

### Privacy and access

Use the endpoint from [Choose the right endpoint](mcp-servers-for-published-docs.md#choose-the-right-endpoint).

The MCP server gives read-only access to your published docs.

Hidden pages remain available through MCP. Hiding a page only removes it from the published table of contents.

It never exposes account data, analytics, or internal GitBook data.

It serves the latest published version only. Drafts and unpublished changes stay private.

### Troubleshooting

If a tool can’t connect:

* Confirm your published site is reachable.
* Confirm the URL uses the endpoint from [Choose the right endpoint](mcp-servers-for-published-docs.md#choose-the-right-endpoint).
* If the site uses authentication, use a client that supports the [MCP authorization spec](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization).
* If the tool needs `stdio` or `SSE`, it won’t work with GitBook.

### Use MCP with authenticated sites

If your GitBook site uses [authenticated access](../site-access/authenticated-access/), the MCP server at `/~gitbook/mcp` uses the same authentication. MCP clients that support the [MCP authorization spec](https://modelcontextprotocol.io/docs/tutorials/security/authorization) — including Claude and Claude Code — can connect automatically using OAuth and Dynamic Client Registration (DCR).

If your site uses share links instead, use the full share-link site URL, then add the endpoint from [Choose the right endpoint](mcp-servers-for-published-docs.md#choose-the-right-endpoint).

GitBook doesn't support share-link-only sites or sites using visitor auth tokens passed as static headers for MCP authentication.

Supported MCP clients — including Claude — follow the [MCP authorization spec](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization) to connect.

{% stepper %}
{% step %}
#### Discover the OAuth server

During the MCP handshake, the client discovers your site's OAuth server.
{% endstep %}

{% step %}
#### Register a client with DCR

The client registers an OAuth client with Dynamic Client Registration.

You don’t need to create a client ID manually.
{% endstep %}

{% step %}
#### Sign in with your site auth provider

The client redirects you to your site's auth provider.

You sign in with the same provider your docs site already uses.
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

This flow works with these authenticated access backends:

* [Auth0](../site-access/authenticated-access/setting-up-auth0.md)
* [Azure AD](../site-access/authenticated-access/setting-up-azure-ad.md)
* [Okta](../site-access/authenticated-access/setting-up-okta.md)
* [AWS Cognito](../site-access/authenticated-access/setting-up-aws-cognito.md)
* [OIDC](../site-access/authenticated-access/setting-up-oidc.md)
* [Custom backend](authenticated-access/setting-up-a-custom-backend.md) with a configured Fallback URL

{% hint style="warning" %}
MCP authentication doesn’t support sites that rely only on static visitor auth tokens in request headers.

Use one of the authenticated access backends above instead.
{% endhint %}

To set this up, start with [Authenticated access](../site-access/authenticated-access/) and [Enabling authenticated access](../site-access/authenticated-access/enabling-authenticated-access.md).
