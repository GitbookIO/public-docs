---
description: What's inside a SKILL.md file and how agents use it.
---

# What SKILL.md contains

`SKILL.md` gives your AI coding assistant the context it needs to create, edit, and format GitBook content correctly. It includes:

* A complete syntax reference for custom blocks.
* Configuration file formats, including `.gitbook.yaml`, `SUMMARY.md`, and `.gitbook/vars.yaml`.
* Frontmatter options, layout controls, variables, expressions, decision tables, and common pitfalls.

An agent reads this file (or has it loaded as a skill) before making changes, the same way it would read a project's own contributing guidelines — the content itself doesn't change what your agent can *do*, only how well it follows GitBook's conventions while doing it.

### Common failure points to watch for

However your assistant applies a skill, review what it produces before you commit it. The most common ways generated content goes wrong:

* Unclosed custom blocks
* Invalid YAML in frontmatter
* Broken variable references
* Links that don't match your page structure

### Confirming your assistant is using it

Ask it to explain how it would format a GitBook page. If it references GitBook blocks, frontmatter, variables, or files like `SUMMARY.md`, the skill is loaded. If it answers with generic Markdown only, the skill likely isn't loaded — see [Install GitBook Skills](install-skills.md) and [Troubleshooting](../reference/troubleshooting.md).

Want to write your own instead of using GitBook's default? See [Author your own skills](author-your-own-skills.md).
