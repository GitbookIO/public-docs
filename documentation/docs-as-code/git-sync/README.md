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

### How changes flow

Git Sync keeps two review workflows separate, and neither one creates the other:

* **A change request in GitBook** is how you propose and review edits inside GitBook. Merging one commits the change directly to your synced branch — it doesn't open a pull request or merge request in GitHub or GitLab. Each commit GitBook pushes is labeled with a `GITBOOK-<number>` reference so you can trace it back to the change request that produced it.
* **A pull request or merge request in your Git provider** is a change proposed in GitHub or GitLab. Merging one pushes a regular commit to the synced branch, which GitBook imports as a new revision — it doesn't create a GitBook change request.

Because the two are independent, review a change in whichever tool it started in: review GitBook change requests in GitBook, and review pull or merge requests in your Git provider.

{% hint style="info" %}
Content imported from a provider commit or pull request goes through the same Markdown conversion as any other Git import. GitBook block types without a Markdown equivalent may not round-trip exactly, so review imported content in GitBook after a sync.
{% endhint %}

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

### Conflicts and precedence

Because Git Sync is bi-directional, GitBook and your repository can both change the same content between syncs.

* **Changes to different content:** GitBook merges non-overlapping changes automatically.
* **The same block or line changed on both sides:** whichever side syncs last overwrites the other — this doesn't surface as a conflict for you to resolve. If you suspect a clash, check the GitBook change request and the repository diff before merging either one.
* **`SUMMARY.md` and repository structure:** if your repository's navigation changes while a GitBook change request that also touches navigation is still open, merging the change request can conflict with the repository's newer structure. Merge or close pending change requests before restructuring `SUMMARY.md` in your repository, and vice versa. See [Content configuration](content-configuration.md#summary) for how `SUMMARY.md` maps to your table of contents.

This is separate from [resolving merge conflicts](../../collaborate/change-requests/change-requests-in-a-space.md#resolving-merge-conflicts) between two GitBook change requests, which only applies to concurrent edits made inside GitBook.

### Rewritten history and force-pushes

If you force-push or otherwise rewrite the history of your synced branch, Git Sync follows the new branch tip on the next sync and imports the rewritten content — it doesn't reject non-fast-forward updates or roll back the published site on its own.

Before rewriting history on a synced branch:

* Merge or close any pending GitBook change requests first — they're based on the branch state before the rewrite, and merging one afterward can reintroduce content the rewrite removed.
* Keep a copy of the branch or the commit SHA you're rewriting from, so you can recover specific content from [version history](../../create-content/version-control.md) in GitBook if the rewrite removes something you still need.

### Working with AI Agents

When working on your docs locally with Git Sync, you can use GitBook's [skill.md file](../ai-coding-assistants-and-skillmd.md) to provide an AI coding assistant with context about GitBook's blocks, features, and best practices.

Head to [ai-coding-assistants-and-skillmd.md](../ai-coding-assistants-and-skillmd.md "mention") to learn more.
