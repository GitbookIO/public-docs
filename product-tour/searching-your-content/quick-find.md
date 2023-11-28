---
description: Learn how to seamlessly search and navigate your documentation
---

# Quick find

GitBook’s quick find command palette lets you search for – and quickly navigate between – all your content, as well as perform common space actions.

{% hint style="info" %}
**Permissions**

All [member roles](../../account-management/member-management/roles.md) can use quick find, but members will only be able to search the content they have permission to access.‌
{% endhint %}

## How to use Quick find

When writing or reading documentation you’ll want to find whatever you need quickly, wherever it’s located. Use our quick find command palette to search and navigate across all your content.

{% hint style="success" %}
**​**You can open the quick find palette by pressing **CMD + K** on Mac or **Ctrl + K** on Windows
{% endhint %}

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Quick find.png" alt="Open Quick find palette, which you to type in command or search a specific term"><figcaption><p>The quick find command palette</p></figcaption></figure>

</div>

## Display of results <a href="#display-of-results" id="display-of-results"></a>

Results of the space you’re in are displayed first, followed by results from other spaces from the organization you’re currently editing in, **as well as other organizations** you are a member of.

So type in what you need, take a look at results in other spaces, and pick the page or section you’re interested in.

When you select a search result from an organization, you will switch to browsing that organization. To go back, use quick find to select a document in the organization you were in before, or use the organization switcher in the sidebar.

{% hint style="info" %}
We do not currently support the ability to prioritize certain content in Quick find results.
{% endhint %}

## Navigation and performing space actions with Quick find

Quick find also helps you navigate to settings and organizations, as well as perform certain space actions like locking and unlocking [live edits](../../collaboration/collaboration/live-edits.md), setting up [Git Sync](../../integrations/git-sync/), and starting a [change request](../../collaboration/collaboration/change-requests.md).

To see the list of actions that Quick find can kick off, open Quick find and scroll down, or use the arrow keys to see the available options.

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Actions with quick find.png" alt="Open Quick find palette scrolled down to navigation and actions options. The actions allow you to move spaces, lock and unlock edits and many more."><figcaption></figcaption></figure>

</div>

## ​Team permissions <a href="#team-permissions" id="team-permissions"></a>

Quick find is compliant with your team’s permission settings, meaning that users will only be able to search the content they have permission to access.‌

{% hint style="warning" %}
**Please note:** Multiple space search is _not_ available when viewing a published [GitBook space](../../content-creation/content-structure/what-is-a-space.md) via its public URL. It’s only available to logged-in members of a GitBook organization while they view the space in the GitBook app, based on their permission settings. External visitors of a public space can only search that space.
{% endhint %}

## ​A note on content indexing <a href="#indexation" id="indexation"></a>

We index your content by grouping it into sections. Sections are **headings** (H1, H2, or H3) with the content that follows it.

When a section starts with H1 and contains a lot of H2/H3 text, your paragraph turns into a big section. We just show 3 lines of information in each result in the quick find results view. When your section is too big, sometimes the keyword match is hidden in a part of the section that isn’t displayed in the preview. Don’t worry, Quick find still found matching sections!
