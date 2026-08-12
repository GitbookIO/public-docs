---
description: "Easily import content from your previous documentation provider —\_or from GitHub or GitLab —\_using Git Sync in GitBook"
---

# Import or migrate your content to GitBook with Git Sync

One of the best ways to import your content into GitBook is using [Git Sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync). With Git Sync, you can choose to import a repository from either GitHub or GitLab, to add all your docs content to your new GitBook organization in minutes.

### Importing from GitHub

From your GitBook [space](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/content-structure/space), navigate to the top right of the screen and click **Set up Git Sync**. This will open a modal where you can configure the GitHub integration.

Before you go any further, you’ll need to install the [GitBook app](https://github.com/apps/gitbook-com/installations/select_target) on GitHub.

If you haven’t done this already, you’ll see a prompt to add the GitBook app to your GitHub account. Follow the instructions in the GitHub popover and either give GitBook-specific repository permissions, or allow access to all repositories, depending on your needs.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2Frz10Uj5T6eeDNw4zbQut%2Fgithub-sync-part-1.mp4?alt=media&token=d9a03db2-43b1-4766-8efb-ae73fc1654f9" %}
To set up GitHub Sync, authorize GitBook with GitHub and select the account your content lives in.
{% endembed %}

Next, select the GitHub repository you want to sync with your GitBook space, and choose which branch you want commits to be pushed to and synced from.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2FxhT2zohp0ulX3VptqL7Y%2Fgithub-sync-part-2.mp4?alt=media&token=719433fa-dc84-4b1e-a68e-c29656f9fa7e" %}
In GitBook, select the repository and branch you want to sync, choose the direction of the initial sync, and GitBook will do the rest.
{% endembed %}

Finally, you can start your initial sync. When syncing for the first time, you’ll have the option to sync in one of two directions:

1. **GitHub -> GitBook** will sync content from your selected branch with your GitBook space. This is great if you have existing Markdown content in a repository and want to import it into GitBook.
2. **GitBook -> GitHub** will sync content from your GitBook space to the selected branch. This is great if you’re starting with an empty repository and want to get your GitBook content in quickly.

### Connecting with GitLab

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2Fj5nRjt49RGbCcv85zpwD%2Fgitlab-sync.mp4?alt=media&token=243208a7-b54f-48c6-bfa4-33151ce88471" %}
To set up GitLab sync, you’ll first need to create an access token — then you can follow the same process as GitHub Sync.
{% endembed %}

From your space, navigate to the top right of the screen and click **Set up Git Sync**. This will open a modal where you can configure the GitLab integration.

From here, you’ll need to enter a personal GitLab access token. You can create your access token in GitLab by navigating to **Settings** > **Access Tokens**

When configuring the tokens, you need to ensure that you enable the following access for your token:

* `api`
* `read_repository`
* `write_repository`

Once you have generated the token, paste it into the text field in GitBook and click **Authenticate**.

Next, select the GitLab repository and branch you want to keep in sync with your GitBook content.

Finally, you can start your initial sync. When syncing for the first time, you’ll have the option to sync in one of two directions:

1. **GitLab -> GitBook** will sync content from your selected branch with your GitBook space. This is great if you have existing Markdown content in a repository and want to import it into GitBook.
2. **GitBook -> GitLab** will sync content from your GitBook space to the selected branch. This is great if you’re starting with an empty repository and want to get your GitBook content in quickly.

Once you have synced your content using Git Sync, the sync runs both ways. That means any changes you or your team make in your GitHub or GitLab repository will be reflected in GitBook, and vice versa.

***

[**→ How to find & replace or batch change with Git Sync**](/broken/pages/gEJCes43tXugzashxJNV)

[**→ Discover more about Git Sync on our website**](https://www.gitbook.com/solutions/git-sync)

[**→ Read the Git Sync documentation**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync)
