---
description: Connect a GitHub repository to a GitBook space.
---

# Enable GitHub Sync

### Getting started

In the section you want to sync with your GitHub repo, click **Set up** next to **Git Sync** in the [section header](../resources/the-gitbook-interface.md). From the provider list, click **GitHub Sync**.

### Authenticate with GitHub

If you're setting up GitHub Sync for the first time and haven't linked a GitHub account, you'll be prompted to do that when you begin configuring Git Sync. If you've already linked your account, you may still need to authenticate via GitHub.

{% hint style="warning" %}
If you see a **"Potential duplicated accounts"** error, your GitHub account is already linked to a different GitBook user account.

Log out of this session and log in using **Sign in with GitHub** to identify which account it's linked to. If you already know which GitBook account is associated with GitHub, log into that account and unlink your GitHub account (in settings) before logging back in and linking your current account.

See [Potential duplicated accounts when signing in](troubleshoot-git-sync.md#potential-duplicated-accounts-when-signing-in) for more detail.
{% endhint %}

### Install the GitBook app to your GitHub account

If you haven't already, you'll be prompted to add the [GitBook app](https://github.com/apps/gitbook-com) to your GitHub account. Follow the GitHub popover to grant specific repository permissions, or access to all repositories, depending on your needs.

### Select a repository and branch

Select the account and repository you want to keep in sync with your GitBook content.

{% hint style="info" %}
**Can't see your repository?** Make sure you've installed the [GitBook GitHub app](https://github.com/apps/gitbook-com) in the right scope — your personal account or the GitHub org where the repository lives — and that you've configured the correct repository access in the app.
{% endhint %}

Once you've selected the repository, choose which branch you want commits pushed to and synced from.

### Perform an initial sync

For the initial sync, the selected source is authoritative — it can replace existing content in its destination. Choose one of these directions:

1. **GitBook → GitHub:** GitBook is the source of truth. Use this only when the selected branch can receive your section's content.
2. **GitHub → GitBook:** The selected GitHub branch is the source of truth. Use this only when your section can receive that branch's content.

{% hint style="warning" %}
**GitHub → GitBook can replace your section's content.** If you select an empty repository, GitBook can replace your section with the repository's empty content. Before starting, confirm the repository, branch, and direction, and make sure the destination content is safe to replace.
{% endhint %}

When you're ready, start the initial sync.

### If you chose the wrong direction

Git Sync operations appear in the section's **Version history**. Find the revision immediately before the Git Sync operation and click **Rollback** to restore the prior content — see [Version history and page tags](../creating-content/version-history-and-page-tags.md) for the full rollback steps.

Disconnecting Git Sync stops future synchronization, but doesn't restore content automatically. If the pre-sync revision is unavailable, or you can't complete the rollback, [contact GitBook Support](../resources/get-support.md).

### Write and commit

You're good to go. If your section was in [live edit](../collaboration/comments-and-live-editing.md) mode, live edits are now locked — this lets GitBook reliably sync content to your repository whenever your team merges a [change request](../collaboration/change-requests/README.md).

Every change request merge results in a commit to your selected GitHub branch. Every commit to that branch syncs to your GitBook section as a history commit.

{% hint style="warning" %}
The GitHub app that powers this integration currently isn't available to customers on GitHub Enterprise Server instances.
{% endhint %}
