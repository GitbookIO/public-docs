---
description: Sync your docs with a Git repository and work with pull requests.
icon: code-pull-request
---

# Git Sync

Git Sync lets technical teams synchronize a GitHub or GitLab repository with GitBook, turning Markdown files into a polished docs site. Edit in GitBook's editor while keeping content synced with your codebase, or edit the Markdown directly in your repo — either way, the other side stays up to date.

Git Sync is bi-directional: changes made in GitBook's editor sync automatically to Git, and commits made on GitHub or GitLab sync back to GitBook. Developers can commit directly from GitHub or GitLab, while technical writers, instructional designers, and product managers edit, discuss, and give feedback directly in GitBook.

{% hint style="info" %}
Only [administrators and creators](../collaboration/roles-permissions-inheritance.md) can enable and configure Git Sync.
{% endhint %}

{% hint style="info" %}
Git Sync supports IP allowlisting for Enterprise customers. If your GitHub, GitLab, or internal network only accepts traffic from approved IPs, allowlist these outbound Git Sync IPs first:

* `34.136.22.210`
* `34.29.189.57`
* `35.223.181.150`
* `34.72.115.112`
* `136.116.236.109`
{% endhint %}

### Get started

* [How Git Sync works](how-git-sync-works.md) — the mental model before you set anything up.
* [Enable GitHub Sync](enable-github-sync.md) or [Enable GitLab Sync](enable-gitlab-sync.md) — connect a repository.
* [.gitbook.yaml configuration](gitbook-yaml-configuration.md) — configure how GitBook parses your repository.
* [Work with monorepos](work-with-monorepos.md) — sync multiple sections from one repository.
* [Preview pull requests](preview-pull-requests.md) and [make batch changes](make-batch-changes.md) — day-to-day workflows once you're synced.
* [Troubleshoot Git Sync](troubleshoot-git-sync.md) — fixes for common errors.

### Working with an AI coding assistant

When working on your docs locally with Git Sync, you can point an AI coding assistant at GitBook's skill.md file to give it context about GitBook's blocks, features, and best practices — see Build with AI → GitBook Skills.
