# Troubleshooting

## I have a GitHub sync error <a href="#i-have-a-github-sync-error" id="i-have-a-github-sync-error"></a>

In case of errors, make sure that:‌

* Your repository **has a** `README.md` **file** at its root (or at the `root` folder specified in your `.gitbook.yaml`). This file is required and is used as the homepage for your documentation. For more details, refer to our [content configuration](content-configuration.md).
* If you have YAML frontmatters in your Markdown files, make sure they are valid using a [linter](http://www.yamllint.com).​

## ​GitBook is not using my `docs` folder <a href="#gitbook-is-not-using-my-docs-folder" id="gitbook-is-not-using-my-docs-folder"></a>

By default, GitBook uses the root of the repository as a starting point. A specific directory can be specified to scope the markdown files. Take a look at our documentation on [content configuration](content-configuration.md) for more details.‌

## GitBook is creating new markdown files <a href="#gitbook-is-creating-new-markdown-files" id="gitbook-is-creating-new-markdown-files"></a>

**When synchronizing and editing from GitBook** with an existing Git repository, GitBook may create new markdown files instead of using the existing ones.‌ This is done to ensure GitBook doesn't overrite files that existed in your repository before.

## ​My repository is not listed <a href="#my-repository-is-not-listed" id="my-repository-is-not-listed"></a>

### For GitHub repositories

Make sure that you have installed the GitBook GitHub app to the correct locations (when installing the app, you can choose to install it to your personal GitHub, or to any organization you have permissions for) and that you have given the app the correct repository permissions.

### For GitLab repositories

Make sure that your access token has been configured with the following access:

* `api`
* `read_repository`
* `write_repository`

## My folders got duplicated

Make sure that all the folders in your repo are in lowercase. For example, if you have a folder called `Hello_World` GitBook won’t sync that folder correctly. Update the name of your folder to all lowercase, and enable sync again.

## ​Nothing happens on GitBook after adding a new file to my repository <a href="#nothing-happens-on-gitbook-after-adding-a-new-file-to-my-repository" id="nothing-happens-on-gitbook-after-adding-a-new-file-to-my-repository"></a>

{% hint style="warning" %}
**This section specifically addresses problems when a `SUMMARY.md` file already exists**

If your repository does not include a `SUMMARY.md` file, GitBook will automatically create one upon the first sync. This means that if you edited your content from GitBook at least once after setting up Git sync, GitBook should have created this file automatically.‌
{% endhint %}

If after updating your repository by adding or modifying a markdown file, you do not see the update reflected on GitBook and the sidebar doesn’t indicate an error during the sync, your modified file(s) is probably not listed in [your `SUMMARY.md` file](content-configuration.md#summary).‌

This could either be because you created the file manually, or because you made an edit on GitBook and the GitBook to Git export phase of the sync created it for you.

The content of this file mirrors your [table of contents](../../content-editor/editor/navigation.md#table-of-contents) on GitBook and is used during the Git to GitBook import phase of the sync to recreate your table of contents and re-conciliate upcoming updates from the repository with your existing content on GitBook.‌

If after ensuring that all your files are included in the `SUMMARY.md` file there’s still nothing happening on GitBook, don’t hesitate to [contact support](../../help-and-faq/faq/support.md) for assistance.

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
