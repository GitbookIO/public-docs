---
description: All the GitBook features, updates, improvements and fixes we released in 2022 and earlier
---

# 2022 and earlier

{% updates format="full" %}
{% update date="2022-12-15" %}
## Editor improvements, and more

We've worked on GitBook's overall editor experience, improving reliability, copy/paste from multiple sources and speedy shortcuts.

### Copy/Paste from Google Docs

Copying and pasting content from Google Docs into GitBook is now faster and more reliable, maintaining the formatting and structure of content created in Google Docs. Headings, lists, and more save their formatting as you paste them in GitBook.

* Copy/pasting from Google Docs will maintain the formatting.

### Copy/Paste from VS Code

Copying and pasting content from VS Code will now automatically paste as a code block, auto-formatting and styling your code in it's detected language.

* Code pasting from VSCode should now be more reliable.
* Pasted code in GitBook will automatically paste as a code block.

### Copy/Paste from Google Sheets and Excel

Copy and pasting content from Google Sheets and Excel now automatically creates a table for you and maintains the position of each cell, row, and column. It's also easier to work with tables.

* Copy/paste from Excel will automatically paste as a table
* Make it possible to select an entire table from its border.

### Inline palette in the editor

Adding inline images, links, emojis and others is now easier with our **inline palette**. It can be triggered by hitting `/` in the editor.

* Add inline controls shortcut `/`
* Add page linking to the inline palette

We've also made improvements to the following:

* Dropping a file on the Editor should now be more reliable.
* Improved performance and image loading.

### Fixed

Below is a list of bug fixes also included in this release:

* Fix an issue where we were not correctly calculating diffs and conflicts for text with marks.
* Fix Edit button not responding after first click.
* Fix an issue where cyclic OpenAPI schemas wouldn't generate any examples.
* Fixed an issue where unsaved content would not be shown in diff view.
* Fix re-ordering and hiding of table columns.
* Fix diff and merge of documents with images or links.
* Fix an issue where the embed would fail if the returned icon did not contain a protocol.
{% endupdate %}

{% update date="2022-11-30" %}
## Annotations, footnotes, and more

We’ve added more ways to provide contextual information for your visitors, as well as improvements to expandable blocks and several bug fixes.

### New

* You can now add inline text annotations! Easily provide useful secondary information with content blocks that expand upon clicking. It’s a handy way to provide additional context without breaking a reader’s train of thought.
* We’ve also added support for footnotes in Markdown, which are imported into GitBook as inline annotations.
* Expandable blocks now have an anchor link you can copy and paste. Additionally, we now expand a block automatically when the page is accessed. This allows you to quickly direct visitors to a specific part of your documentation.

### Improvements

* Better handling of errors in calls to our API, specifically when listing spaces.

### Fixed

* Fix an issue where heading anchors were `undefined` when target immediately after they were created.
* You can now use drag and drop to move a space to a collection that is nested inside another collection.
* When using the inline palette, it should now have the focus return to the editor after closing it.
* Fix pasting tables for certain websites.
* Fix an issue where duplicated characters are sometimes inserted when typing in code blocks.
* Fix page outlines that were too big, now they should be scrollable for viewing the entire list.
* Fix an issue where focus would be trapped in a popover when selecting math equations.
* Fix an issue where diff view would incorrectly show that text had changed if the number of words in the paragraph had changed.
{% endupdate %}

{% update date="2022-11-22" %}
## Linking pages from another space, and more

### New

* GitBook allowed you to create a link to a different space in any document you created. Now, you can go even further and link to a specific page inside that different space.

### Improvements

* We've fixed an issue where the text in a numbered list wouldn't be aligned correctly.
* We've also made some performance improvements in the editor.
{% endupdate %}

{% update date="2022-11-03" %}
## Public docs, integrations, and more

This release was an exciting one, bringing plenty of new features.

### Public docs revamp with new customization options

The **layout and styling** has been modernized!

* The search box is now located in the top-right corner on both desktop and mobile.
* Heading sizes have been improved. In general they are smaller than before, with the exception of a larger page title when viewing on a mobile device.
* Header links are right-aligned on desktop, and visible by clicking on a links menu on mobile.
* Horizontal lines associated with the page title and with other headings have been removed.

And, we've brought in a number of **new customization options** to help you better match your public docs to your own branding:

* Additional font options. Folks subscribed to our Pro and Enterprise plans now have the option to choose from Overpass, Noto Sans, IBM Plex Serif, Poppins and Fira Sans.
* Straight or rounded corners. The option defaults to rounded, but you can decide which works best for your documentation.
* Header sub-links, which are displayed as a dropdown menu.

### Integrations

We've released a *lot* of new integrations! Find out more about the integrations we offer and how to integrate them with your GitBook documentation on our website.

### Card view for tables

Card view will help you to build beautiful landing pages in GitBook. Card view is a new way to display table data, so it's possible to convert existing tables to make use of card view.

### Accessibility

These improvements aren't visible to all, but are very important for folks who use screen readers.

* Images now have an empty alt tag by default, which signals that they are purely decorative, and will therefore be ignored by screen readers. (Alt text can be added to images if you'd like!)
* We've added labels to the search box, the button that closes the table of contents on mobile, and to the link on the custom logo for a space.
* We've improved semantics for tables.

### SEO

* The page title for each page now uses the H1 tag.
* Heading 1, 2, and 3 blocks now use the H2, H3, and H4 tags, respectively.

### PDF export

Improvements have been made to the rendering of titles and page covers, and to page breaks to avoid content blocks being split across multiple pages.

### Tables

In addition to card view, we've made editing tables and their content even easier. You can now open a row to edit its content in a pop-up.

### The GitBook interface

You'll now see sub-menus for some settings within the GitBook app, for example when setting links, working with tables, setting the syntax for code blocks, moving a space, and more. This should make it even easier for you to select the options you want.

We've also made some changes to the customize screen, in line with the new customization features we've shipped.

### Bug fixes

* Previously, if a custom logo was set at the collection level, that logo was not being correctly inherited by spaces within the collection. That's resolved!
* If you invited a user to your organization via SSO, you might not have seen the SSO badge to indicate this. We've taken care of that!
* Tab blocks used to switch back to the first tab when some types of content were added to another tab. That doesn't happen any more!
* We've improved support for Grammarly in the GitBook editor.

### Final notes

We have also:

* Made some more improvements to GitBook's performance.
* Released more under-the-hood tweaks and minor bug fixes.
{% endupdate %}

{% update date="2022-09-06" %}
## Introducing organization management endpoints for the GitBook API

A new API collection is now available for managing members, invites, and teams at scale.

### API for users management

We are introducing a collection of API endpoints to automate the management of members and teams in an organization:

* `/v1/orgs/:id/members`
* `/v1/orgs/:id/invites`
* `/v1/orgs/:id/teams`
{% endupdate %}

{% update date="2022-08-12" %}
## Auto-sizing columns, and more

### Auto-sizing table columns

You can now set table columns to be a fixed size, or auto-size based on available width.

As well as some major improvements to how we handle column sizing (yes, you can now make tiny columns!) this size-to-fit option lets you have some nifty auto-layout style tables in your docs.

<details>

<summary>🐛 And don't forget the bug fixes</summary>

* Fixed an issue where guest members would not see nested content in their sidebar.
* Fixed an issue where table columns would jump when being resized.

</details>
{% endupdate %}

{% update date="2022-08-04" %}
## Code blocks, invites, and more

### Code block line highlighting

You can now highlight lines in code blocks to even-better show your readers the important stuff.

### Code wrapping on/off

It's now possible to toggle line wrapping on and off within code blocks.

### Show/hide line numbers in code blocks

You can now toggle line numbers on/off for each of your code blocks. Line numbers are **off** by default now, to match how most other tools (hi GitHub 👋) show snippets.

You can always turn line numbers on for full-file code blocks and/or where it makes sense – like tutorials!

### Better inviting for spaces and collections

It's now *way* more clear whether you'll be inviting new members as guests or 'full-fat' org members.

### Configurable default role for email domain SSO

You can now set which role you want members to have when they sign in via email domain SSO. Previously this was fixed to the **editor** role and had to be changed manually.

<details>

<summary>🐛 And don't forget the bug fixes</summary>

* Fixed an issue where syntax highlight was bugging out with multi-line comments in code blocks.
* Fixed 'heap out of memory' issues to improve Git sync.

</details>
{% endupdate %}

{% update date="2022-07-26" %}
## New Git Sync, and more

### New, more-stable git sync

After lots of tweaks, improvements and testing, we are rolling out the new Git sync v2 to all of our users.
{% endupdate %}

{% update date="2022-07-18" %}
## Slack and Segment integration, notifications, and more

### Slack & Segment Integrations

You can now integrate both Slack and Segment with GitBook, using our new integrations. We've worked hard on building out a solid integration platform, and we're super happy to release this first couple of integrations.

The Slack integration allows you to post updates to a Slack channel, and the Segment integration allows you to track various events to your own Segment install.

### Email notifications

You can now enable email notifications so you're alerted to important events like space visibility changes and change requests being submitted or merged.
{% endupdate %}

{% update date="2022-06-30" %}
## Multiple breaking changes to ownership, paths & change-requests in the GitBook API

We’ve removed the /v1/owners/:id/spaces endpoint in favor of more explicit replacements.

### Breaking: removing `/v1/owners/:id` endpoints

Endpoint `/v1/owners/:id/spaces` has been removed and replaced by:

* `/v1/orgs/:id/spaces` for an organization
* `/v1/users/:id/spaces` for a user

### Breaking: `path` and `slug` properties in pages

Page previously had only one `path` property representing the page slug in its direct page parent. Pages will now include 2 properties:

* `slug`: representing the page's slug in its direct parent
* `path`: representing the complete page's path in the revision

### Breaking: `url` path parameter for page lookup by path

Requests on page using a URL will now require a URL encoded page's path. For example the previous request:

```
GET /v1/spaces/u23h2u4hi24/content/url/a/b/c
```

should now be:

```
GET /v1/spaces/u23h2u4hi24/content/path/a%2Fb%2Fc
```

### `createChangeRequest` returns entire change-request

Previously `POST /v1/spaces/:space/change-requests` was only returning the ID of the newly created change-request.

The response will now contain the entire change-request object. A property `changeRequest` is appended for compatibility, but marked as deprecated and will be removed in the near future.
{% endupdate %}
{% endupdates %}
