---
description: How to set up and authorize the GitHub Sync integration for GitBook
---

# Enabling GitHub Sync

## 1. Get started

In the space you want to sync with your GitHub repo, head to the space menu in the top right, and select **Synchronize with Git**. From the provider list, select **GitHub**, and click **Configure**.

<figure><img src="../../.gitbook/assets/GitHub sync.png" alt=""><figcaption><p>Choose GitHub as your Git provider</p></figcaption></figure>

## 2. Authenticate with GitHub

If you’re setting up GitHub Sync for the first time and haven’t already linked a GitHub account, you’ll be prompted to do that when you begin configuring Git Sync. If you’ve already linked your account, you might still need to authenticate via GitHub.

## 3. Install the GitBook app to your GitHub account

<figure><img src="../../.gitbook/assets/GitHub authentication.png" alt=""><figcaption><p>Authenticate your GitHub account to connect with GitHub</p></figcaption></figure>

If you’ve not already done so, you’ll see a prompt to add the GitBook app to your GitHub account. Follow the instructions in the GitHub popover and either give GitBook specific repo permissions, or allow access to all repositories, depending on your needs.

## 4. Select a repository and branch

Select the account and repository you want to keep in sync with your GitBook content.

{% hint style="info" %}
**Can’t see your repository?** If you can't find your repository in the list, make sure that you've installed the GitBook GitHub app in the right scope (i.e. your personal account or the GitHub org where the repository lives). You should also check that you’ve configured the correct repository access in the GitBook GitHub app.
{% endhint %}

Once you’ve selected the correct repository, choose which branch you want commits to be pushed to and synced from.

<figure><img src="../../.gitbook/assets/Synchronize with Git.png" alt=""><figcaption><p>Choose your GitHub repository and branch</p></figcaption></figure>

## 5. Perform an initial sync

When syncing for the first time, you’ll have the option to sync in one of two directions:

1. Git**Book** -> Git**Hub** will sync your space’s content **to** the selected branch. This is great if you’re starting from an empty repository and want to get your GitBook content in quickly.
2. Git**Hub** -> Git**Book** will sync your space’s content **from** the selected branch. This is great if you have existing Markdown content in a repository and want to bring it into GitBook.

## 6. Write and commit!

You’re good to go. You’ll notice that if your space was in [live edit](../../collaboration/collaboration/live-edits.md) mode, live edits are now locked. This allows us to reliably sync content to your repository when someone in your team merges a[ change request](../../collaboration/collaboration/change-requests.md) in GitBook — rather than the constant noise of trying to sync live edits!

When you edit on GitBook, every change request merge will result in a commit to your selected GitHub branch.

When you commit to GitHub, every commit will be synced to your GitBook space as a history commit.