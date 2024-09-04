---
description: Learn about the UI and how to navigate pages in GitBook.
---

# Navigation

GitBook is split into different sections to make it easier to organize and manage the content you create. Read on to learn more about these sections, and how they help you build an organized and easily searchable content structure.

### The sidebar

<figure><img src="../../.gitbook/assets/editor-sidebar.png" alt=""><figcaption><p>The GitBook sidebar holds all of your documentation, as well as notifications, the search bar, snippets and more.</p></figcaption></figure>

The sidebar allows you to see and overview of your GitBook organization at a glance. The sidebar contains:

* **Organization switcher**\
  If you’re a part of multiple organizations, you can see and switch between them here. You can also create a new organization from this menu.
* **Notifications**\
  When you’re tagged in a comment or conversation, or when there is important activity in a space you’re working in, you’ll get a [notification](../../collaboration/notifications.md) to show you what’s new.
* **Ask or search**\
  Powered by [GitBook AI](../searching-your-content/gitbook-ai.md), you can ask questions in natural language, or search through the different spaces and content in your organization.
* **Home**\
  The Home page allows you to see everything your team is working on at a glance. View open change requests, discussions and comments, recent page edits and more.
* **Docs sites**\
  The overview page for the docs sites you have created in your organization.
* **Snippets**\
  With [snippets](../../snippets/snippets-beta.md), you can capture complex information from third-party tools. GitBook AI extracts that valuable knowledge within, and documents it for you in seconds.
* **Integrations**\
  GitBook [integrations](broken-reference/) supercharge your content, allowing you to embed more into your pages, or add information to your knowledge base from other apps. Head to the [integration listing page ](../../integrations/third-party-integrations.md)to see all the available integrations.
* **Docs Sites**\
  The [docs sites](../../published-documentation/publish-your-content-as-a-docs-site/) section is where you'll find any docs sites you've created.
* **Spaces**\
  The spaces section is where you’ll find the [collections](content-structure/what-is-a-collection.md) and [spaces](content-structure/what-is-a-space.md) you create when adding more content. Head to our [content structure](content-structure/) section to find out more.
* **Settings**\
  You’ll find [personal settings](../../account-management/account-settings.md) and [organization settings](../../account-management/organization-management.md) at the bottom of the sidebar. Here, you can also toggle light/dark mode, or get help from our support team if needed.
* **Trash**\
  Deleted spaces appear in the trash. You can restore them for up to seven days — after that, they’re permanently deleted.

### Table of contents

<figure><img src="../../.gitbook/assets/editor-toc.png" alt=""><figcaption><p>The table of contents lists all the pages and links in your selected space.</p></figcaption></figure>

The table of contents is a list of [pages, links, and groups](content-structure/content-in-a-space.md#organizing-your-content) that make up a space. You’ll find it to the right of the sidebar. It’s specific to the space you’re currently viewing.

From the table of contents you can:

* create new [pages](navigation.md#pages) and subpages
* create [page groups](navigation.md#groups)
* add [external links](navigation.md#external-links)
* [import external docs](../import.md) like websites or Markdown files
* access [the Actions menu](navigation.md#the-actions-menu) <img src="../../.gitbook/assets/Actions menu.png" alt="Three vertical dots" data-size="line"> for individual pages.

If you want to give more focus to the content of your page, you can temporarily hide the table of contents by hovering your cursor next to it and clicking the **Hide** button <img src="../../.gitbook/assets/Hide button.png" alt="The &#x27;hide&#x27; icon" data-size="line"> that appears. To make it appear again, hover your cursor near the edge of the page and click the **Show** button <img src="../../.gitbook/assets/Show button.png" alt="The &#x27;show&#x27; icon" data-size="line">.

### Space Overview & Space Header

<figure><img src="../../.gitbook/assets/editor-space-header.png" alt=""><figcaption><p>The space header sits at the top of the editor, and offers options that apply to the whole space.</p></figcaption></figure>

The space overview contains information about the space you’re currently viewing. It lets you do things like [publish and share](../../published-documentation/overview.md) your space, configure [GitHub or GitLab sync](../../integrations/git-sync/), and more.

{% hint style="info" %}
The space overview & space header may look different depending on the mode you’re currently in. See [change requests](change-requests.md) for more info.
{% endhint %}

#### Space overview

The space overview appears at the top of GitBook when viewing a space. It includes:

* **The space's breadcrumb**\
  The collection or docs site the space lives in.
* **Collaborators**\
  The avatar of anyone else who’s currently viewing a page in your space, with colored circles to show their cursor color. Click an avatar to jump to the page they’re currently viewing.
* **Git Sync configuration**\
  The [GitHub and GitLab Sync](../../integrations/git-sync/) configuration for your space.
* **The Share menu**\
  Allows you to publish and share your space. You can also invite others to [collaborate](broken-reference/) through this menu.
* **Actions menu** <img src="../../.gitbook/assets/Actions menu.png" alt="" data-size="line">\
  Offers a list of actions for your space. Similar to [page actions](navigation.md#the-actions-menu), the available actions for a space will differ depending on the mode you’re currently in.

#### Space Header

The space sub-navigation is located directly beneath the space header, and lets you collaborate with others on your space, customize it’s look, and more. It includes:

* **The space emoji**\
  You can choose an emoji for your space, to help you easily identify it in the sidebar.
* **The space name**\
  The name of the space that will appear in the sidebar, and your documentation if and when you choose to publish it.
* **Comments**\
  See the [comments and discussions](../../collaboration/comments-discussion.md) you and your team have had about the space content.
* **Broken Links**\
  Any [broken links](../broken-links.md) that have been found in the current space or change request.
* **Change requests**\
  Create, update, and delete [change requests](change-requests.md) in your space.
* **The edit button**\
  If your space is published, or someone has locked[ live edits](live-edits.md), the **Edit** button will appear in the space header. It lets you start a new [change request](change-requests.md) to edit content.

### Content editor

The editor is the main part of your space, where you can write or insert content in GitBook.

In addition to the multiple [content blocks](../blocks/) you can insert, you can also [embed content](../blocks/embed-a-url.md) from other places, such as [integrations](../../integrations/third-party-integrations.md).

### Page title and description <a href="#page-title" id="page-title"></a>

At the top of each page you can set a **title**, add an optional **emoji**, and write a **description**. The title you use will appear in the table of contents, and forms your page’s URL slug when published.

Your page description can be a maximum of 200 characters long, and will act as the preview text for your page in search engines.

{% hint style="info" %}
You can change the URL slug for a page by choosing **Page Actions** <img src="../../.gitbook/assets/Actions menu.png" alt="Actions menu.png" data-size="line"> > **Rename**. Find out more about [Page Actions](navigation.md#page-options) below.
{% endhint %}

### The Actions menu

The page’s Actions menu <img src="../../.gitbook/assets/Actions menu.png" alt="Three vertical dots" data-size="line"> allows you to do things like duplicate, rename or delete your page.

You can open the Actions menu using the <img src="../../.gitbook/assets/Actions menu.png" alt="three vertical dots" data-size="line"> icon that appears when hovering over your page in the sidebar, or from the icon next to the page title.

{% hint style="info" %}
The type of actions available will depend on whether you’re in live editing mode, a change request, or in a space with [locked edits](live-edits.md).
{% endhint %}

### Page options

<figure><img src="../../.gitbook/assets/editor-page-options.png" alt=""><figcaption><p>The <strong>Page options</strong> side panel offers customization options for your documentation and navigation.</p></figcaption></figure>

With [page options](../../published-documentation/customization/page-layouts.md), you to customize your documentation layout and navigation. You can only access page options if you’re in an editing mode.

You can open the **Page options** side panel by opening the page’s **Action menu** <img src="../../.gitbook/assets/Actions menu.png" alt="Three vertical dots" data-size="line"> and choosing **Options**, or by hovering over the main title of the page and clicking **Page options** when it appears.

{% hint style="info" %}
Certain changes, such as disabling the table of content, only apply to published documentation and may not be visible in the editor.
{% endhint %}

### Page outline

<figure><img src="../../.gitbook/assets/editor-page-outline.png" alt=""><figcaption><p>The page outline shows H1 and H2 headings, allowing you to quickly jump to a specific section on an individual page.</p></figcaption></figure>

The **page outline** sits on the right-hand side of the editor, and makes it easy to jump directly to the section of the page you’re looking for.

Any [Heading 1 or Heading 2 blocks](../blocks/heading.md) you add to the page will appear in the page outline listed here.

The page outline will appear in your published site, too. You can toggle it on or off in the [**Page options**](navigation.md#page-options) side panel.

{% hint style="info" %}
If you can’t see the right-hand column of the app, it may be because your browser window is less than 1430 pixels wide. Your browser window needs to be at least 1430 pixels wide to see and use the page outline.
{% endhint %}
