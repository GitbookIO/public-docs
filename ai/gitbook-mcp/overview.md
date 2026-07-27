---
description: Connect an MCP client and drive GitBook through the MCP server.
---

# Work through the GitBook MCP server

GitBook exposes an MCP server that lets AI tools act on content in your organization. Tools like Claude Code, Codex, Cursor, and other MCP clients can use it to create and configure sites, open change requests, draft content, edit pages, and restructure docs.

To connect your AI coding assistant to GitBook's MCP, you need the server URL, an authentication method, and a supported MCP client — the sections below walk through each.

{% hint style="info" %}
Need a read-only MCP server for a *published* docs site instead? GitBook creates one automatically — see Documentation → GitBook AI → "MCP server for published docs".
{% endhint %}

### GitBook's MCP endpoint

Point your MCP client at:

```
https://mcp.gitbook.com/mcp
```

{% hint style="info" %}
Opening this URL in a browser returns an error — use it in an MCP client that can make HTTP requests.
{% endhint %}

* [Connect your client](connect-your-client.md) — per-client setup (Claude Code, Codex, Cursor, VS Code, and others).
* [Common workflows](common-workflows.md) — everyday things to ask your agent to do.
* [MCP tools reference](mcp-tools-reference.md) — every tool the server exposes.

### GitBook MCP vs. published docs MCP

GitBook has two MCP patterns:

* **MCP server for published docs** gives AI tools read-only access to published content — for documentation readers and end users finding information in your published docs.
* **GitBook MCP** (this page) gives AI tools access to your content and workflows through the GitBook API — for your team's agents to edit and manage documentation through automated workflows.

See [Which MCP server do I need?](../reference/which-mcp-server-do-i-need.md) for the full comparison.
