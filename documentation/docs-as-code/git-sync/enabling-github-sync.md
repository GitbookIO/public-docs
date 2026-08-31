---
description: Sync your GitHub repo with GitBook
---

# Enabling GitHub Sync

This guide will take you through setting up your GitBook site with a repo on GitHub.

<figure><img src="../../.gitbook/assets/Git Sync - GitHub (1).png" alt="A GitBook screenshot showing GitHub Sync configuration options"><figcaption><p>GitHub Sync configuration options.</p></figcaption></figure>

{% stepper %}
{% step %}
### Open Git Sync for your site

From your site, open Git Sync in the sidebar.
{% endstep %}

{% step %}
### Connect GitHub

Connect the GitHub account that has access to the repository you want to sync.

{% hint style="warning" %}
If you see a **'Potential duplicated accounts'** error message at this step, this means your GitHub account is already linked with another GitBook user account.

To help you identify which accounts are linked, you will have to log out from this session and log in using the sign-in with GitHub method.

If you already know your GitBook account associated with GitHub you can log into that user account and unlink your GitHub account (done in settings) before logging back in and linking your current account.

Read more on our [troubleshooting page](troubleshooting.md#potential-duplicated-accounts-when-signing-in).
{% endhint %}
{% endstep %}

{% step %}
### Select a repository and branch

Under **Source repository**, select the repository that contains your documentation. Select the branch that GitBook syncs with. If the branch doesn’t exist, GitBook creates it during the initial sync.

{% hint style="info" %}
**Can’t find your repository?** If you can't find your repository in the list, make sure that you've installed the [GitBook GitHub app](https://github.com/apps/gitbook-com) in the right scope (i.e. your personal account or the GitHub org where the repository lives). You should also check that you’ve configured the correct repository access in the GitBook GitHub app.
{% endhint %}
{% endstep %}

{% step %}
### Choose an initial sync direction

Choose the source of truth for the initial sync. Select **Swap direction** if the repository content should replace the GitBook content.

{% hint style="warning" %}
**GitHub → GitBook can replace your section’s content.** If you select an empty repository, GitBook can replace your section with the repository’s empty content.

Before you start the initial sync, confirm the repository, branch, and direction. Make sure the destination content is safe to replace.
{% endhint %}
{% endstep %}

{% step %}
### Set the project directory

If your documentation lives in a subdirectory, enter it under **Project directory**. GitBook stores your site’s `docs.yaml` file in this directory. Use this configuration if your docs live within a [monorepo](monorepos.md).
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

Merge a change request in GitBook to commit its changes to GitHub. Commits to GitHub sync back to GitBook.
{% endstep %}
{% endstepper %}

#### Exclude a space from site-wide Git Sync

In the site’s Git Sync content mapping, click the remove icon next to the space you want to exclude. You can then configure Git Sync from that space.

If the site already has Git Sync, GitBook asks you to choose a scope:

* Select the site’s repository and branch to add the space to site-wide Git Sync.
* Select an independent repository and branch to configure Space Git Sync.

If the site doesn’t use Git Sync, GitBook configures Git Sync independently for the space.

To configure Git Sync for a single space, in the space you want to sync, click **Set up** next to **Git Sync** in the [space header](../../reference/gitbook-ui.md#space-header). From the provider list, click **GitHub Sync**.

{% hint style="warning" %}
The GitHub app that powers our GitHub integration is currently not available to customers on GitHub Enterprise Server instances.
{% endhint %}
