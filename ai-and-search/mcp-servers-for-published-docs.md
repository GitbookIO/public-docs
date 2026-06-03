---
description: >-
  Each published GitBook site includes an MCP server you can connect to external
  tools
icon: mcp
---

# MCP servers for published docs

Every published GitBook site includes a Model Context Protocol (MCP) server.

AI tools can use it to read your published docs directly. This works with tools like Claude Desktop, Cursor, and VS Code extensions.

Your MCP server lives at your published site URL plus `/~gitbook/mcp`.

For example, GitBook’s docs live at `https://gitbook.com/docs`. Its MCP server is `https://gitbook.com/docs/~gitbook/mcp`.

{% hint style="info" %}
If you open this URL in a browser, you’ll see an error. Use it in a tool that can make HTTP requests, such as an AI assistant or IDE.
{% endhint %}

### Connect an AI tool

{% hint style="info" %}
**Page actions** must be enabled for the MCP server to work. If you turn off **Site customization** → **Page actions**, GitBook disables `~gitbook/mcp` and the endpoint returns `404`. **Connect with MCP server** only controls whether the MCP link appears in the page actions menu.
{% endhint %}

{% stepper %}
{% step %}
**Find your MCP server URL**

Take your published GitBook site URL. Then add `/~gitbook/mcp`.
{% endstep %}

{% step %}
**Configure your AI tool**

Open your tool’s MCP settings. Then enter the server URL.

Each tool handles setup differently. Check your tool’s docs for exact steps.
{% endstep %}

{% step %}
**Start using your docs**

Once connected, the tool can search your docs, open pages, and answer questions with your content.
{% endstep %}
{% endstepper %}

### Requirements

To use an MCP server:

* Your site must be published. The MCP server exposes published content only.
* **Page actions** must be enabled in **Site customization** → **Page actions**.
* Your tool must support MCP over HTTP.
* If your site uses authenticated access, the MCP server uses the same access rules.
* If your site uses share links, use the share-link site URL, then add `/~gitbook/mcp`.
* GitBook supports HTTP transport only. `stdio` and `SSE` aren’t supported.

### Add the MCP link to your site

In [Site customization](../docs-site/customization/), open [Page actions](../docs-site/customization/extra-configuration.md#page-actions). Make sure **Page actions** is turned on. Then turn on **Connect with MCP server**.

If **Page actions** is off, GitBook disables `~gitbook/mcp` and the endpoint returns `404`.

**Connect with MCP server** only controls whether GitBook shows the MCP server link in the page actions menu.

Visitors can then copy the server URL from the page actions menu.

### Privacy and access

The MCP server gives read-only access to your published docs.

Hidden pages remain available through MCP. Hiding a page only removes it from the published table of contents.

It never exposes account data, analytics, or internal GitBook data.

It serves the latest published version only. Drafts and unpublished changes stay private.

### Troubleshooting

If a tool can’t connect:

* Confirm your published site is reachable.
* Confirm the URL ends with `/~gitbook/mcp`.
* If the site uses authentication, use a client that supports the [MCP authorization spec](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization).
* If the tool needs `stdio` or `SSE`, it won’t work with GitBook.

### Use MCP with authenticated sites

If your GitBook site uses  [authenticated access](../site-access/authenticated-access/), the MCP server at `/~gitbook/mcp` uses the same authentication. MCP clients that support the [MCP authorization spec](https://modelcontextprotocol.io/docs/tutorials/security/authorization) — including Claude and Claude Code — can connect to the server automatically using OAuth and Dynamic Client Registration (DCR).

If your site uses share links instead, MCP still works. Use the full share-link site URL, then add `/~gitbook/mcp`.

GitBook doesn't support share-link-only sites or sites using visitor auth tokens passed as static headers for MCP authentication.

If your site uses [authenticated access](../site-access/authenticated-access/), the MCP server uses the same access rules. Public sites stay public. Protected sites require the same sign-in.

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
* [Custom backend](../publishing-documentation/authenticated-access/setting-up-a-custom-backend.md) with a configured Fallback URL

{% hint style="warning" %}
MCP authentication doesn’t support sites that rely only on static visitor auth tokens in request headers.

Use one of the authenticated access backends above instead.
{% endhint %}

To set this up, start with [Authenticated access](../site-access/authenticated-access/) and [Enabling authenticated access](../site-access/authenticated-access/enabling-authenticated-access.md).
