# Roles

When adding members to your organization, you can give them a **default role**. This role will apply to any content that inherits its permissions from the organization.

{% hint style="info" %}
Understanding default roles is key to getting the most out of how GitBook handles permission management.&#x20;

See our documentation on [**permissions and inheritance**](permissions-and-inheritance.md) for a full overview of how permissions cascade throughout content in GitBook.
{% endhint %}

### Roles in GitBook

Roles are how you define the level of access and control that members have over content (and the organization, in the case of admins).

{% hint style="warning" %}
Regardless of role, _**every**_ _**single member**_ of an organization _**counts towards**_ the total number of members for _**billing**_ purposes.\
\
You might also like to learn more about [inviting and removing members](invite-members-to-your-organization.md).
{% endhint %}

Each role gets progressively higher levels of access as you move up the list. Let’s start at the lowest access and work our way up:

<details>

<summary>Guest role</summary>

The guest role is a very specific role in GitBook. Guests are members that have **no default organization role**. A guest acts as a standard user in every other regard, they just need to have their permissions set explicitly at a content level.

Inviting a guest to the organization means that they’ll only ever see content they’ve been directly added to. This is great if you want to add external stakeholders or contractors to your organization, but don’t want to worry about giving them access to any content by default.

**Please note that guest members, as with all other members, count towards the total number of members in an organization for billing purposes.**

</details>

<details>

<summary>Reader</summary>

A reader is the most basic role in GitBook: it gives read-only access.

**Reader seats are paid for organizations on all plans**.&#x20;

</details>

<details>

<summary>Commenter</summary>

Commenters have the same read-only access as readers, but they’re also able to leave comments against content and spaces (find our more about how that works in our [comments](../../collaboration/comments.md) documentation).

**Commenter is one of our two advanced member roles, available only on the Pro or Enterprise plan.**

</details>

<details>

<summary>Editor</summary>

Editors are able to read and comment, just like a commenter, but they’re also able to edit content in a couple of ways. Firstly, for spaces that are **open** for [live edits](../../collaboration/live-edits.md), editors can edit the content directly. Secondly, for spaces that have live edits **locked**, editors can create and submit [change requests](../../collaboration/change-requests/). Editors cannot merge change requests.

</details>

<details>

<summary>Reviewer</summary>

Reviewers have all the same permissions as an editor however, they can also merge their own and others’ change requests.

**Reviewer is one of our two advanced member roles, available only on the Pro or Enterprise plan.**

</details>

<details>

<summary>Creator</summary>

Creators are essentially content-level admins. They have all the same permissions as a reviewer, however they can also create and delete spaces, collections and sites, merge change requests and manage permissions at a content level.&#x20;

If a creator is also a creator or admin in another GitBook organization, they have the ability to [move content between organizations](../../creating-content/content-structure/space.md#move-a-space).

</details>

<details>

<summary>Admin</summary>

An admin is like a super-user for your organization — they have full access! Set someone as an admin if you’re comfortable with them making changes that can impact billing, managing members, and generally just being in control of all areas of the organization.&#x20;

If an admin is also a creator or admin in another GitBook organization, they have the ability to [move content between organizations](../../creating-content/content-structure/space.md#move-a-space).

</details>
