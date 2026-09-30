<!-- gitbook-agent-instructions:start -->

## GitBook Documentation Editing

This repository contains documentation synced with GitBook via Git Sync.

Before editing GitBook-synced Markdown, YAML, or asset files, make sure the GitBook skill is available and up to date in your local agent environment. Prefer installing or updating it with:

```bash
npx skills add gitbookio/gitbook-skills
```

This command may add or update local agent skill files. Use them only as local agent instructions; do not commit those installed skill files or any tool-generated agent configuration unless the user explicitly asks for it.

If `npx` is unavailable, load the skill from:

https://gitbook.com/docs/skill.md

When making changes, preserve GitBook sync metadata such as frontmatter, `SUMMARY.md`, `gitbook-docs.yaml`, `.gitbook/`, and asset links unless the requested edit explicitly requires changing them.

<!-- gitbook-agent-instructions:end -->

## Where pages go

- File a page under the group that matches the job the reader is doing. Don't file it by the technology behind the feature, or by where the feature sits in the app's sidebar. The sidebar changes often; the jobs don't.
- Each group heading in `documentation/SUMMARY.md` carries an explicit id, for example `## Work from your tools <a href="#docs-as-code" id="docs-as-code"></a>`. The id is the group's URL segment. Change a group's label freely. Never change its id.
- A page's URL follows the navigation: group id, then parent page slugs, then its own slug. Moving a page to another group or under another parent changes its URL. Don't move pages without a redirect plan agreed with the docs team.
- Describe the app's sidebar in one place only: `documentation/reference/gitbook-ui.md`. On task pages, give one navigation step in bold with → (for example **Settings → Redirects**), and don't say which sidebar section something is under.
