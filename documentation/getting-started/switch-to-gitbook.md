---
description: Bring existing documentation into GitBook from Git, CSV, or other platforms.
icon: swap
---

# Switch to GitBook

You can migrate and unify existing documentation in GitBook using the import tool. Import single or multiple pages using the built-in import tool, or [an entire Git repository using Git Sync](#import-from-a-github-or-gitlab-repo-using-git-sync).

## Using the Import panel

The Import panel makes it easy to migrate your content into your GitBook organization from another documentation website or from existing files.

When you import from another online documentation site, just add the site's URL and GitBook handles the rest.

By default, GitBook uses AI to streamline the import process — intelligently refining and cleaning up imported content that doesn't perfectly match GitBook's formats, so the output uses GitBook's blocks more effectively. You can disable this from the menu.

### Supported import formats

GitBook supports imports from docs websites or files in the following formats:

* Markdown (`.md` or `.markdown`)
* HTML (`.html`)
* Microsoft Word (`.docx`)

GitBook also supports imports from:

* Confluence
* Notion
* GitHub Wiki
* Quip
* Dropbox Paper
* Google Docs

To import multiple pages, upload a ZIP file containing HTML or Markdown files, or use the **Online docs** import option.

{% hint style="info" %}
GitBook is Markdown-based, so importing content in Markdown format yields the best results. If your current tools support exporting in Markdown, use that format for a smoother import.
{% endhint %}

### Where to start an import

When you create a new section, you'll have the option to import content in the modal that appears. If you create an empty section instead, use the **Quickstart** prompt at the bottom of the empty page when you click **Edit**.

You can also import a page or subpage at any time — select **Add new** → **Import pages** at the bottom of the [table of contents](../resources/the-gitbook-interface.md), or open a page's **Actions menu** and choose **Import subpages**.

After choosing an input source, select the file you'd like to import.

{% hint style="warning" %}
GitBook imports content from a range of sources, but differences in product features and document formats may cause variations in the imported content compared to the original.
{% endhint %}

### Limitations

* The maximum number of pages in a single import is **20**.
* The maximum number of files (images, etc.) in a single import is **20**.

## Import from a GitHub or GitLab repo using Git Sync

For large volumes of content, use [Git Sync](../learn/git-sync/README.md) instead. The built-in migration tool handles most imports, but Git Sync scales better for larger migrations.

{% hint style="info" %}
For a video demo, see the [dedicated guide to importing content with Git Sync](https://app.gitbook.com/s/LBGJKQic7BQYBXmVSjy0/editing-and-publishing-documentation/import-or-migrate-your-content-to-gitbook-with-git-sync).
{% endhint %}

{% stepper %}
{% step %}
#### Convert your content into Markdown

GitBook is Markdown-based, so importing content in Markdown format yields the best results. If your content isn't already in Markdown, use a script (like [Markitdown](https://github.com/microsoft/markitdown)) or an online tool to convert it first.
{% endstep %}

{% step %}
#### Organize your content in GitHub or GitLab

Git Sync happens at the section level, so plan carefully how to group your content — use multiple repositories or folders, and make sure the Markdown files end up in the right locations.
{% endstep %}

{% step %}
#### Set up sections and configure Git Sync

Create one or more sections in GitBook to organize your content. Install the [GitHub Sync](https://www.gitbook.com/integrations/github-sync) or [GitLab Sync](https://www.gitbook.com/integrations/gitlab-sync) integration in your organization, and configure it for those sections — synchronizing each one with the folder or repository you set up in the previous step.
{% endstep %}

{% step %}
#### Run Git Sync from GitHub or GitLab into GitBook

When configuring sync direction, choose GitHub → GitBook (or GitLab → GitBook). This pulls the contents of your folder or repository into GitBook.
{% endstep %}
{% endstepper %}
