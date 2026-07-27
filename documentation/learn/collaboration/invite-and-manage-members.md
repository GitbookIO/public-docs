---
description: Add teammates to your organization and manage their access.
---

# Invite and manage members

{% hint style="warning" %}
Inviting additional members to your organization — regardless of their role or how you add them — immediately impacts the price of your subscription. See [Plans and billing policy](../../account-and-billing/plans-and-billing-policy.md) for the details.
{% endhint %}

## Invite someone to your organization

### Via email

Invite members directly through your [organization settings](../../account-and-billing/personal-and-organization-settings.md). In the **Members** section, click **Invite new members**, add email addresses, select their default role, and click **Invite**. Each person gets an email to sign up and instantly join your organization.

{% hint style="info" %}
**Email domain.** You can allow anyone with a specific email domain to join automatically — open **Members** → **Invite new members** and enable the toggle at the bottom of the modal.
{% endhint %}

### Via invite link

Invite links let members sign up and join your organization without an individual email invite. Each link is tied to a specific [role](roles-permissions-inheritance.md), and you can create or revoke as many as you like.

{% stepper %}
{% step %}
#### Open Members settings

Open your [organization settings](../../account-and-billing/personal-and-organization-settings.md) → **Members**.
{% endstep %}

{% step %}
#### Invite by links

Click **Invite new members**, then **Invite by links**.
{% endstep %}

{% step %}
#### Use or create a link

Use an existing link, or click **Create multiple links** to add a new one.
{% endstep %}

{% step %}
#### Set the role and share

Select the [role](roles-permissions-inheritance.md) for new members, copy the link, and share it.
{% endstep %}
{% endstepper %}

To revoke a link, follow the same steps, then open the link's **Actions menu** and choose **Revoke**.

## Invite someone to a single space or collection

Click **Share** in the top-right corner of a space, or open a collection's **Actions menu** and choose **Permissions** — either opens the **Share** modal.

**To invite an existing member or team:** open the **Share** modal, type their name (or a [team](#teams)'s name), choose their role for this space, and click **Invite**. This matters when someone's [role](roles-permissions-inheritance.md) or [permissions](roles-permissions-inheritance.md) don't already cover a specific space.

**To invite someone outside your organization:** open the **Share** modal, enter their email, choose their role, and click **Invite**. By default they join as a [guest](roles-permissions-inheritance.md#guest-role) — guests only access the spaces they're invited to, with whatever role you give them there (editing, or just viewing and commenting). Enable **Invite as an organization member** instead to give them the selected role across all your team's content.

{% hint style="warning" %}
Inviting additional members — as a full member or a guest — immediately impacts the price of your subscription. See [Plans and billing policy](../../account-and-billing/plans-and-billing-policy.md).
{% endhint %}

**To invite guests via a shared link:** create a secret link instead of inviting by email — useful for inviting several people as guests at once. Set the role guests get when they join via the link; anyone who clicks it can sign up, join as a guest, and get access to just that space. Revoke it anytime from the link's **Actions menu** → **Revoke**.

## Manage or remove members

View and manage members from the **Members** section of your [organization settings](../../account-and-billing/personal-and-organization-settings.md) — change roles, see last-active times, view teams and content access, or use the **Actions menu** to copy a member's name/email/user ID or remove them. Click any member for a dedicated details screen.

### Leaving an organization

Open **Settings** → **Organizations**, hover over the organization, and click **Leave**.

{% hint style="danger" %}
You can't rejoin an organization you've left unless you're invited again.
{% endhint %}

If you're an administrator and want to leave, ask another admin to remove you instead.

### Removing a member

Open **Settings** → **Members**, find the member, open their **Actions menu**, and choose **Remove member**.

### Transferring ownership

Nobody "owns" a GitBook organization, but every organization needs at least one admin. If you want a single person in charge of billing and member management, downgrade other admins to the Creator role.

You can add a new admin at any time. If your only admin has already left, see "the only admin left the organization" below.

<details>

<summary>How do I add and manage admin roles in my organization?</summary>

Administrators manage your organization's settings, billing, and member permissions.

**Adding a new admin:** invite them to your organization as described above, selecting **Administrator** as their role. Once they accept, they gain access to administrative settings, including billing.

**If the only admin has left the organization:**

1. [Contact GitBook support](https://www.gitbook.com/contact) to request an update to organization admin permissions.
2. Complete identity verification — typically confirming details linked to the account, such as payment card information.

{% hint style="info" %}
GitBook verifies your identity whenever administrative roles change, to confirm the requesting party's association and authority within the organization.
{% endhint %}

</details>

<details>

<summary>How do I downgrade my organization to a free single-user plan?</summary>

The free plan only allows a single user, with no docs sites. To downgrade, remove all other members first. The admin who remains can remove other users entirely, blocking their access to collaboration and editing features, and should update their own details in the [Billing section](../../account-and-billing/personal-and-organization-settings.md) of organization settings so future bills and receipts go to the right person.

</details>

## Teams

Teams group members so you can manage access at scale — grant or remove a whole team's access to spaces or collections at once. See [Roles, permissions, and inheritance](roles-permissions-inheritance.md) for how team access interacts with individual roles.

### Creating and managing teams

Create, edit, and remove teams from the **Teams** section of your organization settings — click the settings icon, choose the organization, then **Teams** in the sidebar. From there, view and search current teams, or click one to open its details page.

### Managing team members

You can manage team members two ways:

1. Open a member's page (from **Members & permissions**), select the **Teams** tab, click the vertical ellipsis next to a team, and remove them immediately or choose **Manage team**.
2. In the **Teams** section, click a team's member count to open its details page, then multi-select members to remove, or use the button at the top to add more.

### Team owners

Team owners (Enterprise plans only) let you hand over management of a specific team to a selected member. Team owners can add and remove members from teams they own, directly from organization settings → Teams, but have no access to any other organization settings — including managing other teams.
