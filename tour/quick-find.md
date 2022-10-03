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

When writing or reading docs, you'll want to find whatever you need quickly, wherever it’s located.

Use our quick find command palette to search and navigate across all your content.

{% hint style="success" %}
**​**You can easily open the quick find palette by pressing **CMD + K** on Mac or **Ctrl + K** on Windows.
{% endhint %}

![](<../.gitbook/assets/Command Palette.png>)

## Display of results <a href="#display-of-results" id="display-of-results"></a>

Results of the space you're in are displayed first, followed by results from other spaces from the organization you're currently editing in, **as well as other organizations** you are a member of.

So write down what you need, take a look at results in other spaces, pick the page or section you're interested in and voilà!

When you select a search result from an organization, you will switch to browsing that organization. To go back, use Quick Find to select a document in the organization you were in before, or use the organization switcher in your left-hand sidebar.

## Search filters

Quick find supports filtering your results by author, and by space or organization.

To filter your results by author, add a `by:` filter to your query. You can then search for members of your organization by name, and select the author you're interested in.

![](<../.gitbook/assets/Command Palette - s - by.png>)

To filter your results by space or organization, add an `in:` filter to your query. Search for the space or organization you're interested in, and the results of your query will be scoped to the specified space or organization.

![](<../.gitbook/assets/Command Palette - s - in.png>)

## Navigation and performing space actions with quick find

Quick find also helps you navigate to settings and orgs, as well as perform certain space actions like locking and unlocking live edits, setting up Git Sync, and starting a change request.

To see the list of actions that quick find can kick off, open quick find and scroll down, or use the arrow keys to see the available options.

![](<../.gitbook/assets/Command Palette - actions.png>)

## ​Team permissions <a href="#team-permissions" id="team-permissions"></a>

Quick find is compliant with your team permission settings, meaning that users will only be able to search the content they have permission to access.‌

{% hint style="warning" %}
**Please note:** Multiple space search is not available on the public published site of a [GitBook space](../getting-started/content-structure/what-is-a-space.md). It's only available to the authenticated members of a GitBook organization based on their permission settings. External visitors of a public space can only search that space.
{% endhint %}

## ​A note on content indexing <a href="#indexation" id="indexation"></a>

We index your content by grouping it into "sections". Sections are a group of **headings** (H1, H2, or H3) with its following text. A section can be a heading with its text or just text.

When a section starts with H1 and contains a lot of H2/H3 with text, your paragraph turns into a big section. As you can see, we just show 3 lines of information in each result in the quick find results view. When your section is too big, sometimes the keyword match is hidden in a part of the section that isn't displayed in the preview. Don't worry, quick find still found matching sections\![\
](http://app.gitbook.com/@gitbook/s/gitbook-docs/\~/drafts/-Lt-3yOWRPE66HLv1wRo/primary/collaboration/conflict-resolution)
