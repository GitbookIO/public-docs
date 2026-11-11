---
description: >-
  Add GitBook skills to AI coding assistants like Claude Code, Cursor, or Codex
  so they can work with GitBook pages, sites, and workflows
---

# Agent skills

Setting up GitBook for the first time? Point your agent to [Set up GitBook](../setup.md) instead.

GitBook publishes a set of skills in the [gitbook-skills](https://github.com/GitbookIO/gitbook-skills) repository. They teach AI coding assistants how to work with GitBook documentation: writing pages, configuring sites, OpenAPI references, change requests, and integrations. If you use Claude Code, Cursor, Codex, or another coding assistant, add the skills so your agent can use GitBook syntax, blocks, and configuration files correctly.

This fits well with [Git Sync](git-sync/) workflows — make changes in your repo, commit them, and your docs site updates automatically.

{% hint style="info" %}
Prefer writing in the GitBook editor? Use [GitBook Agent](../gitbook-agent/overview.md) to draft, rewrite, review, and translate content without leaving GitBook.
{% endhint %}

## Add GitBook skills to your AI agent

Use this option when your AI coding assistant supports package-based skills.

{% stepper %}
{% step %}
### Connect GitBook MCP

Skills that only edit files, such as `write-docs`, don’t need GitBook authentication. Skills that talk to GitBook — including `configure-site`, `write-openapi`, `cr-create`, and `cr-review` — should use the [GitBook MCP](gitbook-mcp.md) connection, which signs in with OAuth in the browser.

A personal access token from your [developer settings](https://app.gitbook.com/account/developer) is only needed if you’re calling the REST API directly. `cr-create` and `cr-review` use the REST API, so they need a token. `configure-site` and `write-openapi` prefer MCP first, and fall back to a token when MCP isn’t connected.
{% endstep %}

{% step %}
### Install GitBook skills

The skills live in the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository. Run the following command to install them in your project:

{% code expandable="true" %}
```bash
npx -y skills add GitbookIO/gitbook-skills -y
```
{% endcode %}

Without both `-y` flags, the installer waits for input.
{% endstep %}
{% endstepper %}

## Add GitBook skills locally

Download GitBook’s skills if your assistant doesn’t support package-based skills.

{% stepper %}
{% step %}
### Download GitBook skills

Install GitBook skills with `npx -y skills add GitbookIO/gitbook-skills -y` when your assistant supports it.

To copy the files to your project manually, get them from the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository.

<table><thead><tr><th width="156.67578125" valign="top">Skill</th><th width="455.33203125" valign="top">Description</th><th valign="top">Download</th></tr></thead><tbody><tr><td valign="top"><code>write-docs</code></td><td valign="top">Author and edit GitBook-flavored Markdown pages.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/write-docs">GitHub</a><br></td></tr><tr><td valign="top"><code>configure-site</code></td><td valign="top">Create and configure GitBook sites end-to-end via the REST API.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/configure-site">GitHub</a><br></td></tr><tr><td valign="top"><code>write-openapi</code></td><td valign="top">Author and publish OpenAPI reference docs in GitBook.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/write-openapi">GitHub</a></td></tr><tr><td valign="top"><code>cr-create</code></td><td valign="top">Drive a GitBook docs review flow via the REST API — create a change request, push content, request review, and fix comments.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/cr-create">GitHub</a></td></tr><tr><td valign="top"><code>cr-review</code></td><td valign="top">Review GitBook change requests via the REST API — discover CRs, summarize changes, comment, approve, or request changes.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/cr-review">GitHub</a></td></tr><tr><td valign="top"><code>build-integration</code></td><td valign="top">Build, develop, and publish GitBook integrations — custom blocks, ContentKit UI, events, and OAuth.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/build-integration">GitHub</a></td></tr></tbody></table>

{% hint style="warning" %}
Remember to update your local skills as GitBook adds new features.
{% endhint %}
{% endstep %}
{% endstepper %}

## Using GitBook skills

{% prompt description="Scaffold a Git-synced docs site from a folder of markdown" %}
```markdown
Using the GitBook skills, turn this folder of markdown into a GitBook docs site backed by Git Sync.

1. Read my docs folder and propose a site structure — spaces, page tree, and SUMMARY.md navigation. Show me before writing anything.
2. Scaffold the repo in GitBook's monorepo layout (README.md + SUMMARY.md per space) and commit it.
3. Create the site and spaces, then give me exact, copy-paste instructions for the one step I do in the GitBook UI: wiring each space to its directory with Git Sync.
4. Once I confirm sync is set up, verify the site structure matches the plan.
```
{% endprompt %}

{% prompt description="Upgrade a plain markdown page into a polished GitBook page" %}
```markdown
Using the GitBook skills, rewrite this page with GitBook's rich blocks — it's currently plain markdown.

1. Read the page and tell me what you'd upgrade: multi-language code samples → tabs, ordered walkthroughs → steppers, callouts → hints, "choose your path" content → cards.
2. Apply the changes using correct GitBook syntax, including frontmatter (title, description, icon).
3. Keep the words mine — improve the structure, not the voice.
4. List anything I should double-check after it renders in GitBook.
```
{% endprompt %}

{% prompt description="Generate an API reference from an OpenAPI spec" %}
```markdown
Using the GitBook skills, set up an API reference section in my docs from my OpenAPI spec.

1. Find my spec (or help me generate one from the codebase if none exists) and validate it.
2. Set up auto-generated endpoint pages with GitBook's OpenAPI block in SUMMARY.md — don't hand-write endpoint pages; the spec stays the source of truth.
3. Add a short overview page per resource group.
4. Flag gaps in the spec (missing descriptions, examples, response schemas) that would make the rendered reference weak.
```
{% endprompt %}

## FAQ

<details>

<summary>What do the GitBook skills contain?</summary>

The skills in the [gitbook-skills](https://github.com/GitbookIO/gitbook-skills) repository give your AI coding assistant the context it needs to create, edit, and format GitBook content correctly.

`write-docs` includes:

* A complete syntax reference for custom blocks.
* Configuration file formats, including `.gitbook.yaml`, `SUMMARY.md`, and `.gitbook/vars.yaml`.
* Frontmatter options, layout controls, variables, expressions, decision tables, and common pitfalls.

The other skills cover site setup, OpenAPI references, change requests, and integrations.

</details>

<details>

<summary>How do I test AI-generated content?</summary>

Always review and test content generated by AI assistants. When working with an assistant trained on the GitBook skills:

* Verify that custom blocks render correctly in GitBook.
* Check that all internal links work.
* Confirm that the frontmatter is valid YAML.
* Test that variables reference the correct scope.

</details>

<details>

<summary>How do I know my assistant is using the GitBook skills?</summary>

Ask it to explain how it would format a GitBook page.

If it references GitBook blocks, frontmatter, variables, or files like `SUMMARY.md`, the skills are loaded.

If it answers with generic Markdown only, check that the skills are installed and reload the assistant.

</details>

<details>

<summary>Why is the assistant ignoring GitBook-specific syntax?</summary>

This usually means the skills aren’t loaded, or the rules aren’t specific enough.

Make sure the GitBook skills are installed, and that your assistant can read them.

If the assistant caches instructions, restart the session after you add or update a skill.

</details>

<details>

<summary>What if the assistant generates invalid GitBook content?</summary>

Check the common failure points first:

* Unclosed custom blocks
* Invalid YAML in frontmatter
* Broken variable references
* Links that don't match your page structure

Always review the output in GitBook before you commit it.

</details>

<details>

<summary>Do I still need an access token?</summary>

Connect [GitBook MCP](gitbook-mcp.md) and sign in with OAuth when a skill needs to talk to GitBook. That covers most of `configure-site` and `write-openapi`.

You need a personal access token when a skill calls the REST API directly, including `cr-create` and `cr-review`, or when MCP isn’t connected. You can create one in your [developer settings](https://app.gitbook.com/account/developer).

If you’re only editing files locally with `write-docs`, you don’t need a token or an MCP connection.

</details>

<details>

<summary>What if the skill seems outdated?</summary>

Update the installed skills, or point your assistant back to the GitHub source.

If your team copied parts of a skill into custom rules, update those too.

</details>
