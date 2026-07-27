---
description: Install and author GitBook Skills for AI coding agents.
---

# Work with GitBook Skills

GitBook provides [skill files](https://github.com/GitbookIO/gitbook-skills/tree/main) that teach AI coding assistants how to edit GitBook documentation correctly. If you use Claude Code, Cursor, Codex, or another external coding assistant, add GitBook Skills so your agent works with GitBook syntax, blocks, and configuration files.

{% hint style="info" %}
Skills are a quality and consistency layer on top of whatever surface your agent already uses — MCP, the CLI, or the API — not an alternative to any of them. Skills teach your agent GitBook's conventions; MCP, the CLI, and the API are how it actually acts on your content.
{% endhint %}

This fits well with Git Sync workflows — make changes in your repo, commit them, and your docs site updates automatically.

{% hint style="info" %}
Prefer writing in the GitBook editor instead? Use GitBook Agent (Documentation → GitBook AI → GitBook Agent) to draft, rewrite, review, and translate content without leaving GitBook.
{% endhint %}

### Add GitBook Skills to your AI agent

Use this when your AI coding assistant supports package-based skills:

{% stepper %}
{% step %}
#### Create an access token

[Create an access token](https://app.gitbook.com/account/developer) from your GitBook developer settings, so GitBook can authenticate your agent when it works with GitBook Skills.
{% endstep %}

{% step %}
#### Install GitBook Skills

This skill is part of the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository:

```bash
npx skills add GitBookIO/gitbook-skills
```
{% endstep %}
{% endstepper %}

If your assistant doesn't support package-based skills, see [Install GitBook Skills](install-skills.md) for downloading them locally instead.

### Available skills

| Skill | Description |
|---|---|
| `configure-site` | Create and maintain entire GitBook documentation sites. |
| `write-docs` | Write, author, edit, and format GitBook documentation pages. |
| `write-openapi` | Author, configure, structure, and troubleshoot OpenAPI/Swagger API reference docs. |
| `build-integration` | Build custom integrations for GitBook. |
| `cr-create` | Create GitBook change requests, push content, request reviews, and address comments. |
| `cr-review` | Review GitBook change requests, summarize changes, comment, approve, or request changes. |

Get any of these from the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository on GitHub.

{% hint style="warning" %}
Keep your local copy of `SKILL.md` up to date as GitBook adds new features.
{% endhint %}

* [Install GitBook Skills](install-skills.md) — the full installation walkthrough, including manual setup.
* [What SKILL.md contains](whats-inside-a-skill.md) — what your agent actually gets from it.
* [Author your own skills](author-your-own-skills.md) — write a skill tailored to your own team's conventions.
