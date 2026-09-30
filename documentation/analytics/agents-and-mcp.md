---
description: Track how LLMs, coding agents, and crawlers read your documentation
---

# Agents & MCP

The **Agents & MCP** report covers everything reading your site that isn’t a person: LLMs, coding agents, crawlers, and any tool connected to your site’s [MCP server](../ai-for-your-readers/mcp-servers-for-published-docs.md).

To open it, go to **Analyze → Agents & MCP** in your site’s sidebar.

At the top, you’ll see the pages agents read, their share of everything read on your site, and the number of MCP calls. Below that, **Who reads this site** splits reads between people and agents, so you can watch that balance shift over time. See [insights.md](insights.md "mention") for filters, time periods, and comparing periods.

### Surfaces

Agents reach your content through several surfaces, and the report counts each one:

* **Markdown**: pages requested as `.md`.
* **llms.txt**: your [LLM-ready](../getting-started/llm-ready-docs.md) index files.
* **MCP**: reads through your site’s MCP server.
* **Site page views** and **RSS**: agents reading your site the way a browser would.

### MCP activity

Three cards cover what tools did with your docs: the **MCP tools** they called, the **MCP search queries** they ran, and the **pages they read through MCP**. Together they show which parts of your documentation your product’s AI integrations depend on.

### Which agents, and what they read

**Agents** ranks the clients reading your site. Pick a surface to see who reads through it. Clients that don’t identify themselves are grouped as **Unidentified**.

**Pages read** ranks your content by how much agents read it, on the surface they read it through.

{% hint style="info" %}
If agents rarely reach your content, see [llm-ready-docs.md](../getting-started/llm-ready-docs.md "mention") for how to make your site easier for AI tools to discover and read.
{% endhint %}
