---
description: Connect a GitLab repository to a GitBook space.
---

# Enable GitLab Sync

### Getting started

In the section you want to sync with your GitLab repo, click **Set up** next to **Git Sync** in the [section header](../resources/the-gitbook-interface.md). From the provider list, click **GitLab Sync**, then click **Configure**.

### Generate and enter your API access token

Generate an API access token in your GitLab user settings.

{% hint style="info" %}
GitLab has two types of access tokens: Project and Personal. The integration needs a **Personal** token, generated from your GitLab user preferences menu.
{% endhint %}

Enable the following access for your token:

* `api`
* `read_repository`
* `write_repository`

If your token also has a role attached, make sure it's `Maintainer` or `Admin`.

Then paste the token into the API access token field when configuring your GitLab integration.

### Select a repository and branch

Select the repository you want to keep in sync with your GitBook content.

{% hint style="info" %}
**Can't see your repository?** Make sure you've set the correct permissions when creating your API token.
{% endhint %}

Once you've selected the repository, choose which branch you want commits pushed to and synced from.

{% hint style="warning" %}
For many GitLab repositories, `main` is automatically protected. If that's the case, sync a different branch and merge it into `main` yourself, keeping the protection in place.
{% endhint %}

### Perform an initial sync

When syncing for the first time, choose one of two directions:

1. **GitBook → GitLab** syncs your section's content **to** the selected branch — good if you're starting from an empty repository and want your GitBook content in quickly.
2. **GitLab → GitBook** syncs your section's content **from** the selected branch — good if you already have Markdown content in a repository and want to bring it into GitBook.

### Write and commit

You're good to go. If your section was in [live edit](../collaboration/comments-and-live-editing.md) mode, live edits are now locked — this lets GitBook reliably sync content to your repository whenever your team merges a [change request](../collaboration/change-requests/README.md).

Every change request merge results in a commit to your selected GitLab branch. Every commit to that branch syncs to your GitBook section as a history commit.
