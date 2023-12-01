# GitHub pull request preview

{% hint style="info" %}
Customers who configured the GitBook GitHub app before 6th January 2021 and want to enable this feature will need to accept an updated permission request to enable read-only access to PRs. You should have received a notification requesting this access.
{% endhint %}

When you submit a Pull Request (PR) to a GitHub branch that has been synced to a GitBook space, you can preview the content before merging. This allows you to check the impact of changes before merging them.

You can use this feature to have a final layer of checks before merging a PR, allowing you to see your changes in a non-production environment before merging it into your synced branch.

<figure><img src="../../.gitbook/assets/Pull request preview2.png" alt=""><figcaption><p>Pull-Request preview</p></figcaption></figure>

### How to access preview links

This behavior works out of the box, provided you have given the [GitBook GitHub app](https://github.com/apps/gitbook-com) the necessary read-only permissions to PRs.

For every PR done using a target branch synced with a GitBook space, you’ll see a status added to the PR with a unique preview URL. Clicking the **Details** link on the status will take you to the preview URL for your content. You can then make sure the content is as expected before merging the PR.

{% hint style="info" %}
Preview links are only accessible by GitBook users.
{% endhint %}

### Security considerations

For security reasons, by default GitBook doesn’t currently generate previews for PRs opened from forks of your repository. Because the content of the PR preview is accessible under your own domain, whether on `.gitbook.io` or your [custom domain](../../published-documentation/custom-domain/finalize.md), a user could generate malicious content in a fork of your public repository and have it served under your name.

We allow users to explicitly configure this through an option in the Git Sync settings.
