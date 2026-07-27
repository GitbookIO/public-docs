---
description: Use GitBook Skills with an API token when you can't install an MCP client.
---

# No MCP? Use skills directly

If your coding assistant doesn't support MCP, or you'd rather not connect one, you can still get agent-quality docs workflows using GitBook Skills plus an access token — no MCP client required.

### Install Skills locally

If your assistant doesn't support package-based skills, download GitBook's skill files directly from the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository and add them to your project instead of installing via a package manager. See [Install GitBook Skills](../gitbook-skills/install-skills.md) for the full walkthrough.

This works well alongside Documentation → Git Sync — your assistant edits Markdown files in your repo, following GitBook's conventions from the skill file, then you commit and push, and your docs site updates automatically. No connection to GitBook itself is required for this part.

### When you do need an access token

Skills alone teach your assistant GitBook's syntax and conventions for editing local files — they don't give it access to GitBook. You only need an access token once your agent needs to interact with GitBook directly: reading live content, opening a change request, or calling the API instead of just editing files that later sync over Git.

Create a personal access token from your [developer settings](https://app.gitbook.com/account/developer), then either:

* Use it with the CLI — see [CLI for agents](../automate/cli-for-agents.md).
* Use it directly against the API — see [Drop to the API](../extend/drop-to-the-api.md).

If you're only editing files locally with Skills and Git Sync, you might not need a token at all until you connect your assistant to one of these.
