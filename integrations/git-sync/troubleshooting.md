# Troubleshooting

## I have a GitHub sync error <a href="#i-have-a-github-sync-error" id="i-have-a-github-sync-error"></a>

In case of errors, make sure that:‌

* Your repository **has a** `README.md` **file** at its root (or at the `root` folder specified in your `.gitbook.yaml`). This file is required and is used as the homepage for your documentation. For more details, refer to our [content configuration](content-configuration.md).
* If you have YAML frontmatters in your Markdown files, make sure they are valid using a [linter](http://www.yamllint.com).​

## ​GitBook is not using my `docs` folder <a href="#gitbook-is-not-using-my-docs-folder" id="gitbook-is-not-using-my-docs-folder"></a>

By default, GitBook uses the root of the repository as a starting point. A specific directory can be specified to scope the markdown files. See [Configuration](content-configuration.md).‌

## GitBook is creating new markdown files <a href="#gitbook-is-creating-new-markdown-files" id="gitbook-is-creating-new-markdown-files"></a>

**When synchronizing and editing from GitBook** with an existing Git repository, GitBook may create new markdown files instead of using the existing one.‌

## ​My repository is not listed <a href="#my-repository-is-not-listed" id="my-repository-is-not-listed"></a>

### For GitHub repositories

Make sure that you have installed the GitBook GitHub app to the correct location(s) (when installing the app, you can choose to install it to your personal GitHub, or to any organization you have permissions for) and that you have given the app the correct repository permissions.

### For GitLab repositories

Make sure that your Access Token has been configured with the following access:

* api
* read\_repository
* write\_repository

## ​Nothing happens on GitBook after adding a new file to my repository <a href="#nothing-happens-on-gitbook-after-adding-a-new-file-to-my-repository" id="nothing-happens-on-gitbook-after-adding-a-new-file-to-my-repository"></a>

{% hint style="warning" %}
**Note:** If your repository does not include a `SUMMARY.md` file, this article is not for you. Note that if you edited your content from GitBook at least once after setting up Git sync, GitBook should have created this file automatically.‌
{% endhint %}

If after updating your repository by adding or modifying a markdown file, you do not see the update reflected on GitBook and the sidebar doesn't indicate an error during the sync, your modified file(s) is probably not listed in [your `SUMMARY.md` file](content-configuration.md#summary).‌

This could either be because you created the file manually, or because you made an edit on GitBook and the GitBook to Git export phase of the sync created it for you.

The content of this file mirrors [your main Table of Contents](../../editor/content-structure.md) on GitBook and is used during the Git to GitBook import phase of the sync to recreate your ToC and re-conciliate upcoming updates from the repository with your existing content on GitBook.‌

If after ensuring that all your files are included in the `SUMMARY.md` file there's still nothing happening on GitBook, don't hesitate to [contact us](mailto:support@gitbook.com) 💌 for more information.
