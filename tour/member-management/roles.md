# Member roles

![](<../../.gitbook/assets/Space Permissions.png>)

When adding members to your organization, you can give them a **default role**. This role will apply to any content that inherits its permissions from the organization.

{% hint style="info" %}
Understanding default roles is key to getting the most out of how GitBook handles permission management. Check out [**Permissions and inheritance**](permissions-and-inheritance.md) for a full overview of how permissions cascade throughout content in GitBook.
{% endhint %}

## Roles in GitBook

Roles are how you define the level of access and control that members have over content (and the organization, in the case of admins). Each role gets progressively higher levels of access as you move up the list. Let's start at the bottom:

### Reader

A reader is the most basic role in GitBook: it gives read only access.

### Commenter

Commenters have the same read-only access as readers, but they're also able to leave comments against content and spaces (find our more about how that works over at the [Comments](../../getting-started/collaboration/comments-discussion.md) documentation).

{% hint style="info" %}
Commenter is one of our two advanced member roles, available only on the **Pro or Enterprise plan**.
{% endhint %}

### Editor

Editors are able to read and comment, just like a commenter, but they're also able to edit content in a couple of ways. Firstly, for spaces that are **open** for [live edits](../../getting-started/collaboration/live-edits.md), editors can edit the content directly. Secondly, for spaces that have live edits **locked**, editors can create and submit [change requests](../../getting-started/collaboration/change-requests.md). Editors cannot merge change requests.

### Reviewer

Reviewers have all the same permissions of an editor, however they can also merge their own and others' change requests.

{% hint style="info" %}
Reviewer is one of our two advanced member roles, available only on the **Pro or Enterprise plan**.
{% endhint %}

### Creator

Creators are essentially content-level admins. They can create, delete and publish spaces and collections; manage permissions at a content level.

### Admin

An admin is essentially a 'super-user' for your organization – they can do pretty much anything! Set someone as an admin if you're comfortable with them making changes that can impact billing, managing members, and generally just being in control of all areas of the organization.

## The guest role

The guest role is a very specific role in GitBook. Guests are members that have **no default organization role**. A guest acts as a standard user in every other regard, they just need to have their permissions set explicitly at a content level.

Inviting a guest to the organization means that they'll only ever see content they've been directly added to. This is great if you want to add external stakeholders or contractors to your organization, but don't want to worry about giving them access to any content by default.
