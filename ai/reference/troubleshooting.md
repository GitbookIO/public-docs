---
description: Fixes for agent connection and authentication problems.
---

# Troubleshooting

<details>

<summary>Why does nothing happen after I add the GitBook MCP server to my client?</summary>

That's expected in some MCP clients. Adding a server often only saves the configuration — some clients start authentication only when they first connect, list tools, or open the MCP panel. Try triggering one of those actions before assuming the connection failed.

</details>

<details>

<summary>Why doesn't anything happen after I click Authenticate for GitBook MCP?</summary>

Some clients open the browser sign-in flow after a short delay, which can be longer on a slow or unstable network. If no browser tab opens after about a minute, check your network, pop-up settings, and default browser.

</details>

<details>

<summary>How can I tell if my client authenticated successfully with GitBook MCP?</summary>

The exact signal depends on your client, but the result is usually clear: most clients remove the auth prompt, show the server as connected, or let the assistant list and call MCP tools. If the **Authenticate** button stays visible and no tools appear, the flow likely didn't finish — see [Authenticate your agent](../getting-started/authenticate-your-agent.md) for what a successful flow looks like.

</details>

<details>

<summary>What should I check if GitBook MCP authentication still seems stuck?</summary>

* Confirm the server URL points to the MCP endpoint (`https://mcp.gitbook.com/mcp`).
* Confirm the client uses HTTP transport — GitBook MCP supports streamable HTTP only, not `stdio` or `SSE`.
* Retry on a stable network.
* Remove and re-add the server if the client cached a failed state.

</details>

<details>

<summary>Do I need to add a bearer token when I connect a client to GitBook MCP?</summary>

Only if you authenticate with a [personal access token](https://app.gitbook.com/account/developer). If you use OAuth, don't add a bearer token manually — your client gets it during the sign-in flow.

</details>

<details>

<summary>Why is my assistant ignoring GitBook-specific syntax even though I installed Skills?</summary>

This usually means the skill file isn't loaded, or your project rules aren't specific enough. Make sure your assistant reads `SKILL.md` from the repo root, or uses the GitHub URL in its project instructions. If the assistant caches instructions, restart the session after adding or updating the rule. See [Install GitBook Skills](../gitbook-skills/install-skills.md) to confirm it's loaded correctly.

</details>
