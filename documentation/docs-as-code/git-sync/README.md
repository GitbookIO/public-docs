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

### How changes sync and conflict

Git Sync keeps GitBook and your repository in step by syncing one side to the other each time content changes. Understanding which side moves, and when, avoids most sync surprises.

#### The source of truth

You choose a source of truth once, when you set up Git Sync — see [Choose an initial sync direction](enabling-github-sync.md#choose-an-initial-sync-direction). That choice applies to the initial sync only: the selected side replaces the other side's content.

After the initial sync, neither side is permanently authoritative. Sync is bi-directional and event-driven:

* Merging a change request in GitBook exports that content to the synced branch.
* A commit landing on the synced branch imports that content into GitBook.

Each sync brings the destination in line with the source of the change. The most recent sync wins, so the last change to complete a sync determines the published content.

{% hint style="warning" %}
**Avoid editing the same content on both sides at once.** GitBook detects conflicts between change requests within GitBook, but an import from your repository and an unexported GitBook edit are not reconciled the same way — an import can replace GitBook content that was never exported. If you're making a large change, make it on one side and let it sync before editing the other.
{% endhint %}

#### Two kinds of conflict

The conflict flow you use depends on where the competing changes live:

| Where the conflict is                                                   | How to resolve it                                                                                                                                                       |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Between two change requests in GitBook                                   | Resolve it in GitBook. See [Resolving merge conflicts](../../collaborate/change-requests/change-requests-in-a-space.md#resolving-merge-conflicts).                       |
| Between branches in your repository, before the content reaches GitBook  | Resolve it in Git with your usual workflow, then push the resolved result to the synced branch. GitBook imports the result — it never sees the conflict.                  |

When you resolve a conflict in `SUMMARY.md` in your repository, remove every conflict marker (`<<<<<<<`, `=======`, `>>>>>>>`) before you push. GitBook parses `SUMMARY.md` to rebuild your table of contents, and markers left in the file produce a navigation structure you didn't intend. Check the merged file against the structure you want — see [Configure navigation with SUMMARY.md](content-configuration.md#configure-navigation-with-summary.md).

If a GitBook change request is out of date with navigation changes that arrived from your repository, update it before merging. This pulls the imported structure into your change request so you resolve the difference once, in GitBook, rather than producing a second conflicting export.

{% hint style="info" %}
Rewriting the history of the synced branch — force-pushing, rebasing, or resetting it — puts your repository and GitBook into a state Git Sync doesn't reconcile automatically. Prefer a forward commit that reverts the content instead. If you've already rewritten the synced branch and your content is out of step, [contact support](../../help/contact-support.md) rather than pushing further rewrites.
{% endhint %}

### Working with AI Agents

When working on your docs locally with Git Sync, you can use GitBook's [skill.md file](../ai-coding-assistants-and-skillmd.md) to provide an AI coding assistant with context about GitBook's blocks, features, and best practices.

Head to [ai-coding-assistants-and-skillmd.md](../ai-coding-assistants-and-skillmd.md "mention") to learn more.
