# Enabling GitHub Sync

## 1. Get Started

In the space you want to sync with your GitHub repo, head to the space menu in the top right, and select 'Synchronize with Git'. From the Provider list, select GitHub, and hit 'Configure ->'.

![](<../../.gitbook/assets/Git Sync – Provider.png>)

## 2. Authenticate with GitHub

If you're setting up GitHub sync for the first time and haven't already linked a GitHub account, you'll be prompted to do that when you begin configuring Git Sync. If you've already linked your account, you might still need to authenticate via GitHub.

## 3. Install the GitBook app to your GitHub account

![](<../../.gitbook/assets/Git Sync – GH Config.png>)

If you've not already done so, you'll be prompted to add the GitBook app to your GitHub account. Follow the instructions in the GitHub popover and either give GitBook specific repo permissions, or allow access to all repositories, depending on your needs.

## 4. Select a repository and branch

Select the account and repository you want to keep in sync with your GitBook content.

{% hint style="info" %}
**Can't see your repository?** If you can't find your repository in the list, make sure that you've installed the GitBook GitHub app in the right scope (i.e. your personal account or the GitHub org where the repository lives) and that you've configured the correct repository access in the GitBook GitHub app.
{% endhint %}

Once you've selected the correct repository, choose which branch you want commits to be pushed to and synced from.

![](<../../.gitbook/assets/Git Sync – GH Filled.png>)

## 5. Perform an initial sync

When syncing for the first time, you'll have the option to sync GitBook -> GitHub, or GitHub -> GitBook.

Git**Book** -> Git**Hub** will sync your space's content **to** the selected branch. This is great if you're starting from an empty repository and want to get your GitBook content in quickly.

Git**Hub** -> Git**Book** will sync your space's content **from** the selected branch. This is great if you have existing markdown content in a repository and want to bring it into GitBook.

## 6. Write and commit!

You're good to go. You'll notice that if your space was in [live edit](../../editing-content/live-edits-and-real-time-collaboration.md) mode, it's now locked for live edits. This allows us to reliably sync content to your repository when[ change requests](../../editing-content/change-requests.md) are merged in GitBook, rather than the constant noise of trying to sync live edits!

If you're editing on GitBook, every change request merge will result in a commit to your selected GitHub branch.

If you're committing to GitHub, every commit will be synced to your GitBook space.
