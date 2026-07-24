---
description: >-
  Connect AI coding assistants to GitBook so they can create sites, open change
  requests, and edit content through GitBook’s API
---

# GitBook MCP

GitBook exposes an MCP server that lets AI tools act on content in your organization.

Tools like Claude Code, Codex, Cursor, and other MCP clients can use it to create and configure sites, open change requests, draft content, edit pages, and restructure docs.

To connect your AI coding assistant to GitBook’s MCP, you need the server URL, an authentication method, and a supported MCP client. The sections below walk you through each.

{% hint style="info" %}
Need a read-only MCP server for a published docs site? GitBook creates one for you automatically — see [MCP servers for published docs](../../publishing-documentation/mcp-servers-for-published-docs.md) to find out more.
{% endhint %}

## GitBook’s MCP Endpoint

Point your MCP client at:

```http
https://mcp.gitbook.com/mcp
```

{% hint style="info" %}
Opening this URL in a browser returns an error. Use it in an MCP client that can make HTTP requests.
{% endhint %}

## Connect your client

Add GitBook MCP in your client of choice:

{% tabs %}
{% tab title="Claude Code" icon="claude" %}
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

{% tab title="Codex" icon="openai" %}
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

{% tab title="Cursor" icon="cursor" %}
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

{% tab title="VS Code" icon="vscode" %}
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
Any MCP-compatible client can connect over streamable HTTP.

Point it at:

```
https://mcp.gitbook.com/mcp
```

GitBook supports streamable HTTP only. `stdio` and `SSE` aren't supported.

If you use OAuth, you usually don't need any extra auth fields.

If you use a personal access token instead, send it as a bearer token:

```http
Authorization: Bearer <YOUR_PAT>
```
{% endtab %}
{% endtabs %}

## Authenticate GitBook’s MCP

GitBook MCP supports two authentication methods: OAuth and personal access tokens.

{% tabs %}
{% tab title="OAuth" %}
Point your client at the MCP server URL. The client discovers the authorization server, registers itself, and opens the browser sign-in flow automatically.

If you use OAuth, don't add a bearer token manually. The client gets one during sign-in.
{% endtab %}

{% tab title="Personal access token" %}
To skip the browser flow, send your token as a bearer token:

```http
Authorization: Bearer <YOUR_PAT>
```

You can create a personal access token in your [developer settings](https://app.gitbook.com/account/developer).

Use this for scripted setups, or when your client already manages secrets locally.
{% endtab %}
{% endtabs %}

## Using GitBook’s MCP

{% prompt description="Create and configure a new docs site." %}
```markdown
Using the GitBook MCP tools, create a new docs site for me.

1. List my organizations and confirm which one to use before creating anything.
2. Ask what the site is for and what content I have (folder, repo, or just a description). If I point you at a source, echo back what you find there so I can confirm it's right.
3. Show me a short plan — site name, spaces, page structure — and wait for my yes.
4. Create the site, add the content, and publish. Then fetch the live URL to confirm it works and share it with me.
```
{% endprompt %}

{% prompt description="Open a change request and draft content." %}
```markdown
Using the GitBook MCP tools, draft new content for my docs in a change request — don't edit anything live.

1. List my organizations and sites, and confirm which space to work in.
2. Ask me what the content should cover, then open a change request and draft the pages inside it.
3. Match the tone and structure of my existing pages — read a few first.
4. When done, share the change request preview link so I can review and merge it in GitBook.
```
{% endprompt %}

{% prompt description="Move, rename, or restructure pages across a site." %}
```markdown
Using the GitBook MCP tools, help me restructure my docs site.

1. List my organizations and sites, confirm which one, then fetch its current structure and show it to me.
2. Ask what I want changed, then propose the new structure as a simple before/after tree — don't move anything until I approve.
3. Apply the changes, keeping URLs and internal links intact where possible; flag anything that will break.
4. Show me the final structure and the change request or live result to verify.
```
{% endprompt %}

## The difference between the GitBook MCP and published docs MCP

GitBook has two MCP patterns:

* [**MCP servers for published docs**](../../publishing-documentation/mcp-servers-for-published-docs.md) give AI tools read-only access to published content.
* **GitBook MCP** gives AI tools access to your content and workflows through the GitBook API.

Use published docs MCP when you want documentation readers and end-users to find information from your published docs.&#x20;

Use GitBook MCP when you want your team’s agents to edit and manage your documentation through automated workflows.

## FAQ

<details>

<summary>Which transport does GitBook MCP support when I connect an MCP client?</summary>

GitBook MCP supports streamable HTTP.

GitBook MCP doesn't support `stdio` or `SSE`.

If your client asks for extra fields, you can usually leave them empty.

</details>

<details>

<summary>Do I need to add a bearer token when I connect a client to GitBook MCP?</summary>

You only need to add a bearer token if you authenticate with a [personal access token](https://app.gitbook.com/account/developer).

If you use OAuth, don't add a bearer token manually. Your client gets it during the sign-in flow.

</details>

<details>

<summary>Why does nothing happen after I add the GitBook MCP server to my client?</summary>

Yes. That's expected in some MCP clients.

Adding a server often only saves the configuration. Some clients start authentication only when they first connect, list tools, or open the MCP panel.

</details>

<details>

<summary>Why doesn't anything happen after I click Authenticate for GitBook MCP?</summary>

Some clients open the browser sign-in flow after a short delay.

That delay can be longer on a slow or unstable network.

If no browser tab opens after about a minute, check your network, pop-up settings, and default browser.

</details>

<details>

<summary>What happens during the GitBook MCP authentication flow?</summary>

When authentication works, the flow usually looks like this:

1. The client connects to the MCP server.
2. Your browser opens the sign-in flow.
3. You sign in and approve access.
4. The client shows the server as connected, or the MCP tools become available.

</details>

<details>

<summary>How can I tell if my client authenticated successfully with GitBook MCP?</summary>

The exact signal depends on your client, but the result is usually clear.

Most clients remove the auth prompt, show the server as connected, or let the assistant list and call MCP tools.

If the **Authenticate** button stays visible and no tools appear, the flow likely didn't finish.

</details>

<details>

<summary>What should I check if GitBook MCP authentication still seems stuck?</summary>

Try these checks:

* Confirm the server URL points to the MCP endpoint.
* Confirm the client uses HTTP transport.
* Retry on a stable network.
* Remove and re-add the server if the client cached a failed state.

</details>
