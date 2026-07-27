---
description: Authenticate your MCP client with GitBook via OAuth or a personal access token.
---

# Authenticate your agent

GitBook MCP supports two authentication methods: OAuth and personal access tokens.

{% tabs %}
{% tab title="OAuth" %}
Point your client at the MCP server URL (`https://mcp.gitbook.com/mcp`). The client discovers the authorization server, registers itself, and opens the browser sign-in flow automatically.

If you use OAuth, don't add a bearer token manually — the client gets one during sign-in.
{% endtab %}

{% tab title="Personal access token" %}
To skip the browser flow, send your token as a bearer token:

```http
Authorization: Bearer <YOUR_PAT>
```

Create a personal access token in your [developer settings](https://app.gitbook.com/account/developer). Use this for scripted setups, or when your client already manages secrets locally.
{% endtab %}
{% endtabs %}

### What to expect during the OAuth flow

When authentication works, the flow usually looks like this:

1. The client connects to the MCP server.
2. Your browser opens the sign-in flow.
3. You sign in and approve access.
4. The client shows the server as connected, or the MCP tools become available.

If something looks stuck partway through, see [Troubleshooting](../reference/troubleshooting.md).
