---
description: Frequently asked questions about driving GitBook from agents.
---

# FAQ

<details>

<summary>What's the difference between GitBook MCP, the CLI, and Skills?</summary>

They're not alternatives to each other — they're different layers:

* **GitBook MCP** and the **CLI** are both ways for an agent to actually *act* on your GitBook content (read it, edit it, open change requests), just suited to different styles of work — conversational agent sessions for MCP, scriptable/deterministic steps for the CLI. See [Which MCP server do I need?](which-mcp-server-do-i-need.md) and [CLI for agents](../automate/cli-for-agents.md).
* **Skills** don't act on anything by themselves — they teach whichever surface your agent uses (MCP, the CLI, or direct file edits via Git Sync) GitBook's conventions, so its output is correct. See [GitBook Skills overview](../gitbook-skills/overview.md).

</details>

<details>

<summary>Do I still need an access token if I'm just using Skills?</summary>

Not necessarily. Skills alone teach your assistant GitBook's syntax for editing local files — they don't require GitBook access on their own. You only need a token once your agent needs to interact with GitBook directly (reading live content, opening a change request, or calling the API). See [No MCP? Use skills directly](../getting-started/no-mcp-use-skills-directly.md).

</details>

<details>

<summary>Can I use GitBook Agent and an MCP-connected coding assistant together?</summary>

Yes — they're separate products working on the same content. GitBook Agent works inside the GitBook app itself (in the editor, in change requests, in comments). An MCP-connected assistant like Claude Code or Cursor works from your own terminal or IDE, against the same organization, through the GitBook MCP server. Nothing about using one prevents using the other.

</details>
