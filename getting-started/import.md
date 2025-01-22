---
icon: arrow-up-to-line
description: >-
  How to import existing content into GitBook from Confluence, Notion, Git and
  more
---

# Importing content

You can migrate and unify existing documentation in GitBook using the import tool. You have the option to import single or multiple pages — or an entire Git repository.

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

<figure><img src="../.gitbook/assets/10_01_25_import_modal.svg" alt=""><figcaption><p>The import panel in GitBook.</p></figcaption></figure>

When you create a new space, you’ll have the option to import content from the bottom sheet of the first empty page.

Alternatively, you can always import a page or subpage by selecting **New page** > **Import new pages** in the [table of contents](../resources/gitbook-ui.md#table-of-contents), or opening the Actions menu <picture><source srcset="../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/actions_icon_light.svg" alt=""></picture> for a page and choosing **Import subpages**.

After choosing an input source, you can select the file you’d like to import.

{% hint style="warning" %}
GitBook imports content from various sources, but differences in product features and document formats may cause variations in the imported content compared to the original source.
{% endhint %}

### Limitations

GitBook currently has the following limits for imported content:

* The maximum number of pages that can be uploaded in a single import is **20**.
* The maximum number of files (images etc.) that can be uploaded in a single import is **20**.



## Importing using Git Sync

For importing large volumes of content into GitBook, we recommend using Git Sync. Unlike our default import tool, Git Sync is better suited for handling larger migrations efficiently.

Here are the steps:

{% stepper %}
{% step %}
### Get your content into markdown

If your content isn't already in markdown files, we recommend using some scripting or online tools to translate the content.
{% endstep %}

{% step %}
### Organise your content in GitHub or Gitlab

When setting up your GitBook site, it's crucial to organize your content in git efficiently. Since git sync occurs at the space level, carefully plan how to group content. Create multiple repositories or folders, ensuring the necessary markdown files are in the correct locations.
{% endstep %}

{% step %}
### Set up spaces and git sync

To organize your content, create one or more spaces in GitBook as needed. Install Git sync on these spaces and configure it to synchronize with the appropriate folder or repository set up in step 2.&#x20;
{% endstep %}

{% step %}
### Run git sync with direction GitHub -> GitBook

When finishing the configuration ensure you select the direction of GitHub -> GitBook. Run the sync.
{% endstep %}
{% endstepper %}
