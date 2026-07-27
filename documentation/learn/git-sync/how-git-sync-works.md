---
description: The concepts behind GitBook's two-way sync with GitHub and GitLab.
---

# How Git Sync works

Git Sync keeps a GitBook section and a Git repository consistently up to date, in both directions — there's no single source of truth you have to remember to update.

### GitHub Sync

{% stepper %}
{% step %}
#### Add the GitBook app

Add the GitBook app to your GitHub account or organization.
{% endstep %}

{% step %}
#### Link a repository and branch

Link your GitBook section to a GitHub repository, then select the branch you care about.
{% endstep %}

{% step %}
#### Sync both ways

GitBook changes sync to GitHub as commits. GitHub changes sync to GitBook as history commits.
{% endstep %}
{% endstepper %}

See [Enable GitHub Sync](enable-github-sync.md) for the full setup.

### GitLab Sync

{% stepper %}
{% step %}
#### Generate an API token

Generate an API token in GitLab and add it to your GitBook section.
{% endstep %}

{% step %}
#### Link a repository and branch

Link your GitBook section to a GitLab repository, then select the branch you care about.
{% endstep %}

{% step %}
#### Sync both ways

GitBook changes sync to GitLab as commits. GitLab changes sync to GitBook as history commits.
{% endstep %}
{% endstepper %}

See [Enable GitLab Sync](enable-gitlab-sync.md) for the full setup.

### Change requests lock live edit

Once a section is connected to Git Sync, [live edit](../collaboration/comments-and-live-editing.md) mode is locked. This lets GitBook reliably sync content to your repository whenever someone merges a [change request](../collaboration/change-requests/README.md) in GitBook — every merge becomes a commit on your synced branch, and every commit on that branch becomes a history entry in GitBook.

### Commit messages & Autolink

By default, when GitBook exports content to your Git repository, it generates a commit message from the merged change request:

```
GITBOOK-14: Improve documentation about users management
```

**Autolink `GITBOOK-<num>` in GitHub and GitLab.** To automatically turn GitBook change request IDs (like `GITBOOK-123`) into links in your commits, enable GitHub's [Autolink references](https://help.github.com/en/github/administering-a-repository/configuring-autolinks-to-reference-external-resources) feature, using this URL format (where `spaceId` is your section's URL):

```
https://app.gitbook.com/s/{spaceId}/~/changes/<num>/
```

**Customize the commit message template.** If you're using a [monorepo](work-with-monorepos.md) or have specific commit message guidelines, you can customize GitBook's template. Available placeholders:

* `{change_request_number}` — the change request's unique numeric ID
* `{change_request_subject}` — the change request's subject when merged, or `No subject` if none was provided

The default template is:

```
GITBOOK-{change_request_number}: {change_request_subject}
```
