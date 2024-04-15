---
description: "Find out how to easily migrate your existing documentation —\_and which formats GitBook supports."
---

# Import

There are two methods for importing content into GitBook:

1. Using our import tool
2. Using Git Sync

### Using our import tool

The import function allows you to migrate and unify existing documentation in GitBook. You can choose to import single or multiple pages — although some limits apply.

{% hint style="info" %}
**Permissions**\
Only users with [editor permissions or higher](../account-management/member-management/roles.md) can edit pages.
{% endhint %}

### Supported import formats

GitBook supports imports from websites or files in the follow formats:

* Markdown (.md or .markdown)
* HTML (.html)
* Microsoft Word (.docx)

We also support imports from:

* Confluence
* Notion
* GitHub Wiki
* Quip
* Dropbox Paper
* Google Docs

To **import multiple pages** you can upload a ZIP containing HTML or Markdown files.

### The Import panel

When you create a new [space](editor/content-structure/what-is-a-space.md), you’ll have the option to import content from the bottom sheet of the first empty page:

Alternatively, you can always import a page or subpage by selecting **New page** > **Import new pages** in the [table of contents](editor/navigation.md#table-of-contents), or opening the Actions menu <img src="../.gitbook/assets/Actions menu.png" alt="" data-size="line"> for a page and choosing **Import subpages**.

<div data-full-width="false">

<figure><img src="../.gitbook/assets/import-button (2).png" alt=""><figcaption><p>There are two ways to import content into GitBook.</p></figcaption></figure>

</div>

After choosing an input source, you can select the file you’d like to import.

{% hint style="warning" %}
Although GitBook supports importing content from different sources, the end result may be different from your source due to differences in product features and document formats.
{% endhint %}

### Limitations

GitBook currently has the following limits for imported content:

* The maximum number of pages that can be uploaded in a single import is **20**.
* The maximum number of files (images etc.) that can be uploaded in a single import is **20**.

### Importing via Git Sync

If you're looking to import large amounts of content, importing using our Git Sync feature may be preferable as there is no limitation on the amount of content that can be imported.&#x20;

In order to use Git Sync to import, you will first need to get all of your content into markdown files in a Git repo (or folder if you're using a mono repo set up). If your current tool does not allow for markdown export, there are various online tools that can assist with conversion from other formats (pdf, html etc).&#x20;

Once you have this, you can follow the steps in our [Git sync docs](../integrations/git-sync/) to set up the integration. Be sure to select the direction 'GitHub -> GitBook' when choosing the initial sync direction.&#x20;

{% hint style="info" %}
If you're having trouble with importing using either method suggested here, please don't hesitate to reach out to support@gitbook.com for additional guidance.
{% endhint %}

