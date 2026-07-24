---
description: >-
  Use GitBook’s official SKILL.md file to give AI coding assistants like Claude
  Code, Cursor or Codex knowledge of GitBook’s features and blocks
---

# Agent skills

GitBook provides [skill files](https://github.com/GitbookIO/gitbook-skills/tree/main) that teach AI coding assistants how to edit GitBook documentation correctly. If you use Claude Code, Cursor, Codex, or another external coding assistant, add GitBook skills so your agent can work with GitBook syntax, blocks, and configuration files.

This fits well with [Git Sync](../git-sync/) workflows — make changes in your repo, commit them, and your docs site updates automatically.

{% hint style="info" %}
Prefer writing in the GitBook editor? Use [GitBook Agent](../../gitbook-agent/what-is-gitbook-agent.md) to draft, rewrite, review, and translate content without leaving GitBook.
{% endhint %}

## Add GitBook skills to your AI agent

Use this option when your AI coding assistant supports package-based skills.

{% stepper %}
{% step %}
### Create an access token

To let your agent interact with GitBook, you need to [create an access token](https://app.gitbook.com/account/developer) from your GitBook developer settings. GitBook uses this token to authenticate your agent when working with GitBook skills.
{% endstep %}

{% step %}
### Install GitBook skills

This skill is part of the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository. Run the following command to install GitBook skills directly to your project:

{% code expandable="true" %}
```bash
npx skills add GitBookIO/gitbook-skills
```
{% endcode %}
{% endstep %}
{% endstepper %}

## Add GitBook skills locally

Download GitBook’s skills if your assistant doesn’t support package-based skills.

{% stepper %}
{% step %}
### Create an access token

To let your agent interact with GitBook, you need to [create an access token](https://app.gitbook.com/account/developer) from your GitBook developer settings. GitBook uses this token to authenticate your agent when working with GitBook skills.
{% endstep %}

{% step %}
### Download GitBook skills

Install GitBook skills with `npx skills add GitBookIO/gitbook-skills` when your assistant supports it.

To copy the files to your project manually, get GitBook skills from the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository.

<table><thead><tr><th width="156.67578125" valign="top">Skill</th><th width="455.33203125" valign="top">Description</th><th valign="top">Download</th></tr></thead><tbody><tr><td valign="top"><code>configure-site</code></td><td valign="top">Create and maintain entire GitBook documentation sites.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/configure-site">GitHub</a><br></td></tr><tr><td valign="top"><code>write-docs</code></td><td valign="top">Write, author, edit, and format GitBook documentation pages.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/write-docs">GitHub</a><br></td></tr><tr><td valign="top"><code>write-openapi</code></td><td valign="top">Author, configure, structure, and troubleshoot OpenAPI/Swagger API reference docs.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/write-openapi">GitHub</a></td></tr><tr><td valign="top"><code>build-integration</code></td><td valign="top">Build custom integrations for GitBook.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/build-integration">GitHub</a></td></tr><tr><td valign="top"><code>cr-create</code></td><td valign="top">Create GitBook change requests, push content, request reviews, and address comments.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/cr-create">GitHub</a></td></tr><tr><td valign="top"><code>cr-review</code></td><td valign="top">Review GitBook change requests, summarize changes, comment, approve, or request changes.</td><td valign="top"><a href="https://github.com/GitbookIO/gitbook-skills/tree/main/skills/cr-review">GitHub</a></td></tr></tbody></table>

{% hint style="warning" %}
Remember to update your local repository with the latest `SKILL.md` file as GitBook adds new features.
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

<summary>What does SKILL.md contain?</summary>

`SKILL.md` gives your AI coding assistant the context it needs to create, edit, and format GitBook content correctly.

It includes:

* A complete syntax reference for custom blocks.
* Configuration file formats, including `.gitbook.yaml`, `SUMMARY.md`, and `.gitbook/vars.yaml`.
* Frontmatter options, layout controls, variables, expressions, decision tables, and common pitfalls.

</details>

<details>

<summary>How do I test AI-generated content?</summary>

Always review and test content generated by AI assistants. When working with an assistant trained on the skill file:

* Verify that custom blocks render correctly in GitBook.
* Check that all internal links work.
* Confirm that the frontmatter is valid YAML.
* Test that variables reference the correct scope.

</details>

<details>

<summary>How do I know my assistant is using SKILL.md?</summary>

Ask it to explain how it would format a GitBook page.

If it references GitBook blocks, frontmatter, variables, or files like `SUMMARY.md`, the skill is loaded.

If it answers with generic Markdown only, check your project rules and reload the assistant.

</details>

<details>

<summary>Why is the assistant ignoring GitBook-specific syntax?</summary>

This usually means the skill file isn’t loaded, or the rules aren’t specific enough.

Make sure your assistant reads `SKILL.md` from the repo root, or uses the GitHub URL in its project instructions.

If the assistant caches instructions, restart the session after you add or update the rule.

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

You need an access token when your agent interacts with GitBook directly. You can create a personal access token in your [developer settings](https://app.gitbook.com/account/developer).

If you’re only editing files locally with `SKILL.md`, you might not need one until you connect the assistant to GitBook workflows or APIs.

</details>

<details>

<summary>What if the skill seems outdated?</summary>

Update your local `SKILL.md`, or point your assistant back to the GitHub source.

If your team copied parts of the file into custom rules, update those too.

</details>
