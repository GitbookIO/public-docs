---
description: Use Git Sync to apply large-scale changes across many pages at once.
---

# Make batch changes

Editing page by page in the GitBook editor works well for day-to-day writing, but for changes that touch many pages at once — a terminology rename, a folder restructure, a find-and-replace across dozens of files — it's usually faster to work against the synced Git repository directly.

### Why batch changes work better in Git

Once a section is connected via [Git Sync](README.md), its content is just Markdown files in a repository. That means you can use your own tooling — an IDE's project-wide find-and-replace, a script, or a command-line tool — to make the same edit across many files at once, instead of opening each page individually in GitBook.

### Workflow

{% stepper %}
{% step %}
#### Make sure the section is Git-synced

Batch edits only make sense once a section syncs with a repository — see [Enable GitHub Sync](enable-github-sync.md) or [Enable GitLab Sync](enable-gitlab-sync.md) if it isn't set up yet.
{% endstep %}

{% step %}
#### Pull the latest synced content

Work from a local checkout of the branch GitBook syncs with, so you're editing the same content GitBook has.
{% endstep %}

{% step %}
#### Make your changes locally

Apply your bulk edit across the affected Markdown files. If you're restructuring pages, update [`SUMMARY.md`](gitbook-yaml-configuration.md#summary) to match — GitBook uses it to reconcile your table of contents on the next sync.
{% endstep %}

{% step %}
#### Commit and push (or open a pull request)

Push directly to the synced branch, or open a pull request first if you want a [preview](preview-pull-requests.md) and review before it lands. Either way, the change reaches GitBook as a single sync rather than dozens of individual edits.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
While a batch change is mid-flight, avoid editing the same pages in the GitBook UI — concurrent edits from both sides of a two-way sync are more likely to conflict the larger the change is. See [Troubleshoot Git Sync](troubleshoot-git-sync.md) if a sync doesn't come through as expected.
{% endhint %}
