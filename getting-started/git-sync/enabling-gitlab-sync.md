# Enabling GitLab Sync

## 1. Get Started

In the space you want to sync with your GitLab repo, head to the space menu in the top right, and select 'Synchronize with Git'. From the Provider list, select **GitLab**, and hit 'Configure ->'.

![](<../../.gitbook/assets/Git Sync – GitLab.png>)

## 2. Generate and enter your API token

You can generate an API token in your GitLab user settings.

Ensure that you enable the following access for your token:

* api
* read\_repository
* write\_repository

![](<../../.gitbook/assets/Git Sync – GitLab Config.png>)

Then you can paste the token into the Api Access Token field when configuring your GitLab integration.

## 3. Select a repository and branch

Select the repository you want to keep in sync with your GitBook content.

{% hint style="info" %}
**Can't see your repository?** Ensure you've set the correct permissions when creating your API token.
{% endhint %}

Once you've selected the correct repository, choose which branch you want commits to be pushed to and synced from.

![](<../../.gitbook/assets/Git Sync – GitLab Filled.png>)

{% hint style="info" %}
**Good to know:** For many GitLab repositories, the `main` branch might be automatically set to 'protected'. If this is the case, we recommend adding a specific branch to sync your content between. You can then merge this into `main` and keep the protection in place.
{% endhint %}

## 4. Perform an initial sync

When syncing for the first time, you'll have the option to sync GitBook -> GitLab, or GitLab -> GitBook.

Git**Book** -> Git**Lab** will sync your space's content **to** the selected branch. This is great if you're starting from an empty repository and want to get your GitBook content in quickly.

Git**Lab** -> Git**Book** will sync your space's content **from** the selected branch. This is great if you have existing markdown content in a repository and want to bring it into GitBook.

## 5. Write and commit!

You're good to go. You'll notice that if your space was in [live edit](../collaboration/live-edits.md) mode, it's now locked for live edits. This allows GitBook to reliably sync content to your repository when[ change requests](../collaboration/change-requests.md) are merged in GitBook, rather than the constant noise of trying to sync live edits!

If you're editing on GitBook, every change request merge will result in a commit to your selected GitLab branch.

If you're committing to GitLab, every commit will be synced to your GitBook space.
