---
description: Install GitBook Skills so local AI agents understand your docs conventions.
---

# Install GitBook Skills

{% stepper %}
{% step %}
#### Create an access token

[Create an access token](https://app.gitbook.com/account/developer) from your GitBook developer settings — GitBook uses this to authenticate your agent when it works with GitBook Skills.
{% endstep %}

{% step %}
#### Install the skills

If your assistant supports package-based skills, install directly:

```bash
npx skills add GitBookIO/gitbook-skills
```

If it doesn't, copy the files manually from the [`gitbook-skills`](https://github.com/GitbookIO/gitbook-skills) repository into your project instead. See [GitBook Skills overview](overview.md) for the full list of available skills and what each does.

{% hint style="warning" %}
Keep your local copy of `SKILL.md` up to date as GitBook adds new features — re-run the install command, or re-download the files, periodically. If your team copied parts of the file into custom rules, update those too.
{% endhint %}
{% endstep %}
{% endstepper %}

### Using GitBook Skills

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

### Confirming it's working

Ask your agent to explain how it would format a GitBook page. If it references GitBook blocks, frontmatter, variables, or files like `SUMMARY.md`, the skill is loaded. If it answers with generic Markdown only, check your project rules and reload the assistant — see [Troubleshooting](../reference/troubleshooting.md) if it still doesn't pick it up.
