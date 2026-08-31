---
description: Connect an entire published docs site to one Git repository with Git Sync.
---

# How to sync your entire docs site with a Git repository

Git Sync connects your repository to a published docs site. Your repo stays the source of truth, but you can now organize and manage all of your GitBook spaces under one unified Git Sync configuration — making it much easier to keep a multi-space site in sync with a single repository.

{% hint style="info" %}
Before you start, make sure you know:

* Which spaces are currently synced
* Which site each space should belong to
* The repo, branch, and project directory for each space
* Whether any space should stay hidden or in draft during the move
{% endhint %}

{% stepper %}
{% step %}
### **Create or open your site**

Open the site in GitBook that you plan on syncing with GitHub or GitLab. If you're consolidating multiple spaces into one site, it's a good idea to create the site structure first, so each space has a clear place in your navigation before you connect anything.

You can review and reorganize your structure at any time from your site's dashboard, in the **Structure** section of the **Settings** tab.
{% endstep %}

{% step %}
### **Initiate Git Sync**

From your site's dashboard, open the **Git Sync** panel. Here you'll authorize your Git provider and choose the repository and branch you want to sync with your site.

{% tabs %}
{% tab title="GitHub" icon="github" %}
Install the [GitBook app](https://github.com/apps/gitbook-com/installations/select_target) on GitHub before connecting your repository. Grant the app access to selected repositories or all repositories.
{% endtab %}

{% tab title="GitLab" icon="gitlab" %}
Create a personal access token in GitLab. In GitLab, navigate to **Settings** > **Access Tokens**. Enable the following token scopes:

* `api`
* `read_repository`
* `write_repository`

In GitBook, enter the token, then click **Authenticate**.
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
### **Verify your space mapping**

Once Git Sync is connected, review how each space in your site maps to a directory in your repository, and make sure everything points where you expect.

{% hint style="warning" %}
Setting up site-level Git Sync will override any existing space-based configuration. If you'd like to keep syncing certain spaces individually, remove them from the site-level configuration here.
{% endhint %}
{% endstep %}

{% step %}
### **Start your sync**

When you're happy with the mapping, click **Sync** to start syncing. GitBook will connect your repository to the site and begin keeping the two in sync.
{% endstep %}

{% step %}
### **Sync individual spaces (optional)**

If some spaces should sync to a separate repository, you can still configure them individually. Open the **Git Sync** panel from the space header of each space you want to sync on its own, and connect it to its own repo, branch, and directory.
{% endstep %}

{% step %}
### **Verify and test**

That's it! Explore your new setup to make sure everything is working as expected. Make a small change in your repository and check that the commit comes through to your site — and, if you're syncing in both directions, edit a page in GitBook and confirm the change lands back in your repo.
{% endstep %}
{% endstepper %}

[**→ How to find & replace or batch change with Git Sync**](find-and-replace-or-make-batch-changes-across-your-gitbook-docs-with-git-sync.md)

[**→ Discover more about Git Sync on our website**](https://www.gitbook.com/solutions/git-sync)

[**→ Read the Git Sync documentation**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync)
