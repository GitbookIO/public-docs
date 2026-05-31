---
description: >-
  Understand how permissions work in GitBook and how to control who can access
  and edit your content
---

# Permissions and inheritance

GitBook has a flexible permissions model that lets you have as much, or as little, control over permissions as you need. The permission model in GitBook is a [**role-based**](roles.md#roles-in-gitbook)**, cascading** model. This means that you set defaults and then, at any level of content, decide whether to inherit those defaults or not.

You can set permissions at four levels: **organization**, **site**, **collection**, and **space**.

### Organization default roles

When you add a member to your organization, you set [their default role](roles.md). This role applies to any piece of content that inherits its permissions from the organization defaults.

### How permissions cascade

Permissions in GitBook resolve by **precedence**, not by the highest role across every level.

For spaces in inherited mode, GitBook resolves access in this order:

* **Space** — direct member and team overrides on the space
* **Site** — permissions from the parent site
* **Collection** — permissions from the parent collection, if there is one
* **Organization** — the default role set for each member

This means site permissions override organization defaults and parent collection defaults for linked spaces in inherited mode. Direct space-level overrides still take precedence over everything else.

Here are two examples of how this works in practice:

<details>

<summary><strong>Example 1</strong></summary>

A member has a Creator role at the organization level. A linked space is in inherited mode, and the parent site sets that member to Commenter. The member gets Commenter access in that space, because the site takes precedence over the organization default.

</details>

<details>

<summary><strong>Example 2</strong></summary>

A collection sets a space to Reader, and the parent site sets it to Commenter. The space uses Commenter, because site permissions take precedence over the parent collection in inherited mode. If you then give one member direct Creator access on the space, that direct override wins for that member.

</details>

{% hint style="info" %}
**Note:** Site permissions only apply to spaces in inherited mode. If a space has its own permissions configured — meaning it is not in inherited mode — those take precedence and site-level permissions will not affect it.
{% endhint %}

### Managing inheritance

Any time you create a collection or a space, you’ll be able to set the type of inheritance you want. You have three broad options when setting the inheritance for a piece of content:

### Inherit

Setting the inheritance to **inherit** will make the space or collection inherit the roles assigned in the **parent level content**. For top-level spaces or collections, this parent is the organization, so they would inherit the organization default roles. For spaces or sub-collections inside a collection, the parent will be the collection the content sits within.

When a space is linked to a site and stays in inherited mode, GitBook resolves access in this order: direct space overrides, then the parent site, then the parent collection, and finally the organization. Site permissions take precedence over organization and collection defaults, but they do not change direct space-level overrides.

### Specific role access

Selecting a specific role when setting a collection or space’s permission inheritance will **reset** the organization default roles and assign every **non-admin** to that role within the collection or space. For example, if you set the inheritance to **reader**, everyone in the organization would have read-only access to the space or collection, regardless of their default role.

Direct member or team access on that collection or space can still override this inherited setting. If you set a specific role on the space itself, the space is no longer using inherited mode, so site permissions do not affect it.

### No access

You can also completely revoke access for any non-admin organization members at a space or collection level. This will hide the content from everyone except for admins and whomever created the space or collection.

{% hint style="info" %}
The default inheritance option for any newly-created space or collection is **inherit**. This means that whenever a piece of content is created, it’ll inherit permissions from its parent by default.
{% endhint %}

### Setting content specific permissions

Once you’ve decided on the permission inheritance for your space or collection, you can further customise access by giving teams or members **direct access**.

### Giving a team direct access

You can add a team directly to a collection or space with a specific role. This will give anyone in that team the specified access to the content.

{% hint style="info" %}
Team access is a great way to ensure that the right people have access to the right content; any time someone is added to or removed from a team, they’ll gain or lose, respectively, the permissions set on the content.
{% endhint %}

### Giving a member direct access

Similarly to teams, you can also give members direct access. This is the most granular way of managing permissions. When giving single members direct access to a collection or space, you override any inherited permissions they might have. Direct member access is great if you need very specific control over collaborators.

Members with direct access at the space level are removed from the inheritance pattern entirely. Their role is set explicitly, and is not affected by org, site, or collection-level permissions.

### Keeping on top of permissions

While this might seem pretty complex at first, GitBook’s permission model gives you control if you need it, and gets out of the way if you don’t. For many teams, a **set-and-forget** approach to permission management is all they need. For other teams, especially larger organizations, this level of control over access and workflow is essential.

#### Set and forget

If you just want to get your teammates onboarded and editing content with you, then you might never even need to look at permissions. Invite folks, set their default role, and any content you create will default to inheriting these roles. No need to get into the weeds!

#### Control over access and workflow

For larger organizations, teams that split their organization up into discrete collections, or teams that need very granular control over workflow; then getting into the weeds is exactly what’s needed. Using a combination of inheritance, overriding, direct team access and direct user access, you can create workflows and access models that keep you in control.
