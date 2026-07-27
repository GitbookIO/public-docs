---
description: Fixes for common Git Sync errors and sync conflicts.
---

# Troubleshoot Git Sync

### I have a GitHub sync error

**Only create readme files in your repo.** When Git Sync is enabled, don't create readme files through the GitBook UI — files named `README.md`, `readme.md`, `Readme.md`, or `README` (no extension) created this way:

* Create duplicate README files in your repository
* Cause rendering conflicts between GitBook and GitHub
* Can break builds and deployment processes
* Result in unpredictable file precedence

Manage your README directly in your Git repository instead.

**Still facing errors?** Make sure:

* Your repository has a `README.md` at its root (or at the `root` folder specified in your `.gitbook.yaml`), created directly in Git. This file is required as your documentation's homepage — see [.gitbook.yaml configuration](gitbook-yaml-configuration.md).
* Any YAML frontmatter in your Markdown files is valid — check it with a [linter](http://www.yamllint.com).

### GitBook is not using my `docs` folder

By default, GitBook uses the repository root as its starting point. Specify a directory to scope the Markdown files instead — see [.gitbook.yaml configuration](gitbook-yaml-configuration.md#root).

### GitBook is creating new markdown files

When syncing and editing from GitBook against an existing Git repository, GitBook may create new Markdown files instead of using existing ones. This happens to avoid overwriting files that already existed in your repository.

### Redirects aren't working correctly

The YAML needs to be correctly formatted — indentation or whitespace errors can break redirects. [Validate your YAML](https://www.yamllint.com/) to confirm.

When setting redirects, don't add leading slashes — for example, redirecting to `./misc/support.md`, not `/misc/support.md`.

Also note: as long as a page exists at a path, GitBook won't look for a redirect there. To redirect an old page to a new one, remove the old page first.

### My repository is not listed

**For GitHub repositories:** make sure you've installed the GitBook GitHub app to the right location (your personal account, or any organization you have permissions for) with the correct repository permissions.

**For GitLab repositories:** make sure your access token has `api`, `read_repository`, and `write_repository` access.

### Nothing happens on GitBook after adding a new file to my repository

{% hint style="warning" %}
This section specifically covers cases where a `SUMMARY.md` file already exists. If your repository doesn't include one, GitBook creates it automatically on first sync — so if you've edited content from GitBook at least once since setting up Git Sync, this file should already exist.
{% endhint %}

If you add or modify a Markdown file and don't see the update reflected on GitBook — with no sync error shown in the sidebar — the file is probably not listed in your [`SUMMARY.md`](gitbook-yaml-configuration.md#summary). This can happen if you created the file manually, or if an edit made in GitBook triggered the GitBook-to-Git export phase to create it for you.

`SUMMARY.md` mirrors your section's table of contents in GitBook, and is used during the Git-to-GitBook import phase to reconcile updates from the repository with your existing content.

If all your files are included in `SUMMARY.md` and you're still not seeing updates, [contact support](../resources/get-support.md).

### GitHub preview is not showing

If your GitHub preview isn't showing, your Git Sync integration was likely configured before January 2022 — versions from before that date don't include GitHub preview.

You should have received a notification asking you to accept an updated permission request for read-only PR access. If you didn't:

1. Uninstall the Git Sync integration from your organization.
2. Reinstall the new version with the updated permissions.

Uninstalling requires reconfiguring the integration on any sections it was previously connected to.

### Potential duplicated accounts when signing in

This usually happens when the GitHub account you use to set up sync is already associated with a different GitBook user account.

To identify which GitBook account it's linked to:

1. Log out of your current GitBook session (e.g. `name@email.com`).
2. Log out of any GitHub sessions.
3. Go to the [login page](https://app.gitbook.com/login).
4. Select **Sign in with GitHub**.
5. Enter your GitHub credentials.
6. Once logged in, go to [account settings](https://app.gitbook.com/account) and either:
   1. Unlink the account from **Third-party Login → GitHub** in Personal settings, or
   2. Delete the account entirely if you don't need it.
7. Log out.
8. Log back in using your `name@email.com` GitBook account.
9. Try setting up Git Sync again.
