---
description: >-
  Everything you need to know to set up a two-way sync between GitBook and
  GitHub or GitLab
---

# Bi-directional Git integration

With GitBook you can synchronize your content with GitHub or GitLab repositories and keep your content consistently up to date.

<figure><img src="../../.gitbook/assets/Synchronize with Git.png" alt="A screenshot of the GitBook app. On the right hand side is a panel with options for configuring the Git Sync feature. There are sections for authenticating your git account, choosing a git repository, and choosing a branch."><figcaption><p>Git Sync configuration panel</p></figcaption></figure>

## GitHub Sync: How it works

1. Add the GitBook app to your GitHub account or organization.
2. Link your GitBook space to a GitHub repository.
3. Select the branch you care about.
4. GitBook changes are synced to GitHub as commits, GitHub changes are synced to GitBook as history commits.

You can find full GitHub Sync instructions here:

{% content-ref url="enabling-github-sync.md" %}
[enabling-github-sync.md](enabling-github-sync.md)
{% endcontent-ref %}

## GitLab Sync: How it works

1. Generate an API token in GitLab and add it to your GitBook space.
2. Link your GitBook space to a GitLab repository.
3. Select the branch you care about.
4. GitBook changes are synced to GitLab as commits, GitLab changes are synced to GitBook as history commits.

You can find full GitLab Sync instructions here:

{% content-ref url="enabling-gitlab-sync.md" %}
[enabling-gitlab-sync.md](enabling-gitlab-sync.md)
{% endcontent-ref %}
