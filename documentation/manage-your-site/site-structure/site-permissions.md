---
description: >-
  What each role can do when managing a site's structure, settings, and
  publishing
---

# Site permissions

Your [role](../../collaborate/member-management/roles.md) on a site determines what you can do when working with it — from browsing its content to changing its structure, settings, and publishing. This page covers what each role unlocks for managing a site. For how a member ends up with a given role on a site, see [permissions and inheritance](../../collaborate/member-management/permissions-and-inheritance.md).

### What each role unlocks on a site

{% hint style="info" %}
Each role includes everything the roles below it can do.
{% endhint %}

<table><thead><tr><th width="171.3333740234375">Role</th><th>Can do</th></tr></thead><tbody><tr><td><strong>Admin</strong></td><td>Everything: site settings, publishing, members, billing, integrations</td></tr><tr><td><strong>Creator</strong></td><td>Restructure the site: add, publish, rename, reorder, and delete sections and variants</td></tr><tr><td><strong>Reviewer</strong></td><td>Merge change requests — publishing their content to the live site</td></tr><tr><td><strong>Editor</strong></td><td>Edit page content in change requests, submit them for review, add <strong>draft</strong> sections and variants</td></tr><tr><td><strong>Commenter</strong></td><td>Read content and leave comments</td></tr><tr><td><strong>Reader</strong></td><td>Read-only access</td></tr></tbody></table>

#### Admin — full control

Admin is required for anything that affects the site as a whole rather than a single piece of its content:

* Site settings — title, visibility, custom domain, default section or variant.
* Publishing and unpublishing the site.
* Site-wide branding and customization, as opposed to a single variant's override.
* Managing members and teams on the site, including role overrides.
* Installing and configuring integrations, including MCP servers.
* Managing redirects, share links, and the site's private-site authentication.
* Configuring the AI assistant, its knowledge sources, and feedback channels.
* Site billing and plan.

If an action changes something every reader or every editor is affected by — not just one page or one section — it requires admin permissions.

{% hint style="warning" %}
Organization admins always have site Admin on every site in the organization, regardless of any per-site role settings. There's no way to give an org admin a lower role on a specific site.
{% endhint %}

#### Creator — shaping the site

Creator unlocks control over the site's structure — the sections, section groups, and variants that make up its table of contents:

* Add a section, variant, or group directly as **published** content, not just drafts.
* Publish a draft that an editor created, or turn published content back into a draft.
* Rename, reorder, and move sections, groups, and variants.
* Delete a section or variant.
* Customize an individual variant's branding overrides, such as its title.

In short, a creator can fully rebuild how a site is organized without needing site-wide administrative access.

#### Reviewer — merging content changes

Reviewer adds one capability on top of Editor: **merging change requests**, which publishes their content straight to the live site. This makes Reviewer the first role that can actually change published content, even though it can't touch the site's structure or settings.

{% hint style="info" %}
Merge access is defined per space, not per site — it's the same Reviewer role, applied to whichever spaces make up the site. A member only needs Reviewer to merge; they don't need to be the one who opened the change request.
{% endhint %}

#### Editor — day-to-day content work

Editor is the entry point for making changes. An editor can:

* Edit page content by submitting a change request, the same as in any space. This doesn't go live immediately — the change stays as a proposal until someone with Reviewer access or above merges it.
* Add a new section or variant to the site's structure — but only as a **draft**. Draft content isn't visible on the published site until someone with Creator access or above publishes it.
* Resolve findings surfaced by GitBook's AI content-quality scans.

An editor cannot merge their own or anyone else's change request — that requires Reviewer access or above.

{% hint style="info" %}
Letting editors add draft structure — without letting them publish it — means a writer can stage a new section or variant for review without accidentally changing what readers see.
{% endhint %}

#### Commenter — browsing and commenting

Commenter includes Reader access and adds the ability to leave comments. Neither role can change site content or settings.

#### Reader — browsing

Reader access lets you open a site in the dashboard, browse its structure, and read published content.

### Where to manage this

A site's members, their roles, and its default permission level are managed from **Site settings → Members**, by anyone with Admin access to the site. See [permissions and inheritance](../../collaborate/member-management/permissions-and-inheritance.md) for how that default, team access, and direct member overrides combine to decide a member's role.
