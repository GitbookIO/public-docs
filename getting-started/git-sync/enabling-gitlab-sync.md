---
description: Set up and authorize the GitLab integration for GitBook
---

# Enabling GitLab Sync

### Getting started

In the space you want to sync with your GitLab repo, head to the space menu in the top right, and select **Synchronize with Git**. From the provider list, select **GitLab Sync**, and click **Configure**.

<figure><img src="../../.gitbook/assets/10_01_25_git_sync-gitlab.svg" alt=""><figcaption><p>GitLab Sync configuration options.</p></figcaption></figure>

### Generate and enter your API access token

You can generate an API access token in your GitLab user settings.

{% hint style="info" %}
There are two types of access tokens in GitLab: Project and Personal. Note that in order for the integration to work you’ll need to use a Personal token, which you can generate from your GitLab user preferences menu.
{% endhint %}

Ensure that you enable the following access for your token:

* `api`
* `read_repository`
* `write_repository`

If the tokens you create also have a specific role attached to them, also make sure that it has a `Maintainer` or `Admin` role.

Then you can paste the token into the API access token field when configuring your GitLab integration.

### Select a repository and branch

Select the repository you want to keep in sync with your GitBook content.

{% hint style="info" %}
**Can’t see your repository?** Ensure you’ve set the correct permissions when creating your API token.
{% endhint %}

Once you’ve selected the correct repository, choose which branch you want commits to be pushed to and synced from.

{% hint style="warning" %}
For many GitLab repositories, the `main` branch might be automatically set to protected. If this is the case, we recommend adding a specific branch to sync your content between. You can then merge this into `main` and keep the protection in place.
{% endhint %}

### Perform an initial sync

When syncing for the first time, you’ll have the option to sync in one of two directions:

1. Git<mark style="color:red;">**Book**</mark> -> Git**Lab** will sync your space’s content **to** the selected branch. This is great if you’re starting from an empty repository and want to get your GitBook content in quickly.
2. Git**Lab** -> Git<mark style="color:red;">**Book**</mark> will sync your space’s content **from** the selected branch. This is great if you have existing markdown content in a repository and want to bring it into GitBook.

### Write and commit

You’re good to go. You’ll notice that if your space was in [live edit](../../collaboration/live-edits.md) mode, live edits are now locked. This allows GitBook to reliably sync content to your repository when someone in your team merges a[ change request](../../collaboration/change-requests.md) in GitBook.

When you edit on GitBook, every change request merge will result in a commit to your selected GitLab branch.

When you commit to GitLab, every commit will be synced to your GitBook space as a history commit.

### "Edit on GitLab" Link

You can optionally show a link for your users to contribute to your documentation from your linked repository. To enable, select [Customize > Configuration](../../publishing-documentation/customization/extra-configuration.md).
