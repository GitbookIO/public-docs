---
description: See a preview of your content when making a pull request in GitHub
---

# GitHub pull request preview

When you submit a pull request (PR) to a GitHub branch that has been synced to a GitBook space, you can preview the content before merging. This allows you to check the impact of changes before merging them.

You can use this feature to have a final layer of checks before merging a PR, allowing you to see your changes in a non-production environment before merging it into your synced branch.

<figure><img src="../../.gitbook/assets/10_01_25_git_sync_preview.svg" alt="A screenshot showing a pull request in GitHub for changes to some docs.“ ><figcaption><p>See a preview of your GitBook site when making a Pull Request.</p></figcaption></figure>

### How to access preview links

This behavior works out of the box, provided you have given the [GitBook GitHub app](https://github.com/apps/gitbook-com) the necessary read-only permissions to PRs.

For every PR create using a target branch synced with a GitBook space, you’ll see a status added to the PR with a unique preview URL. Clicking the **Details** link on the status will take you to the preview URL for your content. You can then make sure the content is as expected before merging the PR.

{% hint style="info" %}
Preview links are only accessible by users with a GitBook account.
{% endhint %}

### Security considerations

For security reasons, by default GitBook doesn’t currently generate previews for PRs opened from forks of your repository. Because the content of the PR preview is accessible under your own domain, whether on `.gitbook.io` or your custom domain, a user could generate malicious content in a fork of your public repository and have it served under your name.

We allow users to explicitly configure this through an option in the Git Sync settings.
