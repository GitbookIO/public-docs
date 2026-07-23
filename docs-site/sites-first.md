---
description: >-
  Learn how the site workspace changes navigation, content structure, and
  permissions in GitBook
icon: sparkle
tags:
  - tag: beta
    primary: true
---

# Site workspace

## The sites-first workspace in GitBook

GitBook is now reorganized to be a site specific. Everything in the app is organized around the docs sites you publish, so what you see while editing matches what your visitors see when reading.

This page explains what changed, what it means for your existing content, and how to opt in.

<figure><img src="../.gitbook/assets/site-centric @2x.png" alt=""><figcaption></figcaption></figure>

### Why the site workspace

Previously, GitBook organized your work around spaces and collections, and sites were built on top by linking spaces together. That meant the structure you navigated in the app never quite matched the structure of your published site.

The site workspace closes that gap. Your organization contains sites, and every piece of content lives inside a site as a **section**. The hierarchy you edit is the hierarchy your readers get.

### What’s new

#### All Sites is your new home

When you open GitBook, you land on the **All Sites** screen: every docs site in your organization, in one place. It replaces the old Home screen as your starting point. To get back to it from anywhere, use the switcher at the top of the sidebar.

#### The sidebar shows your site, not your org

Opening a site replaces the sidebar with that site’s content tree, the same structure visitors see on your published site. Navigate straight to any section and start editing without switching contexts.

The content tree in the sidebar is read-only. To reorganize your site, open the **structure editor**, a dedicated screen that replaces the old Structure tab in Site settings. Changes you make there reflect back in the sidebar immediately.

#### Sections replace spaces

Content in a site now lives in **sections**. If you’ve used GitBook before, a section is what you knew as a space linked to a site. Sections work the same way in the editor. The change is where they live and how they inherit settings from their site.

{% hint style="warning" %}
In the GitBook API, sections are still represented as `space` objects. Nothing changes for API integrations or Git Sync.
{% endhint %}

#### Site tools, one click away

Insights, Analytics, Customization, and Site settings are now items in the site sidebar and open in the main view. You no longer need to dig through nested settings to find them. The screens themselves work exactly as before.

#### Draft sections

New sections start as **drafts**: linked to your site, editable by your team, but not visible to visitors. When you’re ready, publish a draft individually, or publish several at once from the structure editor.

To see how drafts will look on your site, switch the site preview between **Live** and **Live + Drafts**.

#### Organization settings, in context

Organization settings no longer take over the whole screen. They open in context at the organization level, alongside the All Sites screen, so you can adjust organization-wide options without losing your place.

#### Site-inherited permissions

Sections can inherit permissions from their site instead of from collections. When a member has access through more than one route, the most permissive grant applies. On Enterprise plans, sections shared across sites inherit the broadest access.

This is opt-in per space. Content you don’t opt in keeps the existing collection-based permissions.

### What happens to existing spaces and collections

Nothing is deleted or unpublished.

* Spaces already linked to a site become sections of that site.
* Spaces not linked to any site appear in a new **All content** section, alongside your sites, in the familiar tree view. Collections are preserved there as folders.
* If every space in your organization belongs to a site, the All content section doesn’t appear at all.

### How the rollout works

The site workspace is rolling out in phases. When it’s available for your organization, you’ll see an option to switch on the new experience, along with a short in-app tour of what moved where.
