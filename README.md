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
```markdown
# GitBook Setup Agent

## Goal
Get my docs live on a published GitBook site. Done = you hand me the live URL and confirm it loads. Tell me clearly when a step needs me — do everything else yourself.

**If this prompt was pasted before** and the gitbook MCP tools are already connected, don't start over — skip Connect and continue from where we left off, re-confirming the plan with me briefly.

## Account
I most likely have a GitBook account. If sign-in fails during Connect, send me to https://app.gitbook.com/join first, then retry.

## Prepare (start immediately)
Ask for my docs — a local folder or a repo. Verify the source before building: echo back exactly what you're reading and list its top-level contents so I can confirm it's right. If you can't access something I named (private repos return 404, same as nonexistent), stop and ask — never substitute a different source. Show me the site plan before creating anything in GitBook.

## Connect
If the gitbook MCP tools are already available in this session, skip straight to the next section. Otherwise:

Connect to GitBook's MCP server: `https://mcp.gitbook.com/mcp` (streamable HTTP, OAuth).

- **Claude Code**: `claude plugin marketplace add GitbookIO/gitbook-skills` then `claude plugin install gitbook@gitbook-skills` — I run `/reload-plugins` and `/mcp` to sign in.
- **Codex**: `codex mcp add gitbook --url https://mcp.gitbook.com/mcp`
- **Cursor**: add the URL under `mcpServers` in `.cursor/mcp.json`, then I enable it in Settings → MCP.
- **Chat app with no terminal**: tell me to add the URL as a custom connector in my app's settings.
- **Anything else**: fetch https://gitbook.com/docs/getting-started/ai-documentation/gitbook-mcp.md for setup instructions, or fall back to the REST API with a PAT from https://app.gitbook.com/account/developer.

Most tools don't load new MCP servers mid-session. If the gitbook tools don't appear after setup, tell me to restart the app and paste this prompt again — you'll detect the connection and continue. If you can run commands, also install GitBook's skills: `npx -y skills add GitbookIO/gitbook-skills -y`

## Check before creating
Once connected, check whether these docs already have a GitBook site — look at the repo's Git Sync state and list my org's sites. If a site exists, don't create a duplicate: switch to updating it (edit locally and push if Git Sync is wired, or open a change request). Create a new site only if nothing exists.

## Build and publish
Create the site with the GitBook MCP tools, import my content, and publish. Skip Git Sync for this first publish — offer it once the site is live. Fetch the live URL to confirm it loads, then give it to me.

```
{% endcode %}

<p align="center"><a href="claude://code/new?q=%23%20GitBook%20Setup%20Agent%0AGet%20my%20docs%20live%20on%20a%20published%20GitBook%20site.%20Done%20%3D%20you%20give%20me%20the%20live%20URL%20and%20confirm%20it%20loads.%20Tell%20me%20when%20a%20step%20needs%20me%3B%20do%20the%20rest%20yourself.%0AAsk%20for%20my%20docs%20%28folder%20or%20repo%29.%20Echo%20what%20you%20read%20and%20list%20its%20top%20contents%20so%20I%20can%20confirm.%20If%20a%20source%20is%20unreachable%20%28private%20repos%20return%20404%29%2C%20stop%20and%20ask%20-%20never%20substitute%20another.%20Show%20me%20the%20site%20plan%20before%20creating%20anything.%0AConnect%20%28skip%20if%20gitbook%20MCP%20tools%20already%20available%29%3A%0Aclaude%20plugin%20marketplace%20add%20GitbookIO%2Fgitbook-skills%0Aclaude%20plugin%20install%20gitbook%40gitbook-skills%0AThen%20I%20run%20%2Freload-plugins%20and%20%2Fmcp%20to%20sign%20in.%20If%20tools%20don%27t%20appear%2C%20I%20restart%20and%20paste%20this%20prompt%20again%3B%20detect%20the%20connection%20and%20continue.%0ACheck%20my%20org%20for%20an%20existing%20site%20for%20these%20docs%20first%3B%20if%20found%2C%20update%20it%2C%20don%27t%20duplicate.%0ACreate%20the%20site%20via%20MCP%2C%20import%20content%2C%20publish%20%28no%20Git%20Sync%20yet%3B%20offer%20it%20after%20live%29.%20Verify%20the%20URL%20loads%2C%20then%20share%20it." class="button secondary" data-icon="claude">Claude Code</a><a href="cursor://anysphere.cursor-deeplink/prompt?text=%23%20GitBook%20Setup%20Agent%0AGet%20my%20docs%20live%20on%20a%20published%20GitBook%20site.%20Done%20%3D%20you%20give%20me%20the%20live%20URL%20and%20confirm%20it%20loads.%20Tell%20me%20when%20a%20step%20needs%20me%3B%20do%20the%20rest%20yourself.%0AAsk%20for%20my%20docs%20%28folder%20or%20repo%29.%20Echo%20what%20you%20read%20and%20list%20its%20top%20contents%20so%20I%20can%20confirm.%20If%20a%20source%20is%20unreachable%20%28private%20repos%20return%20404%29%2C%20stop%20and%20ask%20-%20never%20substitute%20another.%20Show%20me%20the%20site%20plan%20before%20creating%20anything.%0AConnect%20%28skip%20if%20gitbook%20MCP%20tools%20already%20available%29%3A%0AAdd%20server%20gitbook%20with%20url%20https%3A%2F%2Fmcp.gitbook.com%2Fmcp%20to%20.cursor%2Fmcp.json%20under%20mcpServers.%20Install%20skills%3A%20npx%20-y%20skills%20add%20GitbookIO%2Fgitbook-skills%20-y%0ACursor%20won%27t%20load%20new%20MCP%20servers%20mid-session%3A%20I%20enable%20it%20in%20Settings%20%3E%20MCP%2C%20sign%20in%2C%20reload%20Cursor%2C%20and%20paste%20this%20prompt%20again%3B%20detect%20the%20connection%20and%20continue.%0ACheck%20my%20org%20for%20an%20existing%20site%20for%20these%20docs%20first%3B%20if%20found%2C%20update%20it%2C%20don%27t%20duplicate.%0ACreate%20the%20site%20via%20MCP%2C%20import%20content%2C%20publish%20%28no%20Git%20Sync%20yet%3B%20offer%20it%20after%20live%29.%20Verify%20the%20URL%20loads%2C%20then%20share%20it." class="button secondary" data-icon="cursor">Cursor</a><a href="codex://threads/new?prompt=%23%20GitBook%20Setup%20Agent%0AGet%20my%20docs%20live%20on%20a%20published%20GitBook%20site.%20Done%20%3D%20you%20give%20me%20the%20live%20URL%20and%20confirm%20it%20loads.%20Tell%20me%20when%20a%20step%20needs%20me%3B%20do%20the%20rest%20yourself.%0AAsk%20for%20my%20docs%20%28folder%20or%20repo%29.%20Echo%20what%20you%20read%20and%20list%20its%20top%20contents%20so%20I%20can%20confirm.%20If%20a%20source%20is%20unreachable%20%28private%20repos%20return%20404%29%2C%20stop%20and%20ask%20-%20never%20substitute%20another.%20Show%20me%20the%20site%20plan%20before%20creating%20anything.%0AConnect%20%28skip%20if%20gitbook%20MCP%20tools%20already%20available%29%3A%0Acodex%20mcp%20add%20gitbook%20--url%20https%3A%2F%2Fmcp.gitbook.com%2Fmcp%0Anpx%20-y%20skills%20add%20GitbookIO%2Fgitbook-skills%20-y%0ANew%20servers%20don%27t%20load%20mid-session%3A%20after%20these%20run%2C%20I%20restart%20Codex%2C%20approve%20sign-in%20in%20my%20browser%2C%20and%20paste%20this%20prompt%20again%3B%20detect%20the%20connection%20and%20continue.%0ACheck%20my%20org%20for%20an%20existing%20site%20for%20these%20docs%20first%3B%20if%20found%2C%20update%20it%2C%20don%27t%20duplicate.%0ACreate%20the%20site%20via%20MCP%2C%20import%20content%2C%20publish%20%28no%20Git%20Sync%20yet%3B%20offer%20it%20after%20live%29.%20Verify%20the%20URL%20loads%2C%20then%20share%20it." class="button secondary" data-icon="openai">Codex</a></p>
{% endcolumn %}
{% endcolumns %}

#### Quickstart guides

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-robot">:robot:</i></h4></td><td><strong>AI quickstart</strong></td><td><a href="getting-started/ai-documentation/">ai-documentation</a></td></tr><tr><td><h4><i class="fa-hand-pointer">:hand-pointer:</i></h4></td><td><strong>Editor quickstart</strong></td><td><a href="getting-started/quickstart.md">quickstart.md</a></td></tr></tbody></table>

#### Explore GitBook's features

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-card-cover-dark data-type="image">Cover image (dark)</th></tr></thead><tbody><tr><td><h4>GitBook Agent</h4></td><td><a href="gitbook-agent/write-and-edit-with-ai.md">Writing with GitBook Agent</a></td><td><a href="gitbook-agent/review-change-requests-with-gitbook-agent.md">Review change requests</a></td><td><a href="gitbook-agent/automatic-docs-improvements.md">Identify content gaps</a></td><td><a href="publishing-documentation/channels.md">Channels</a></td><td><a href=".gitbook/assets/GitBook Agent.png">GitBook Agent.png</a></td><td><a href=".gitbook/assets/GitBook Agent - dark.png">GitBook Agent - dark.png</a></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td><h4>GitBook Assistant</h4></td><td><a href="ai-and-search/connections/">Connections</a></td><td><a href="docs-site/embedding/">Docs Embed</a></td><td><a href="docs-site/embedding/configuration/creating-custom-tools.md">Connect to custom tools</a></td><td></td><td><a href=".gitbook/assets/GitBook Assistant.png">GitBook Assistant.png</a></td><td></td><td><a href=".gitbook/assets/GitBook Assistant - dark.png">GitBook Assistant - dark.png</a></td><td></td><td></td><td></td><td></td></tr><tr><td><h4>Git Sync</h4></td><td><a href="getting-started/git-sync/enabling-github-sync.md">Enabling GitHub Sync</a></td><td><a href="getting-started/git-sync/content-configuration.md">Content configuration</a></td><td><a href="getting-started/git-sync/github-pull-request-preview.md">GitHub pull request preview</a></td><td><a href="getting-started/git-sync/monorepos.md">Monorepos</a></td><td><a href=".gitbook/assets/Git Sync.png">Git Sync.png</a></td><td></td><td></td><td><a href=".gitbook/assets/Git Sync - dark.png">Git Sync - dark.png</a></td><td></td><td></td><td></td></tr><tr><td><h4>AI Insights</h4></td><td><a href="docs-site/ai-insights.md">AI insights</a></td><td><a href="ai-and-search/gitbook-ai-assistant.md">GitBook Assistant</a></td><td><a href="gitbook-agent/automatic-docs-improvements.md">Identify content gaps</a></td><td><a href="docs-site/insights.md">Site analytics</a></td><td><a href=".gitbook/assets/AI insights.png">AI insights.png</a></td><td></td><td></td><td></td><td><a href=".gitbook/assets/AI insights - dark.png">AI insights - dark.png</a></td><td></td><td></td></tr><tr><td><h4>MCP Server</h4></td><td><a href="getting-started/ai-documentation/gitbook-mcp.md">GitBook MCP</a></td><td><a href="publishing-documentation/mcp-servers-for-published-docs.md">MCP servers for published docs</a></td><td><a href="getting-started/ai-documentation/ai-coding-assistants-and-skillmd.md">AI coding assistants and skill.md</a></td><td><a href="getting-started/ai-documentation/optimizing-for-ai.md">Optimizing for AI</a></td><td><a href=".gitbook/assets/MCP server.png">MCP server.png</a></td><td></td><td></td><td></td><td></td><td><a href=".gitbook/assets/MCP server - dark.png">MCP server - dark.png</a></td><td></td></tr><tr><td><h4>API</h4></td><td><a href="https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api">GitBook API</a></td><td><a href="https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api/quickstart">Quickstart</a></td><td><a href="https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api/api-reference">API reference</a></td><td></td><td><a href=".gitbook/assets/API.png">API.png</a></td><td></td><td></td><td></td><td></td><td></td><td><a href=".gitbook/assets/API - dark.png">API - dark.png</a></td></tr></tbody></table>

#### Looking for something else?

<button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">Ask a question…</button>
