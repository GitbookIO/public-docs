---
description: Reference for roles, what they can do, and how permissions inherit.
---

# Roles, permissions, and inheritance

When you add a member to your organization, you give them a default role. That role applies to any content that inherits its permissions from the organization — understanding roles is key to getting the most out of GitBook's permission management.

{% hint style="warning" %}
Regardless of role, every member counts toward your organization's total member count for billing purposes. See [Invite and manage members](invite-and-manage-members.md).
{% endhint %}

## Roles in GitBook

Each role gets progressively more access than the one before it, starting from the lowest:

<details>

<summary>Guest</summary>

Guests have no default organization role — they only ever see content they've been directly added to. This is ideal for external stakeholders or contractors you don't want to give any default access.

{% hint style="warning" %}
Guest members count toward your organization's total member count for billing purposes.
{% endhint %}

</details>

<details>

<summary>Reader</summary>

The most basic role — read-only access.

{% hint style="info" %}
Reader seats are paid on all plans.
{% endhint %}

</details>

<details>

<summary>Commenter</summary>

Same read-only access as Reader, plus the ability to leave comments on content and spaces — see [Comments and live editing](comments-and-live-editing.md).

{% hint style="info" %}
This role is available on Premium and Ultimate plans.
{% endhint %}

</details>

<details>

<summary>Editor</summary>

Can read and comment like a Commenter, and can also edit content: directly, in spaces open for [live edits](comments-and-live-editing.md), or by creating and submitting [change requests](change-requests/README.md) in spaces with live edits locked. Editors can't merge change requests.

</details>

<details>

<summary>Reviewer</summary>

Everything an Editor can do, plus merging their own and others' change requests.

{% hint style="info" %}
This role is available on Premium and Ultimate plans.
{% endhint %}

</details>

<details>

<summary>Creator</summary>

Content-level admin: everything a Reviewer can do, plus creating and deleting spaces, collections, and sites, and managing permissions at a content level.

{% hint style="info" %}
A Creator who's also a Creator or Admin in another GitBook organization can move content between organizations — see [Content structure](../creating-content/content-structure.md).
{% endhint %}

</details>

<details>

<summary>Admin</summary>

A super-user for the organization, with full access — set someone as Admin if you're comfortable with them affecting billing, managing members, and controlling every area of the organization.

{% hint style="info" %}
An Admin who's also a Creator or Admin in another GitBook organization can move content between organizations — see [Content structure](../creating-content/content-structure.md).
{% endhint %}

</details>

### Roles on a docs site

At the site level, only Administrators can change site settings. Every other role can still contribute to and edit content in the spaces they have access to — they just can't manage the site itself.

| Permission level | Permissions on the site |
|---|---|
| Administrator | Edit and view |
| Creator | View |
| Reviewer | View |
| Editor | View |
| Commenter | View |
| Reader | View |
| No access | Cannot view |

### Reader role vs. public docs reader

| | Reader role (organization) | Public docs reader (site visitor) |
|---|---|---|
| Invitation required | Yes | No |
| Paid seat | Yes | No |
| Content access | Published and unpublished (with permission) | Published only |

## Permissions and inheritance

GitBook's permission model is **role-based** and **cascading** — you set defaults, then decide at any level of content whether to inherit them or override them. You can set permissions at four levels: **organization**, **site**, **collection**, and **space**.

### Organization default roles

The default role you set for a member (above) applies to any content that inherits its permissions from the organization.

### How permissions cascade

Permissions resolve by **precedence**, not by the highest role across every level. For spaces in inherited mode, GitBook resolves access in this order:

1. **Space** — direct member and team overrides on the space
2. **Site** — permissions from the parent site
3. **Collection** — permissions from the parent collection, if there is one
4. **Organization** — the member's default role

So site permissions override organization and parent-collection defaults for linked spaces in inherited mode — but a direct space-level override still wins over everything else.

<details>

<summary>Example 1</summary>

A member has a Creator role at the organization level. A linked space is in inherited mode, and the parent site sets that member to Commenter. The member gets Commenter access in that space, because the site takes precedence over the organization default.

</details>

<details>

<summary>Example 2</summary>

A collection sets a space to Reader, and the parent site sets it to Commenter. The space uses Commenter, because site permissions take precedence over the parent collection in inherited mode. Give one member direct Creator access on the space, and that direct override wins for them specifically.

</details>

{% hint style="info" %}
Site permissions only apply to spaces in inherited mode. A space with its own permissions configured (not inherited) ignores site-level permissions entirely.
{% endhint %}

### Managing inheritance

Any time you create a collection or space, you choose how it handles inheritance:

**Inherit** — the space or collection inherits roles from its parent (the organization, for top-level content; the parent collection, for nested content). When a linked space stays in inherited mode, GitBook resolves access as described above: direct overrides, then site, then collection, then organization.

**Specific role access** — choosing a specific role resets the organization defaults and assigns every non-admin that role within the collection or space. For example, setting a space to Reader gives everyone read-only access there, regardless of their organization-level role. Direct member or team access can still override this, and once a space has a specific role set, it's no longer in inherited mode — so site permissions don't affect it.

**No access** — revokes access for all non-admin members at that space or collection, hiding it from everyone except admins and its creator.

{% hint style="info" %}
New spaces and collections default to **Inherit**.
{% endhint %}

### Setting content-specific permissions

Once you've set a space or collection's inheritance, refine access further with direct access for teams or members.

**Team access** — add a team directly to a collection or space with a specific role, giving everyone on that team the specified access. As people join or leave the team, they gain or lose that access automatically.

**Member access** — the most granular option. Giving an individual member direct access overrides any inherited permissions for them specifically, removing them from the inheritance pattern entirely — their role is explicit and unaffected by org, site, or collection-level permissions.

### Keeping on top of permissions

**Set and forget** — invite people, set their default role, and let new content inherit it. Most teams never need to go further than this.

**Control over access and workflow** — larger organizations, or teams that split into discrete collections with specific workflows, get real value from combining inheritance, overrides, and direct team/member access to build the access model they need.
