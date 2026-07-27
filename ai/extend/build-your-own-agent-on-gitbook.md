---
description: Combine the GitBook API and Skills to build a custom agent integration.
---

# Build your own agent on GitBook

GitBook MCP and the CLI cover the common case: pointing an existing coding assistant at GitBook. If you're building your own agent, product, or automation on top of GitBook instead — rather than connecting a client like Claude or Cursor — you'll typically combine two pieces already covered in this section:

* **The GitBook API** — the same API that powers MCP and the CLI, and your direct integration point for reading and writing content, managing sites, and running workflows programmatically. See [Drop to the API](drop-to-the-api.md) for when and how to authenticate against it directly.
* **GitBook Skills** — the conventions layer that keeps output consistent with GitBook's syntax and structure. If your agent generates GitBook content, teach it GitBook's conventions the same way any coding assistant would — either GitBook's own skill, or [a custom one](../gitbook-skills/author-your-own-skills.md) reflecting your own product or team's conventions.

In short: use the API as your agent's hands, and a skill as its knowledge of how GitBook content should look — the same division MCP and the CLI already make for you, just built into your own product instead of a general-purpose coding assistant.

### Where to start

1. Get familiar with the API's authentication and core resources by first using it directly — see [Drop to the API](drop-to-the-api.md).
2. Decide whether your agent needs GitBook's own conventions, your team's, or both, and write or install the relevant skill.
3. If your agent will run unattended (not in an interactive coding session), build in the same review discipline covered in [Validate agent content in CI](../automate/validate-agent-content-in-ci.md) — don't skip review just because there's no human typing the prompts.
