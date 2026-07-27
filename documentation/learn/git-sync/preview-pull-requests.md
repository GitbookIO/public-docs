---
description: Preview docs changes from pull requests before merging.
---

# Preview pull requests

When you open a pull request against a GitHub branch synced to a GitBook section, you can preview the content before merging — a final check to see the impact of your changes in a non-production environment.

### How to access preview links

This works out of the box, provided the [GitBook GitHub app](https://github.com/apps/gitbook-com) has the necessary read-only permissions to PRs.

For every PR targeting a synced branch, GitHub shows a status with a unique preview URL. Click **Details** on that status to open the preview and check the content before merging.

{% hint style="info" %}
Preview links are only accessible to users with a GitBook account.
{% endhint %}

### Security considerations

By default, GitBook doesn't generate previews for PRs opened from forks of your repository. Since preview content is served under your own domain (`.gitbook.io` or your custom domain), allowing fork previews by default could let someone generate malicious content in a public fork and have it served under your name. You can explicitly opt into fork previews in your Git Sync settings.

### FAQ

<details>

<summary>Why can't I see a preview of my GitBook documentation in my pull request?</summary>

Common causes:

* **Your site isn't published.** PR preview URLs are served from your published docs site (on `.gitbook.io` or your custom domain).
* **Your site is behind authenticated access.** Git Sync PR previews aren't available for sites published behind [authenticated access](../access/authenticated-access/README.md).

</details>
