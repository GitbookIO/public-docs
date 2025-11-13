---
description: >-
  How to import existing content into GitBook from Confluence, Notion, Git and
  more
icon: arrow-up-to-line
---

# Importing content

You can migrate and unify existing documentation in GitBook using the import tool.

You have the option to import single or multiple pages using our built-in import tool — or [an entire Git repository using Git Sync](import.md#import-using-git-sync).

## Using the Import Panel

### Supported import formats

GitBook supports imports from websites or files in the following formats:

* Markdown (`.md` or `.markdown`)
* HTML (`.html`)
* Microsoft Word (`.docx`)

We also support imports from:

* Confluence
* Notion
* GitHub Wiki
* Quip
* Dropbox Paper
* Google Docs

If you want to **import multiple pages**, you can upload a ZIP file containing HTML or Markdown files.

{% hint style="info" %}
GitBook is Markdown-based, so importing content in Markdown format will yield the best results. If your current tools support exporting in Markdown, we recommend using that format for a smoother import process.
{% endhint %}

### The Import panel

<figure><img src="../.gitbook/assets/10_01_25_import_modal.svg" alt="A GitBook screenshot showing the import panel"><figcaption><p>The import panel in GitBook.</p></figcaption></figure>

When you create a new space, you’ll have the option to import content from the bottom sheet of the first empty page.

Alternatively, you can always import a page or subpage by selecting **New page** > **Import new pages** in the [table of contents](../resources/gitbook-ui/#table-of-contents), or opening the Actions menu <picture><source srcset="../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/actions_icon_light.svg" alt="The Actions menu icon in GitBook"></picture> for a page and choosing **Import subpages**.

After choosing an input source, you can select the file you’d like to import.

{% hint style="warning" %}
GitBook imports content from various sources, but differences in product features and document formats may cause variations in the imported content compared to the original source.
{% endhint %}

### Limitations

GitBook currently has the following limits for imported content:

* The maximum number of pages that can be uploaded in a single import is **20**.
* The maximum number of files (images etc.) that can be uploaded in a single import is **20**.

***

## Import using Git Sync

For importing large volumes of content into GitBook, we recommend using [Git Sync](git-sync/). Unlike our integrated import tool, Git Sync is better suited for handling larger migrations efficiently.

{% hint style="info" %}
You’ll find the essential steps to import your content below. For more detailed steps and a video demo, head over to our dedicated guide to [importing content into GitBook using Git Sync](https://app.gitbook.com/s/LBGJKQic7BQYBXmVSjy0/editing-and-publishing-documentation/import-or-migrate-your-content-to-gitbook-with-git-sync).
{% endhint %}

Here’s how to do it:

{% stepper %}
{% step %}
#### Convert your content into Markdown

GitBook is Markdown-based, so importing content in Markdown format will yield the best results. If your current tools support exporting in Markdown, we recommend using that format for a smoother import process.

If your content isn’t already in Markdown files, we recommend using a script (like [Markitdown](https://github.com/microsoft/markitdown)) or an online tool to convert your content.
{% endstep %}

{% step %}
#### Organize your content in GitHub or GitLab

When setting up your GitBook site, it’s crucial to organize your content in your GitHub or GitLab repository efficiently. Since Git Sync occurs at the space level, carefully plan how to group your content. Create multiple repositories or folders, ensuring the necessary Markdown files are in the correct locations.
{% endstep %}

{% step %}
#### Set up spaces and Git Sync

To organize your content, create one or more spaces in GitBook as needed. Install the [GitHub Sync](https://www.gitbook.com/integrations/github-sync) or [GitLab Sync](https://www.gitbook.com/integrations/gitlab-sync) integrations in your organization and configure it for those spaces. You’ll need to synchronize your space with the folder or repository you set up in the previous step.
{% endstep %}

{% step %}
#### Run Git Sync in the direction GitHub → GitBook

When following the configuration process, make sure you select the direction of GitHub → GitBook. This will result in the contents of your folder or repository being pulled from GitHub or GitLab into GitBook.
{% endstep %}
{% endstepper %}
