---
description: Connect Claude, Cursor, or any MCP client to the GitBook MCP server.
---

# Connect your client

Add GitBook MCP in your client of choice.

{% tabs %}
{% tab title="Claude Code" %}
Register the server in your terminal:

```bash
claude mcp add --transport http gitbook https://mcp.gitbook.com/mcp
```

Then start Claude Code with `claude` and run `/mcp` to finish the browser sign-in.

If you prefer a personal access token, pass it as an authorization header:

```bash
claude mcp add --transport http gitbook https://mcp.gitbook.com/mcp \
  --header "Authorization: Bearer <YOUR_TOKEN>"
```
{% endtab %}

{% tab title="Codex" %}
Add the server from your terminal:

```bash
codex mcp add gitbook --url https://mcp.gitbook.com/mcp
```

Then sign in through the browser.

To use a personal access token instead, add this to `~/.codex/config.toml`:

```toml
[mcp_servers.gitbook]
url = "https://mcp.gitbook.com/mcp"
bearer_token_env_var = "GITBOOK_MCP_TOKEN"
enabled = true
```
{% endtab %}

{% tab title="Cursor" %}
Add the server to `~/.cursor/mcp.json`, or to your project at `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "gitbook": {
      "url": "https://mcp.gitbook.com/mcp"
    }
  }
}
```

Then sign in when Cursor prompts you.
{% endtab %}

{% tab title="VS Code" %}
Add the server to `.vscode/mcp.json` in your workspace:

```json
{
  "servers": {
    "gitbook": {
      "type": "http",
      "url": "https://mcp.gitbook.com/mcp"
    }
  }
}
```

Then start it from the MCP view and sign in.
{% endtab %}

{% tab title="Other" %}
Any MCP-compatible client can connect over streamable HTTP. Point it at:

```
https://mcp.gitbook.com/mcp
```

GitBook supports streamable HTTP only — `stdio` and `SSE` aren't supported.

If you use OAuth, you usually don't need any extra auth fields. If you use a personal access token instead, send it as a bearer token:

```http
Authorization: Bearer <YOUR_PAT>
```
{% endtab %}
{% endtabs %}

See [Authenticate your agent](../getting-started/authenticate-your-agent.md) for more on the two authentication methods, and [Troubleshooting](../reference/troubleshooting.md) if a client doesn't seem to connect.
