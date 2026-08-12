# Find & replace or make batch changes across your GitBook docs with Git Sync

{% hint style="warning" %}
#### GitBook now supports find & replace through GitBook Agent

Head to [GitBook Agent](/broken/spaces/NkEGS7hzeqa35sMXQZ4X/pages/KHHFlE1MtpVIaZboN8b2) to learn more about using GitBook Agent to edit pages in bulk.
{% endhint %}

When you change something about your product, manually updating your documentation in all the affected places can be a real pain. Thankfully, with [Git Sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync) in GitBook, it’s a simple process.

Because Git Sync links your documentation to a GitHub or GitLab repository, you can make changes from your code editor and they’ll automatically sync to your docs when you merge. It’s the best way to find & replace a specific word or phrase, or make bulk changes to your docs.&#x20;

Here’s how it works:

{% stepper %}
{% step %}
### Sync your GitBook space to a Git repository

If your GitBook space is not already synced to a Git repository, set it up using [the Git Sync guide in our documentation](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync). It will only take a few minutes and you’ll unlock some powerful new capabilities.
{% endstep %}

{% step %}
### Branch and clone your Git repository

Now that your content is synced, you can make changes to your docs from your repository:

1. First, create [a new branch of your repository in GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository) or [in GitLab](https://docs.gitlab.com/ee/user/project/repository/branches/).
2. Next, follow GitHub’s guide on [cloning a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) to download a local version of your branch. Once you’ve downloaded your branch, [open it in VS Code](https://code.visualstudio.com/docs/editor/codebasics#_opening-a-project) or your preferred code editor or IDE.
{% endstep %}

{% step %}
### Commit and push changes to your repository

1. Use your editor’s [find & replace feature](https://code.visualstudio.com/docs/editor/codebasics#_find-and-replace) to make bulk changes across multiple files at the same time.
2. After making your edits, you can commit them to your branch in the local Git repository.
3. When you’re ready, push the changes to your remote repository on GitHub or GitLab.
{% endstep %}

{% step %}
### Create a pull or merge request

Create [a pull request in GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) or [a merge request in GitLab](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html) for your branch.
{% endstep %}

{% step %}
### Merge your changes

You can request a review of your changes in either GitHub or GitLab. When you’re ready, you can merge the changes to update your documentation in GitBook.

{% hint style="warning" %}
**Note:** You can also review and merge your changes in the GitBook editor. However, when using find & replace on text you may accidentally replace text within configuration files like `SUMMARY.md` or `.gitbook.yaml`.&#x20;

This could cause broken links if not properly updated, so you should always check your changes in GitHub and GitLab before merging.
{% endhint %}
{% endstep %}
{% endstepper %}
