---
description: >-
  Learn how the site workspace changes navigation, content structure, and
  permissions in GitBook
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: false
  actions:
    visible: true
---

# Site workspace

GitBook is organized around your docs sites. Everything in the app is arranged around the sites you publish, so what you see while editing matches what your visitors see when reading.

This page explains the workspace and what it means for your existing content.

<div data-with-frame="true"><figure><img src="../.gitbook/assets/Site workspace.png" alt="A site open in GitBook, with its sections in the sidebar"><figcaption></figcaption></figure></div>

## Why the site workspace

In the site workspace, the structure you navigate in the app matches the structure of your published site. Your organization contains sites, and every piece of content lives inside a site as a **section**. The hierarchy you edit is the hierarchy your readers get.

## How the workspace is organized

### Home shows all your sites

When you open GitBook, you land on your organization **Home**: your docs sites, recent changes, and organization-wide tools, in one place. To get back to it from anywhere, use the switcher at the top of the sidebar.

### The sidebar shows your site, not your org

Opening a site replaces the sidebar with that site’s content tree, the same structure visitors see on your published site. Navigate straight to any section and start editing without switching contexts.

The content tree in the sidebar is read-only. To reorganize your site, open the **structure editor**, a dedicated screen that replaces the **Structure** tab in **Site settings**. Changes you make there reflect back in the sidebar immediately.

### Sections replace spaces

Content in a site lives in **sections**. If you’ve used GitBook before, a section is what you knew as a space linked to a site. Sections work the same way in the editor. The change is where they live and how they inherit settings from their site.

{% hint style="info" %}
In the GitBook API, sections are still represented as `space` objects. Nothing changes for API integrations or Git Sync.
{% endhint %}

### Site tools, one click away

**Insights**, **Analytics**, **Customization**, and **Site settings** are items in the site sidebar and open in the main view.

### Draft sections

New sections start as **drafts**: linked to your site, editable by your team, but not visible to visitors. When you’re ready, publish a draft individually, or publish several at once from the structure editor.

To see how drafts will look on your site, switch the site preview between **Live** and **Live + Drafts**.

### Organization settings, in context

Organization settings open in context at the organization level, alongside your organization **Home**, so you can adjust organization-wide options without losing your place.

### Site-inherited permissions

Sections can inherit permissions from their site instead of from collections. When a member has access through more than one route, the most permissive grant applies. On Enterprise plans, sections shared across sites inherit the broadest access.

Site-inherited permissions are opt-in per section. Sections you don’t opt in keep the existing collection-based permissions.

## What happens to existing spaces and collections

Nothing is deleted or unpublished. Existing content moves as follows:

* Spaces already linked to a site become sections of that site.
* Spaces not linked to any site appear in an **All content** section, alongside your sites, in a tree view. Collections are preserved there as folders.
* If every space in your organization belongs to a site, the All content section doesn’t appear at all.
