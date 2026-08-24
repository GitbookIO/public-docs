---
description: >-
  Synchronize your GitBook docs with GitHub or GitLab with GitBook’s
  bi-directional integration
---

# GitHub & GitLab Sync

<figure><img src="../../.gitbook/assets/Site-wide Git Sync.png" alt="A GitBook screenshot showing the Git Sync setup"><figcaption><p>Set up Git Sync for your GitBook docs.</p></figcaption></figure>

### Overview

Git Sync allows technical teams to sync GitHub or GitLab repositories with GitBook and turn a repo of Markdown files into beautiful, user-friendly docs. Edit directly in GitBook’s powerful editor while keeping content synchronized with your codebase on GitHub or GitLab.

Git Sync is bi-directional, so changes you make directly in GitBook’s editor are automatically synced, as are any commits made on GitHub or GitLab. This allows developers to commit directly from GitHub or GitLab and technical writers, instructional designers, and product managers to edit, discuss and feedback changes directly in GitBook.

### Set up Git Sync

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-github">:github:</i></h4></td><td><h4>Set up GitHub Sync</h4></td><td>Set up and authorize the GitHub integration for GitBook.</td><td><a href="enabling-github-sync.md">enabling-github-sync.md</a></td></tr><tr><td><h4><i class="fa-gitlab">:gitlab:</i></h4></td><td><h4>Set up GitLab Sync</h4></td><td>Set up and authorize the GitLab integration for GitBook.</td><td><a href="enabling-gitlab-sync.md">enabling-gitlab-sync.md</a></td></tr></tbody></table>

{% hint style="info" %}
Git Sync supports IP allowlisting for Enterprise customers. If your GitHub, GitLab, or internal network only accepts traffic from approved IPs, allowlist these outbound Git Sync IPs before you enable the integration:

* `34.136.22.210`
* `34.29.189.57`
* `35.223.181.150`
* `34.72.115.112`
* `136.116.236.109`
{% endhint %}

{% hint style="info" %}
Only [administrators and creators](../../collaborate/member-management/roles.md) can enable and configure Git Sync.
{% endhint %}

### Working with AI Agents

When working on your docs locally with Git Sync, you can use GitBook's [skill.md file](../ai-coding-assistants-and-skillmd.md) to provide an AI coding assistant with context about GitBook's blocks, features, and best practices.

Head to [ai-coding-assistants-and-skillmd.md](../ai-coding-assistants-and-skillmd.md "mention") to learn more.
