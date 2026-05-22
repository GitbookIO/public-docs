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
* Your tool must support MCP over HTTP.
* If your site uses authenticated access, the MCP server uses the same access rules.
* If your site uses share links, use the share-link site URL, then add `/~gitbook/mcp`.
* GitBook supports HTTP transport only. `stdio` and `SSE` aren’t supported.

### Add the MCP link to your site

In [Site customization](../docs-site/customization/), open the [Page actions](../docs-site/customization/extra-configuration.md#page-actions) section. Then turn on **Connect with MCP server**.

This setting controls whether GitBook shows the MCP server link in the page actions menu.

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
* If the site uses authentication, use a client that supports MCP authorization.
* If the tool needs `stdio` or `SSE`, it won’t work with GitBook.

### Use MCP with authenticated sites

If your GitBook site uses [authenticated access](../site-access/authenticated-access/), the MCP server at `/~gitbook/mcp` uses the same authentication. MCP clients that support the [MCP authorization spec](https://modelcontextprotocol.io/docs/tutorials/security/authorization) — including Claude and Claude Code — can connect to the server automatically using OAuth and Dynamic Client Registration (DCR).

If your site uses share links instead, MCP still works. Use the full share-link site URL, then add `/~gitbook/mcp`.

**How it works**

When a supported MCP client connects to your authenticated site's MCP server, it:

1. Discovers the OAuth server via the MCP handshake
2. Dynamically registers an OAuth client (no manual client ID setup required)
3. Redirects you to your site's upstream auth provider to sign in
4. Exchanges the auth code for an access token and stores it locally for all subsequent requests

GitBook prompts you to authenticate the first time you connect. After that, the client reuses the token until it expires.

**Requirements**

For this flow to work, your site must use one of GitBook's supported authentication backends:

* Auth0, Azure AD, Okta, AWS Cognito, or OIDC via the native integrations
* A custom backend with a Fallback URL configured

GitBook doesn't support sites using visitor auth tokens passed as static headers for MCP authentication.
