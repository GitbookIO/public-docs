---
description: Sync your GitLab repo with GitBook
---

# Enabling GitLab Sync

This guide will take you through setting up your GitBook site with a repo on GitLab.

<figure><img src="../../.gitbook/assets/Git Sync - GitLab.png" alt="A GitBook screenshot showing GitLab Sync configuration options"><figcaption><p>GitLab Sync configuration options.</p></figcaption></figure>

{% stepper %}
{% step %}
### Open Git Sync for your site

From your site, open Git Sync in the sidebar.
{% endstep %}

{% step %}
### Connect GitLab

Create a Personal access token in your GitLab user settings. Enable `api`, `read_repository`, and `write_repository`, then enter the token in GitBook.

{% hint style="info" %}
If your token has a role, select `Maintainer` or `Admin`.
{% endhint %}
{% endstep %}

{% step %}
### Select a repository and branch

Under **Source repository**, select the repository that contains your documentation. Select the branch that GitBook syncs with. If the branch doesn’t exist, GitBook creates it during the initial sync.

{% hint style="info" %}
**Can’t find your repository?** Make sure your Personal access token has the required scopes and repository access.
{% endhint %}

{% hint style="warning" %}
If your `main` branch is protected, select a separate branch for Git Sync. You can merge that branch into `main` while keeping its protection.
{% endhint %}
{% endstep %}

{% step %}
### Choose an initial sync direction

Choose the source of truth for the initial sync. Select **Swap direction** if the repository content should replace the GitBook content.

{% hint style="warning" %}
**GitLab → GitBook can replace your site’s content.** Before you start the sync, confirm the repository, branch, and direction. Make sure the destination content is safe to replace.
{% endhint %}
{% endstep %}

{% step %}
### Set the project directory

If your documentation lives in a subdirectory, enter it under **Project directory**. GitBook stores your site’s `gitbook-docs.yaml` file in this directory. Use this configuration if your docs live within a [monorepo](monorepos.md).
{% endstep %}

{% step %}
### Map your spaces

Under **Content mapping**, assign each space to a directory in the repository. Use `./` for paths relative to the project directory. Use `/` for paths from the repository root. Newly linked spaces sync automatically.
{% endstep %}

{% step %}
### Review advanced options

If needed, configure agent instruction files, a commit message template, or fork previews.
{% endstep %}

{% step %}
### Sync your site

Click **Sync** to start the initial sync.
{% endstep %}

{% step %}
### Write and commit

Merge a change request in GitBook to commit its changes to GitLab. Commits to GitLab sync back to GitBook.
{% endstep %}
{% endstepper %}

#### Exclude a space from site-wide Git Sync

In the site’s Git Sync content mapping, click the remove icon next to the space you want to exclude. You can then configure Git Sync from that space.

If the site already has Git Sync, GitBook asks you to choose a scope:

* Select the site’s repository and branch to add the space to site-wide Git Sync.
* Select an independent repository and branch to configure Space Git Sync.

If the site doesn’t use Git Sync, GitBook configures Git Sync independently for the space.

To configure Git Sync for a single space, in the space you want to sync, click **Set up** next to **Git Sync** in the [space header](../../reference/gitbook-ui.md#space-header). From the provider list, click **GitLab Sync**, and click **Configure**.
