---
description: >-
  Create and publish AI-native documentation your users will love. GitBook gives
  you intelligent tools to build product guides, API references, and
  documentation that improves over time.
icon: book-open
layout:
  width: wide
  title:
    visible: false
  description:
    visible: false
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
  actions:
    visible: true
---

# Overview

{% columns %}
{% column width="33.33333333333333%" %}
## Publish your documentation in under 5 minutes

Publishing your docs with GitBook is as simple as asking your agent

<a href="https://app.gitbook.com/" class="button primary">Sign up</a><a href="https://www.gitbook.com/enterprise" class="button secondary">Get a demo</a>
{% endcolumn %}

{% column width="66.66666666666667%" %}
{% code overflow="wrap" expandable="true" %}
````md
# GitBook Setup Agent

## Task
Take my docs and turn them into a live, published GitBook site. Go end-to-end — don't stop until it's live or you hit a step only I can do.

## Tooling
You have two ways to work with GitBook. Check what's available and pick accordingly:

1. **GitBook MCP server** (preferred if already connected) — check your available tools for `gitbook-mcp`. If it's connected, use it.
2. **GitBook skill** (fallback, or if I ask for it) — if the MCP server isn't installed and can't be added, install the skill instead:
```bash
   npx skills add GitbookIO/gitbook-skills
```
   Then follow the skill's instructions to drive the GitBook REST API directly. This path requires a GitBook API token (PAT) from me — ask for it if you don't have one.

## Setting up the MCP server (if not connected)
Connect to `https://mcp.gitbook.com/mcp`. Use OAuth unless I give you a PAT.

**Claude Code:**
```bash
claude mcp add --transport http gitbook-mcp https://mcp.gitbook.com/mcp
```
(with PAT, add `--header "Authorization: Bearer <YOUR_PAT>"`) — then run `/mcp` to auth/verify.

**Codex:**
```bash
codex mcp add gitbook-mcp --url https://mcp.gitbook.com/mcp
```
(for PAT, set `GITBOOK_MCP_TOKEN` and add a `[mcp_servers.gitbook-mcp]` block with `bearer_token_env_var` to `~/.codex/config.toml`) — verify with `codex mcp list`.

If MCP setup fails or isn't supported in this environment, fall back to the skill (option 2 above) rather than stopping.

## Import Docs
Once you have a working connection (MCP or skill), pull in my existing docs (point me to a folder, repo, or other docs site if you need one) and set up the site, structure, and content from there. Either path should end in the same result: a structured, published site.
````
{% endcode %}

<p align="center"><a href="claude://code/new?q=%23%20GitBook%20Setup%20Agent%0A%23%23%20Task%0ATake%20my%20docs%20and%20turn%20them%20into%20a%20live%2C%20published%20GitBook%20site%2C%20using%20the%20GitBook%20MCP%20server.%20Go%20end-to-end%20%E2%80%94%20don%27t%20stop%20until%20it%27s%20live%20or%20you%20hit%20a%20step%20only%20I%20can%20do.%0A%23%23%20Getting%20Started%0AConnect%20to%20the%20GitBook%20MCP%20server%3A%20%60https%3A//mcp.gitbook.com/mcp%60.%20Use%20OAuth%20unless%20I%20give%20you%20a%20PAT.%0A%2A%2AClaude%20Code%3A%2A%2A%0A%60%60%60bash%0Aclaude%20mcp%20add%20--transport%20http%20gitbook-mcp%20https%3A//mcp.gitbook.com/mcp%0A%60%60%60%0A%28with%20PAT%2C%20add%20%60--header%20%22Authorization%3A%20Bearer%20%3CYOUR_PAT%3E%22%60%29%20%E2%80%94%20then%20run%20%60/mcp%60%20to%20auth/verify.%0A%2A%2ACodex%3A%2A%2A%0A%60%60%60bash%0Acodex%20mcp%20add%20gitbook-mcp%20--url%20https%3A//mcp.gitbook.com/mcp%0A%60%60%60%0A%28for%20PAT%2C%20set%20%60GITBOOK_MCP_TOKEN%60%20and%20add%20a%20%60%5Bmcp_servers.gitbook-mcp%5D%60%20block%20with%20%60bearer_token_env_var%60%20to%20%60~/.codex/config.toml%60%29%20%E2%80%94%20verify%20with%20%60codex%20mcp%20list%60.%0A%23%23%20Import%20Docs%0AOnce%20connected%2C%20pull%20in%20my%20existing%20docs%20%28point%20me%20to%20a%20folder%2C%20repo%2C%20or%20other%20docs%20site%20if%20you%20need%20one%29%20and%20use%20the%20MCP%20server%20to%20set%20up%20the%20site%2C%20structure%2C%20and%20content%20from%20there." class="button secondary">Claude Code</a><a href="cursor://anysphere.cursor-deeplink/prompt?text=%23%20GitBook%20Setup%20Agent%0A%23%23%20Task%0ATake%20my%20docs%20and%20turn%20them%20into%20a%20live%2C%20published%20GitBook%20site%2C%20using%20the%20GitBook%20MCP%20server.%20Go%20end-to-end%20%E2%80%94%20don%27t%20stop%20until%20it%27s%20live%20or%20you%20hit%20a%20step%20only%20I%20can%20do.%0A%23%23%20Getting%20Started%0AConnect%20to%20the%20GitBook%20MCP%20server%3A%20%60https%3A//mcp.gitbook.com/mcp%60.%20Use%20OAuth%20unless%20I%20give%20you%20a%20PAT.%0A%2A%2AClaude%20Code%3A%2A%2A%0A%60%60%60bash%0Aclaude%20mcp%20add%20--transport%20http%20gitbook-mcp%20https%3A//mcp.gitbook.com/mcp%0A%60%60%60%0A%28with%20PAT%2C%20add%20%60--header%20%22Authorization%3A%20Bearer%20%3CYOUR_PAT%3E%22%60%29%20%E2%80%94%20then%20run%20%60/mcp%60%20to%20auth/verify.%0A%2A%2ACodex%3A%2A%2A%0A%60%60%60bash%0Acodex%20mcp%20add%20gitbook-mcp%20--url%20https%3A//mcp.gitbook.com/mcp%0A%60%60%60%0A%28for%20PAT%2C%20set%20%60GITBOOK_MCP_TOKEN%60%20and%20add%20a%20%60%5Bmcp_servers.gitbook-mcp%5D%60%20block%20with%20%60bearer_token_env_var%60%20to%20%60~/.codex/config.toml%60%29%20%E2%80%94%20verify%20with%20%60codex%20mcp%20list%60.%0A%23%23%20Import%20Docs%0AOnce%20connected%2C%20pull%20in%20my%20existing%20docs%20%28point%20me%20to%20a%20folder%2C%20repo%2C%20or%20other%20docs%20site%20if%20you%20need%20one%29%20and%20use%20the%20MCP%20server%20to%20set%20up%20the%20site%2C%20structure%2C%20and%20content%20from%20there." class="button secondary">Cursor</a><a href="codex://threads/new?prompt=%23%20GitBook%20Setup%20Agent%0A%23%23%20Task%0ATake%20my%20docs%20and%20turn%20them%20into%20a%20live%2C%20published%20GitBook%20site%2C%20using%20the%20GitBook%20MCP%20server.%20Go%20end-to-end%20%E2%80%94%20don%27t%20stop%20until%20it%27s%20live%20or%20you%20hit%20a%20step%20only%20I%20can%20do.%0A%23%23%20Getting%20Started%0AConnect%20to%20the%20GitBook%20MCP%20server%3A%20%60https%3A//mcp.gitbook.com/mcp%60.%20Use%20OAuth%20unless%20I%20give%20you%20a%20PAT.%0A%2A%2AClaude%20Code%3A%2A%2A%0A%60%60%60bash%0Aclaude%20mcp%20add%20--transport%20http%20gitbook-mcp%20https%3A//mcp.gitbook.com/mcp%0A%60%60%60%0A%28with%20PAT%2C%20add%20%60--header%20%22Authorization%3A%20Bearer%20%3CYOUR_PAT%3E%22%60%29%20%E2%80%94%20then%20run%20%60/mcp%60%20to%20auth/verify.%0A%2A%2ACodex%3A%2A%2A%0A%60%60%60bash%0Acodex%20mcp%20add%20gitbook-mcp%20--url%20https%3A//mcp.gitbook.com/mcp%0A%60%60%60%0A%28for%20PAT%2C%20set%20%60GITBOOK_MCP_TOKEN%60%20and%20add%20a%20%60%5Bmcp_servers.gitbook-mcp%5D%60%20block%20with%20%60bearer_token_env_var%60%20to%20%60~/.codex/config.toml%60%29%20%E2%80%94%20verify%20with%20%60codex%20mcp%20list%60.%0A%23%23%20Import%20Docs%0AOnce%20connected%2C%20pull%20in%20my%20existing%20docs%20%28point%20me%20to%20a%20folder%2C%20repo%2C%20or%20other%20docs%20site%20if%20you%20need%20one%29%20and%20use%20the%20MCP%20server%20to%20set%20up%20the%20site%2C%20structure%2C%20and%20content%20from%20there." class="button secondary">Codex</a></p>
{% endcolumn %}
{% endcolumns %}

#### Quickstart guides

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-robot">:robot:</i></h4></td><td><h4>AI Quickstart</h4></td><td><a href="getting-started/ai-documentation/">ai-documentation</a></td></tr><tr><td><h4><i class="fa-hand-pointer">:hand-pointer:</i></h4></td><td><h4>Editor Quickstart</h4></td><td><a href="getting-started/quickstart.md">quickstart.md</a></td></tr></tbody></table>

#### Explore GitBook's features

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-card-cover-dark data-type="image">Cover image (dark)</th></tr></thead><tbody><tr><td><h4>GitBook Agent</h4></td><td><a href="gitbook-agent/write-and-edit-with-ai.md">Writing with GitBook Agent</a></td><td><a href="gitbook-agent/review-change-requests-with-gitbook-agent.md">Review change requests</a></td><td><a href="gitbook-agent/identifying-content-gaps.md">Identify content gaps</a></td><td><a href="publishing-documentation/channels.md">Channels</a></td><td><a href=".gitbook/assets/GitBook Agent.png">GitBook Agent.png</a></td><td><a href=".gitbook/assets/GitBook Agent - dark.png">GitBook Agent - dark.png</a></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td><h4>GitBook Assistant</h4></td><td><a href="ai-and-search/connections/">Connections</a></td><td><a href="docs-site/embedding/">Docs Embed</a></td><td><a href="docs-site/embedding/configuration/creating-custom-tools.md">Connect to custom tools</a></td><td></td><td><a href=".gitbook/assets/GitBook Assistant.png">GitBook Assistant.png</a></td><td></td><td><a href=".gitbook/assets/GitBook Assistant - dark.png">GitBook Assistant - dark.png</a></td><td></td><td></td><td></td><td></td></tr><tr><td><h4>Git Sync</h4></td><td><a href="getting-started/git-sync/enabling-github-sync.md">Enabling GitHub Sync</a></td><td><a href="getting-started/git-sync/content-configuration.md">Content configuration</a></td><td><a href="getting-started/git-sync/github-pull-request-preview.md">GitHub pull request preview</a></td><td><a href="getting-started/git-sync/monorepos.md">Monorepos</a></td><td><a href=".gitbook/assets/Git Sync.png">Git Sync.png</a></td><td></td><td></td><td><a href=".gitbook/assets/Git Sync - dark.png">Git Sync - dark.png</a></td><td></td><td></td><td></td></tr><tr><td><h4>AI Insights</h4></td><td><a href="docs-site/ai-insights.md">AI insights</a></td><td><a href="ai-and-search/gitbook-ai-assistant.md">GitBook Assistant</a></td><td><a href="gitbook-agent/identifying-content-gaps.md">Identify content gaps</a></td><td><a href="docs-site/insights.md">Site analytics</a></td><td><a href=".gitbook/assets/AI insights.png">AI insights.png</a></td><td></td><td></td><td></td><td><a href=".gitbook/assets/AI insights - dark.png">AI insights - dark.png</a></td><td></td><td></td></tr><tr><td><h4>MCP Server</h4></td><td><a href="getting-started/ai-documentation/gitbook-mcp.md">GitBook MCP</a></td><td><a href="publishing-documentation/mcp-servers-for-published-docs.md">MCP servers for published docs</a></td><td><a href="getting-started/ai-documentation/ai-coding-assistants-and-skillmd.md">AI coding assistants and skill.md</a></td><td><a href="getting-started/ai-documentation/optimizing-for-ai.md">Optimizing for AI</a></td><td><a href=".gitbook/assets/MCP server.png">MCP server.png</a></td><td></td><td></td><td></td><td></td><td><a href=".gitbook/assets/MCP server - dark.png">MCP server - dark.png</a></td><td></td></tr><tr><td><h4>API</h4></td><td><a href="https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api">GitBook API</a></td><td><a href="https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api/quickstart">Quickstart</a></td><td><a href="https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api/api-reference">API reference</a></td><td></td><td><a href=".gitbook/assets/API.png">API.png</a></td><td></td><td></td><td></td><td></td><td></td><td><a href=".gitbook/assets/API - dark.png">API - dark.png</a></td></tr></tbody></table>

#### Looking for something else?

<button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">Ask a question…</button>
