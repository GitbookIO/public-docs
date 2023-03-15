---
description: Learn how to seamlessly search and navigate your documentation
---

# Quick find

GitBook's quick find command palette lets you search for – and quickly navigate between – all your content, as well as perform common space actions.

{% hint style="info" %}
**Permissions**

All member roles can use quick find. Quick find is compliant with your team permission settings, meaning that members will only be able to search the content they have permission to access.‌
{% endhint %}

## How to use quick find

When writing or reading documentation you'll want to find whatever you need quickly, wherever it’s located. Use our quick find command palette to search and navigate across all your content.

{% hint style="success" %}
**​**You can open the quick find palette by pressing **CMD + K** on Mac or **Ctrl + K** on Windows
{% endhint %}

<figure><img src="../.gitbook/assets/Quick find.png" alt="Open Quick find palette, which you to type in command or search a specific term"><figcaption><p>The quick find command palette</p></figcaption></figure>

## Display of results <a href="#display-of-results" id="display-of-results"></a>

Results of the space you're in are displayed first, followed by results from other spaces from the organization you're currently editing in, **as well as other organizations** you are a member of.

So type in what you need, take a look at results in other spaces, and pick the page or section you're interested in.

When you select a search result from an organization, you will switch to browsing that organization. To go back, use quick find to select a document in the organization you were in before, or use the organization switcher in the sidebar.

## Search filters

Quick find supports filtering your results by author, and by space or organization.

<details>

<summary>To filter your results by author</summary>

Add a `by:` filter to your query. You can then search for members of your organization by name, and select the author you're interested in.

</details>

<details>

<summary>To filter your results by space or organization</summary>

Add an `in:` filter to your query. Search for the space or organization you're interested in, and the results of your query will be scoped to the specified space or organization.

</details>

<figure><img src="../.gitbook/assets/Search filters.png" alt="Open Quick find palette with a filter enabled. You can filter your results by author or by searching in a specific content"><figcaption></figcaption></figure>

## Navigation and performing space actions with quick find

Quick find also helps you navigate to settings and organizations, as well as perform certain space actions like locking and unlocking [live edits](../collaboration/collaboration/live-edits.md), setting up [Git Sync](git-sync/), and starting a [change request](../collaboration/collaboration/change-requests.md).

To see the list of actions that quick find can kick off, open quick find and scroll down, or use the arrow keys to see the available options.

<figure><img src="../.gitbook/assets/Actions with quick find.png" alt="Open Quick find palette scrolled down to navigation and actions options. The actions allow you to move spaces, lock and unlock edits and many more. "><figcaption></figcaption></figure>

## ​Team permissions <a href="#team-permissions" id="team-permissions"></a>

Quick find is compliant with your team permission settings, meaning that users will only be able to search the content they have permission to access.‌

{% hint style="warning" %}
**Please note:** Multiple space search is _not_ available when viewing a published [GitBook space](../content-creation/content-structure/what-is-a-space.md) via its public URL. It's only available to logged-in members of a GitBook organization while they view the space in the GitBook app, based on their permission settings. External visitors of a public space can only search that space.
{% endhint %}

## ​A note on content indexing <a href="#indexation" id="indexation"></a>

We index your content by grouping it into sections. Sections are **headings** (H1, H2, or H3) with the content that follows it.

When a section starts with H1 and contains a lot of H2/H3 with text, your paragraph turns into a big section. We just show 3 lines of information in each result in the quick find results view. When your section is too big, sometimes the keyword match is hidden in a part of the section that isn't displayed in the preview. Don't worry, quick find still found matching sections\![\
](http://app.gitbook.com/@gitbook/s/gitbook-docs/\~/drafts/-Lt-3yOWRPE66HLv1wRo/primary/collaboration/conflict-resolution)
