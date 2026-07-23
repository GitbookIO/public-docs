---
description: >-
  A breakdown of every role in GitBook — what each one can do, and how to use
  them to control access across your organization
---

# Roles

When adding members to your organization, you can give them a **default role**. This role will apply to any content that inherits its permissions from the organization. Understanding default roles is key to getting the most out of how GitBook handles permission management.

See our documentation on [**permissions and inheritance**](permissions-and-inheritance.md) for a full overview of how permissions cascade throughout content in GitBook.

### Roles in GitBook

Roles are how you define the level of access and control that members have over content (and the organization, in the case of admins).

{% hint style="warning" %}
Regardless of role, every single member of an organization counts toward the total number of members for billing purposes. To learn more about member management, see [inviting and removing members](invite-members-to-your-organization.md).
{% endhint %}

Each role gets progressively higher levels of access as you move up the list. Let’s start at the lowest access and work our way up:

<details>

<summary>Guest role</summary>

The guest role is a very specific role in GitBook. Guests are members that have **no default organization role**. A guest acts as a standard user in every other regard, they just need to have their permissions set explicitly at a content level.

Inviting a guest to the organization means that they’ll only ever see content they’ve been directly added to. This is great if you want to add external stakeholders or contractors to your organization, but don’t want to worry about giving them access to any content by default.

{% hint style="warning" %}
Guest members count toward the total number of members in an organization for billing purposes.
{% endhint %}

</details>

<details>

<summary>Reader</summary>

A reader is the most basic role in GitBook: it gives read-only access.

{% hint style="info" %}
Reader seats are paid for organizations on all plans.
{% endhint %}

</details>

<details>

<summary>Commenter</summary>

Commenters have the same read-only access as readers, but they’re also able to leave comments against content and spaces (find out more about how that works in our [comments](../comments.md) documentation).

{% include "../../.gitbook/includes/pro-and-enterprise-hint.md" %}

</details>

<details>

<summary>Editor</summary>

Editors are able to read and comment, just like a commenter, but they’re also able to edit content in a couple of ways. Firstly, for spaces that are **open** for [live edits](../live-edits.md), editors can edit the content directly. Secondly, for spaces that have live edits **locked**, editors can create and submit [change requests](../change-requests/). Editors cannot merge change requests.

</details>

<details>

<summary>Reviewer</summary>

Reviewers have all the same permissions as an editor however, they can also merge their own and others’ change requests.

{% include "../../.gitbook/includes/pro-and-enterprise-hint.md" %}

</details>

<details>

<summary>Creator</summary>

Creators are essentially content-level admins. They have all the same permissions as a reviewer, however they can also create and delete spaces, collections and sites, merge change requests and manage permissions at a content level.

{% hint style="info" %}
If a creator is also a creator or admin in another GitBook organization, they can [move content between organizations](../../creating-content/content-structure/sections.md#move-a-space).
{% endhint %}

</details>

<details>

<summary>Admin</summary>

An admin is like a super-user for your organization — they have full access! Set someone as an admin if you’re comfortable with them making changes that can impact billing, managing members, and generally just being in control of all areas of the organization.

{% hint style="info" %}
If an admin is also a creator or admin in another GitBook organization, they can [move content between organizations](../../creating-content/content-structure/sections.md#move-a-space).
{% endhint %}

</details>

### Roles on a docs site

When roles are applied at the [site level](permissions-and-inheritance.md), only **Administrators** can change site settings. All other roles can still contribute to and edit content in the spaces they have access to — they just can't manage the site itself. The table below shows how each role maps to its site permissions.

| Permission level | Permissions on the site |
| ---------------- | ----------------------- |
| Administrator    | Edit and view           |
| Creator          | View                    |
| Reviewer         | View                    |
| Editor           | View                    |
| Commenter        | View                    |
| Reader           | View                    |
| No access        | Cannot view             |

### **Reader role and public docs reader**

The Reader role is an invited organization member with a paid seat. A public docs reader is a site visitor who doesn't need an invitation or a paid seat.

<table><thead><tr><th width="198.80078125"></th><th>Reader role (your organization)</th><th>Public docs reader (site visitor)</th></tr></thead><tbody><tr><td><strong>Invitation required</strong></td><td>Yes</td><td>No</td></tr><tr><td><strong>Paid seat</strong></td><td>Yes</td><td>No</td></tr><tr><td><strong>Content access</strong></td><td>Published and unpublished (with permission)</td><td>Published only</td></tr></tbody></table>
