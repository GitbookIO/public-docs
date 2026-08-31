---
description: "Easily import content from your previous documentation provider —\_or from GitHub or GitLab —\_using Git Sync in GitBook"
---

# Import or migrate your content to GitBook with Git Sync

One of the best ways to import your content into GitBook is using [Git Sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync). With Git Sync, you can choose to import a repository from either GitHub or GitLab, to add all your docs to a GitBook site in just a few minutes.

{% tabs %}
{% tab title="Import multiple sections" %}
Git Sync allows you to sync multiple spaces and folders of content into one GitBook site.&#x20;

{% stepper %}
{% step %}
### Create or open your site

Create a site and add each section to its navigation. Match each section to a directory in your repository.
{% endstep %}

{% step %}
### Connect your repository

From your site dashboard, open **Git Sync** in the sidebar. Authenticate with GitHub or GitLab, then select your repository and branch.
{% endstep %}

{% step %}
### Map your sections

Review the directory mapping for each section. Make sure every section points to the correct repository directory.
{% endstep %}

{% step %}
### Choose the initial sync direction

Choose one of these directions:

* **Repository → GitBook:** Import content from the selected branch into your space.
* **GitBook → repository:** Export your space content to the selected branch.
{% endstep %}

{% step %}
### Start and verify the sync

Click **Sync** to import your content. Confirm that each repository directory appears in the expected site section.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Import a single section" %}
You can sync a single space of a GitBook site with a Git repository by following these steps:

{% stepper %}
{% step %}
### Open Git Sync

In your GitBook [space](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/content-structure/space), click **Set up Git Sync**.
{% endstep %}

{% step %}
### Configure GitHub or GitLab

#### GitHub

Install the [GitBook app](https://github.com/apps/gitbook-com/installations/select_target) on GitHub. Grant access to selected repositories or all repositories.

In GitBook, authorize GitBook with GitHub and select the account that contains your content.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2Frz10Uj5T6eeDNw4zbQut%2Fgithub-sync-part-1.mp4?alt=media&token=d9a03db2-43b1-4766-8efb-ae73fc1654f9" %}
Authorize GitBook with GitHub and select the account that contains your content.
{% endembed %}

#### GitLab

In GitLab, select **Settings** → **Access Tokens**. Create a personal access token with these scopes:

* `api`
* `read_repository`
* `write_repository`

In GitBook, enter the token and click **Authenticate**.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2Fj5nRjt49RGbCcv85zpwD%2Fgitlab-sync.mp4?alt=media&token=243208a7-b54f-48c6-bfa4-33151ce88471" %}
Create a GitLab access token, then authenticate GitBook.
{% endembed %}
{% endstep %}

{% step %}
### Select your repository and branch

Select the repository and branch that contain the section you want to import.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2FxhT2zohp0ulX3VptqL7Y%2Fgithub-sync-part-2.mp4?alt=media&token=719433fa-dc84-4b1e-a68e-c29656f9fa7e" %}
Select a repository and branch, then choose the initial sync direction.
{% endembed %}
{% endstep %}

{% step %}
### Choose the initial sync direction

Choose one of these directions:

* **Repository → GitBook:** Import content from the selected branch into your space.
* **GitBook → repository:** Export your space content to the selected branch.
{% endstep %}

{% step %}
### Start and verify the sync

Click **Sync** to start the initial sync. After it finishes, Git Sync keeps GitBook and your repository synchronized in both directions.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

[**→ How to find & replace or batch change with Git Sync**](find-and-replace-or-make-batch-changes-across-your-gitbook-docs-with-git-sync.md)

[**→ Discover more about Git Sync on our website**](https://www.gitbook.com/solutions/git-sync)

[**→ Read the Git Sync documentation**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync)
