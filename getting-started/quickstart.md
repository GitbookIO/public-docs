---
description: Get up and running in GitBook and publish your first docs site in minutes
icon: bolt
---

# Quickstart

This quickstart guide explains how to get set up in GitBook and publish your first docs site in minutes.

At the end of this guide, you’ll have a live documentation site, ready to expand and customize.

{% stepper %}
{% step %}
#### Create your account

[Create an account](https://app.gitbook.com/join) to get started with your first documentation site.
{% endstep %}

{% step %}
#### Create your first site

1. From the **All Sites** screen, click the **+** next to **Sites** in the sidebar.
2. Give your site a name your visitors will recognize.
3. Click **Create**.
{% endstep %}

{% step %}
#### Choose how you want to start

GitBook welcomes you to your new site and asks how you'd like to begin.

<table><thead><tr><th width="200">Starting point</th><th>Best for</th></tr></thead><tbody><tr><td><strong>Docs template</strong></td><td>Starting from a ready-made documentation layout with placeholder sections — the fastest way to see a full site working.</td></tr><tr><td><strong>Import</strong></td><td>Bringing in existing content from online docs, Markdown, or HTML.</td></tr><tr><td><strong>OpenAPI</strong></td><td>Generating interactive API reference docs from an OpenAPI spec.</td></tr><tr><td><strong>Blank</strong></td><td>Starting from an empty section and building from scratch.</td></tr><tr><td><strong>Sync with Git</strong></td><td>Keeping your docs in sync with a GitHub or GitLab repository.</td></tr></tbody></table>

Or, you can pick from your organization's existing content if you already have some work in GitBook.

This guide follows the template path:

1. Click **Docs template** and review the preview.
2. Click **Use Docs Template** to apply it.
{% endstep %}

{% step %}
#### Explore your new site

Your site opens unpublished, so you can edit, customize, and preview everything before it goes live. The sidebar shows:

<table><thead><tr><th width="160">Sidebar area</th><th>What you'll find</th></tr></thead><tbody><tr><td><strong>Site header</strong></td><td>Your site name, its publish status, and the <strong>Preview</strong> and <strong>Publish</strong> buttons.</td></tr><tr><td><strong>General</strong></td><td><strong>Overview</strong>, <strong>Change requests</strong>, <strong>Site structure</strong>, and <strong>Settings</strong>.</td></tr><tr><td><strong>Tools</strong></td><td><strong>Styleguide</strong>, <strong>Customize</strong>, <strong>Analyze</strong>, and <strong>Extend</strong>.</td></tr><tr><td><strong>Content</strong></td><td>These are your site's sections - for the Docs template: Home, Documentation, API Reference, Changelog, and Help Center. Use the icons on the <strong>Content</strong> header to find, rename, and add sections.</td></tr></tbody></table>

{% hint style="success" %}
Your content isn't published yet — so you can edit, customize, and preview your docs site before making it live. Click **Publish** to make it live immediately.

<i class="fa-arrow-down">:arrow-down:</i> [Jump to the 'Publish your documentation' step on this page](quickstart.md#publish-your-documentation)
{% endhint %}
{% endstep %}

{% step %}
#### Edit your content

The Docs template starts you with placeholder sections in the **Content** part of the sidebar. Click any section to open it and see its placeholder content.

There are two ways to edit and update your content in GitBook — in our visual editor, or following a docs-as-code workflow. **You can choose one, or use a combination of both.** Whichever workflow you prefer, you'll edit your content using a **branch-based editing flow**. Find out more on [the Concepts page](../resources/concepts.md).

{% tabs %}
{% tab title="Visual editor" %}
GitBook's what-you-see-is-what-you-get (WYSIWYG) editor lets you edit content visually, drag content blocks to reorganize them, and see how your content looks as you work. It's ideal if you don't want to work in a code editor, or you're used to tools like Notion or Google Docs.

**Edit your docs in a change request**

1. In the **Content** section of the sidebar, click a section — such as Documentation — to open it.
2. Click **Edit** in the top-right corner. This opens a change request where you can change the content of the section.
3. Click **Add new…** > **Page** in the table of contents on the left-hand side.
4. Give your new page a title.

**Preview your changes**

Along the top of the web app you'll see tabs for **Editor**, **Changes**, and **Preview**. These switch between different views for your content. Click **Preview** to see how your docs site looks with all the changes in your change request, on both desktop and mobile.

**Merge your changes**

Once you're happy with your changes, click the **Merge** button in the top-right corner. This updates the primary version of your content with all the edits from the change request. If the content is part of a live docs site, the site updates immediately.
{% endtab %}

{% tab title="Docs as code" %}
Sync your documentation with a GitHub or GitLab repository to enable code-based editing in your existing developer environment. It's ideal for technical users who prefer to manage documentation alongside other code.

**Set up Git Sync**

1. Open the section you want to sync from the **Content** part of the sidebar.
2. Click the Git Sync indicator's **Set up** button in the top bar.
3. Follow the instructions to sync the section to your chosen Git repository. Head to the [Git Sync pages](git-sync/) to find out more.

**Edit your docs from your developer environment**

Once you've synced your section to your Git repository:

1. Open the repository.
2. Create a pull request.
3. Make the changes you want.

{% hint style="info" %}
GitBook supports [Markdown editing](../creating-content/formatting/markdown.md), so you can create and format content using common syntax.

Every standard block in GitBook can be written and formatted using Markdown.
{% endhint %}

**Preview your changes**

You can [preview your changes](git-sync/github-pull-request-preview.md) on your published docs site from the pull request in GitHub or GitLab. Your pull request shows a status with a unique preview URL. Click **Details** on that status to open it and see how your site looks once merged.

**Merge your changes**

Merge your pull request and your content updates both in the GitBook app and on your docs site, if it's live. In the GitBook app, every commit and your merged pull request sync to your section as updates in the version history.
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
#### Customize your docs

**Organize your site navigation**

Add more content to your site — an API reference, a help center, a changelog — at any time, and organize your site's navigation bar so visitors find what they're looking for. Head to [Site structure](../docs-site/site-structure/) to learn about sections, groups, and variants.

**Customize the look and feel**

Your site looks great out of the box — and under **Customize**, you can set your own [logo, colors, and font](../docs-site/customization/icons-colors-and-themes.md), adjust the layout, and update your [site's visibility](../docs-site/site-settings.md#audience).
{% endstep %}

{% step %}
#### Publish your documentation <a href="#publish-your-documentation" id="publish-your-documentation"></a>

You can publish your site with a click at any time.

1. Open your site from the **All Sites** screen.
2. Click **Publish** in the site header.

Once your site is live, the **Overview** screen updates with a link to the live site.

{% hint style="success" %}
Want to explore publishing in more detail? Check out [our complete guide to creating and publishing content in GitBook](https://app.gitbook.com/s/LBGJKQic7BQYBXmVSjy0/editing-and-publishing-documentation/complete-guide-to-publishing-docs-gitbook).
{% endhint %}
{% endstep %}
{% endstepper %}

#### Add a custom domain

By default, your site is published with a unique URL in this format:

{% code title="Your site’s default URL" %}
```
https://[organization-name].gitbook.io/[site-title]
```
{% endcode %}

While this may be suitable for some teams, many choose to change their URL to [a custom domain](../docs-site/custom-domain/) or [a custom subdirectory](../docs-site/custom-domain/setting-a-custom-subdirectory/).

1. Expand **Settings** in your site's sidebar.
2. Click **Domain and URL**.
3. Choose the option you want.
4. Follow the instructions to configure the DNS settings with your domain provider.

{% hint style="info" %}
It can take up to 48 hours for your DNS changes to take effect — although they typically propagate much faster.
{% endhint %}

#### Next steps

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-type="image">Cover image (dark)</th><th data-hidden data-card-cover-dark data-type="image">Cover image (dark)</th></tr></thead><tbody><tr><td><strong>Invite your team to collaborate</strong></td><td>Add team members to your organization and set permissions</td><td><a href="../.gitbook/assets/25_12_10_invite_your_team_to_collaborate_1.png">25_12_10_invite_your_team_to_collaborate_1.png</a></td><td><a href="../collaboration/member-management/invite-members-to-your-organization.md">invite-members-to-your-organization.md</a></td><td><a href="../.gitbook/assets/25_12_10_invite_your_team_to_collaborate.png">25_12_10_invite_your_team_to_collaborate.png</a></td><td><a href="../.gitbook/assets/25_12_10_invite_your_team_to_collaborate.png">25_12_10_invite_your_team_to_collaborate.png</a></td><td></td><td></td><td></td></tr><tr><td><strong>Change site visibility</strong></td><td>Control who can see your content with share links and authenticated access</td><td><a href="../.gitbook/assets/25_12_10_change_site_visibility_1.png">25_12_10_change_site_visibility_1.png</a></td><td><a href="../docs-site/publish-a-docs-site/#publish-a-docs-site">#publish-a-docs-site</a></td><td><a href="../.gitbook/assets/25_12_10_change_site_visibility.png">25_12_10_change_site_visibility.png</a></td><td></td><td><a href="../.gitbook/assets/25_12_10_change_site_visibility.png">25_12_10_change_site_visibility.png</a></td><td><a href="../.gitbook/assets/25_12_10_change_site_visibility.png">25_12_10_change_site_visibility.png</a></td><td></td></tr><tr><td><strong>Add auto-translations</strong></td><td>Create one-click translations that update automatically</td><td><a href="../.gitbook/assets/25_12_10_add_auto_translations_1.png">25_12_10_add_auto_translations_1.png</a></td><td><a href="../docs-site/site-settings.md">site-settings.md</a></td><td><a href="../.gitbook/assets/25_12_10_add_auto_translations.png">25_12_10_add_auto_translations.png</a></td><td></td><td></td><td><a href="../.gitbook/assets/25_12_10_add_auto_translations.png">25_12_10_add_auto_translations.png</a></td><td></td></tr><tr><td><strong>Install integrations</strong></td><td>Integrate with your stack and extend functionality with powerful integrations</td><td><a href="../.gitbook/assets/25_12_10_install_integrations_1.png">25_12_10_install_integrations_1.png</a></td><td><a href="https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/integrations">Integrations</a></td><td><a href="../.gitbook/assets/25_12_10_install_integrations.png">25_12_10_install_integrations.png</a></td><td></td><td></td><td></td><td><a href="../.gitbook/assets/25_12_10_install_integrations.png">25_12_10_install_integrations.png</a></td></tr><tr><td><strong>Add an API reference</strong></td><td>Create auto-updating, interactive API reference docs from an API spec</td><td><a href="../.gitbook/assets/25_12_10_add_an_api_reference_1.png">25_12_10_add_an_api_reference_1.png</a></td><td><a href="https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/api-references">Document an API</a></td><td><a href="../.gitbook/assets/25_12_10_add_an_api_reference.png">25_12_10_add_an_api_reference.png</a></td><td></td><td></td><td></td><td></td></tr><tr><td><strong>Track docs analytics</strong></td><td>Use the built-in insights to measure success and understand user behavior</td><td><a href="../.gitbook/assets/25_12_10_track_docs_analytics_1.png">25_12_10_track_docs_analytics_1.png</a></td><td><a href="../docs-site/insights.md">insights.md</a></td><td><a href="../.gitbook/assets/25_12_10_track_docs_analytics.png">25_12_10_track_docs_analytics.png</a></td><td></td><td></td><td></td><td></td></tr></tbody></table>
