---
description: The authoring MCP server vs. the published-docs MCP server, side by side.
---

# Which MCP server do I need?

GitBook has two MCP servers, built for opposite sides of your documentation. If you've landed here confused about which one you need, this table should settle it:

| | GitBook MCP (this section) | MCP server for published docs |
|---|---|---|
| **Who connects to it** | You and your team's agents, authoring content | Your readers' AI tools, consuming your published docs |
| **Access** | Your content and workflows, through the GitBook API | Read-only access to *published* content only |
| **Endpoint** | `https://mcp.gitbook.com/mcp` | `{your-published-site-url}/~gitbook/mcp` (a different endpoint per site) |
| **What it's for** | Creating sites, opening change requests, drafting and editing content, restructuring docs | Letting AI tools discover and retrieve your published docs as resources — no scraping required |
| **Where it's documented** | [Work through the GitBook MCP server](../gitbook-mcp/overview.md) | Documentation → GitBook AI → "MCP server for published docs" |

**Use GitBook MCP** when you want your own agents — Claude Code, Cursor, Codex, or similar — to edit and manage your documentation through automated workflows.

**Use the published-docs MCP server** when you want documentation readers and end users to find information from your already-published docs, using their own AI tools.

They're unrelated in setup: connecting one doesn't affect or require the other, and a single organization can have both in use at once — your team authoring through GitBook MCP, while your published site simultaneously serves readers' AI tools through its own server.
