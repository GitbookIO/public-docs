# Troubleshooting

## I have a GitHub sync error <a href="#i-have-a-github-sync-error" id="i-have-a-github-sync-error"></a>

### Be sure to only create readme files in your repo

When Git Sync is enabled, be careful not to create readme files through the GitBook UI. Creating readme files through the GitBook UI:

* Creates duplicate README files in your repository
* Causes rendering conflicts between GitBook and GitHub
* May break builds and deployment processes
* Results in unpredictable file precedence

This includes files named README.md, readme.md, Readme.md, and README (without extension). Instead, remember to manage your README file directly in your git repository.

### Still facing errors?

Make sure that:‌

* Your repository **has a** `README.md` **file** at its root (or at the `root` folder specified in your `.gitbook.yaml`) that was created directly in your git repository. This file is required and is used as the homepage for your documentation. For more details, refer to our [content configuration](content-configuration.md).
* If you have YAML frontmatters in your Markdown files, make sure they are valid using a [linter](http://www.yamllint.com).​

## ​GitBook is not using my `docs` folder <a href="#gitbook-is-not-using-my-docs-folder" id="gitbook-is-not-using-my-docs-folder"></a>

By default, GitBook uses the root of the repository as a starting point. A specific directory can be specified to scope the markdown files. Take a look at our documentation on [content configuration](content-configuration.md) for more details.‌

## GitBook is creating new markdown files <a href="#gitbook-is-creating-new-markdown-files" id="gitbook-is-creating-new-markdown-files"></a>

**When synchronizing and editing from GitBook** with an existing Git repository, GitBook may create new markdown files instead of using the existing ones.‌ This is done to ensure GitBook doesn't overwrite files that existed in your repository before.

## Redirects aren't working correctly

The YAML file needs to be correctly formatted for the redirects to work. Errors such as incorrect indentation or whitespace can result in your redirects not working. [Validating your YAML file](https://www.yamllint.com/) can ensure that the redirects will work smoothly.

When setting redirects, do not add any leading slashes. For example, trying to redirect to `./misc/support.md` will not work.

It's also important to consider that as long as a page exists for a path, GitBook won’t be looking for a possible redirect. So if you're setting up a redirect for an old page to a new one, you will need to remove the old page in order for the redirect to work.

## ​My repository is not listed <a href="#my-repository-is-not-listed" id="my-repository-is-not-listed"></a>

### For GitHub repositories

Make sure that you have installed the GitBook GitHub app to the correct locations (when installing the app, you can choose to install it to your personal GitHub, or to any organization you have permissions for) and that you have given the app the correct repository permissions.

### For GitLab repositories

Make sure that your access token has been configured with the following access:

* `api`
* `read_repository`
* `write_repository`

## ​Nothing happens on GitBook after adding a new file to my repository <a href="#nothing-happens-on-gitbook-after-adding-a-new-file-to-my-repository" id="nothing-happens-on-gitbook-after-adding-a-new-file-to-my-repository"></a>

{% hint style="warning" %}
**This section specifically addresses problems when a `SUMMARY.md` file already exists**

If your repository does not include a `SUMMARY.md` file, GitBook will automatically create one upon the first sync. This means that if you edited your content from GitBook at least once after setting up Git sync, GitBook should have created this file automatically.‌
{% endhint %}

If after updating your repository by adding or modifying a markdown file, you do not see the update reflected on GitBook and the sidebar doesn’t indicate an error during the sync, your modified file(s) is probably not listed in [your `SUMMARY.md` file](content-configuration.md#summary).‌

This could either be because you created the file manually, or because you made an edit on GitBook and the GitBook to Git export phase of the sync created it for you.

The content of this file mirrors your [table of contents](../../resources/gitbook-ui/#table-of-contents) on GitBook and is used during the Git to GitBook import phase of the sync to recreate your table of contents and re-conciliate upcoming updates from the repository with your existing content on GitBook.‌

If after ensuring that all your files are included in the `SUMMARY.md` file there’s still nothing happening on GitBook, don’t hesitate to [contact support](https://gitbook.com/docs/help-center/further-help/how-do-i-contact-support) for assistance.

## GitHub preview is not showing

If your GitHub preview is not showing, it might be because your GitSync integration was configured before January 2022. Versions of GitSync configured before this date do not include GitHub Preview.

You should have received a notification requesting you to accept an updated permission request to enable read-only access to PRs.

In case you did not receive the notification, to troubleshoot you need to update to the new version:

1. Uninstall the GitSync integration from your organization.
2. Reinstall the new version with the updated permissions.

Note that uninstalling the GitSync integration will require reconfiguring the integration again on any sections it was previously connected to.

## Potential duplicated accounts when signing in

This error usually occurs when the GitHub account that you use to set up the sync is already associated with a different GitBook user account.

A good way to identify which GitBook account the GitHub account is already linked to is:

1. Log out from your current GitBook user session (i.e. `name@email.com`)
2. Log out from any GitHub user sessions.
3. Go to [the Log in page](https://app.gitbook.com/login).
4. Select the "Sign in with GitHub" option.
5. Enter your GitHub credentials.
6. Once logged in, go to [the account settings](https://app.gitbook.com/account) and either:
   1. Unlink the account from the "Third-party Login > GitHub" section in the Personal setting
   2. Delete the account altogether if you do not need it.
7. Log out from the session.
8. Log back in using your `name@email.com` GitBook account.
9. Try to set up Git Sync again.

## Error when pushing to a repository with a protected branch

This error occurs when your Git branch is protected:

```
Error: Missing permissions to push to the refs/heads/main protected branch. Check your branch configuration on your git provider.
```

Git Sync requires the GitBook app to push changes to your repository without restrictions, including during setup. Allow the GitBook app to bypass branch protections for the sync to work.

GitBook supports these branch protections, as long as the app is allowed to bypass them:

* Require a pull request before merging
* Restrict who can push to matching branches

In GitHub, open your repository's branch protection settings and allow `gitbook-com` to bypass those restrictions.

## Git Sync file size limitations

Git Sync limits individual file sizes to a maximum of 100MB. To improve performance and synchronization speed, optimize the size of files and assets in your repository.

## Git Sync status shows an unexpected error

**If the error appeared when merging a change request in GitBook:** create a new change request with a small change — such as adding a word — and merge it. This retriggers the sync and GitBook exports all content again, including the changes from the failed sync.

**If the error appeared when merging a commit from GitHub or GitLab:** create a new commit in your repository with a small change. When it merges, GitBook imports all content from the repository again, including the changes from the failed sync.

**If the error appeared during first-time setup:** remove the GitHub or GitLab integration, enable it again in your section, and go through the setup process once more.

If none of these steps help, [contact support](https://gitbook.com/docs/help-center/further-help/how-do-i-contact-support).

## My table of contents is not correctly structured

Your `SUMMARY.md` file mirrors your table of contents on GitBook — the way it's structured is reflected in your content. Make sure the file reflects the structure you want to see in your documentation. See [Content configuration](content-configuration.md#summary) for the expected format.

## Why am I getting a "Git authentication failed" message?

This message appears when you attempt to push to a repository that hasn't granted GitBook access. In that case, syncing from your repository to GitBook works, but not the other way — and your repositories may not be listed correctly.

For GitHub, grant access in your GitHub settings: open **Manage Organization → Integrations → Applications**, click **Configure** next to GitBook, and select the repositories the GitBook app can access.

For GitLab, make sure your access token is configured with `api`, `read_repository`, and `write_repository` access.

## Does Git Sync also sync pull requests?

No. Creating a pull request in GitHub or GitLab doesn't create a change request in GitBook, and creating a change request in GitBook doesn't create a pull request in your repository.
