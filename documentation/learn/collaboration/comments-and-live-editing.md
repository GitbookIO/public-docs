---
description: Comment on content and edit together in real time.
---

# Comments and live editing

## Comments

Comments let you leave feedback on specific content without switching out of GitBook.

### Add a comment

Click the **Comments** button in the [section header](../../resources/the-gitbook-interface.md) to open the comments panel. Commenting there attaches feedback to the whole page — to comment on a specific block instead, hover over it and click the comment icon that appears on the right.

Tag teammates by typing `@` followed by their name.

{% hint style="info" %}
Guests can leave comments, but can't see or mention other users in the organization.
{% endhint %}

### Comment threads

Reply to any comment to turn it into a discussion thread, or leave an emoji reaction by clicking the emoji button on a message or thread.

### Resolving comments

Resolve a comment when you're done with it — this hides it from the main view, while keeping it accessible in the comments panel's **Resolved** tab.

## Live editing

With live edits enabled, org members can edit a section directly, without creating a [change request](change-requests/README.md). While editing, you'll see the avatars of anyone else currently viewing the section, and GitBook supports true live collaboration — multiple people working the same document at once.

{% hint style="info" %}
Live edits are **locked** by default on any newly created section. To edit content, either [create a change request](change-requests/README.md) or unlock live edits.
{% endhint %}

### Toggling live edit mode

Toggle live edit mode from a section's **Actions menu** in the [section header](../../resources/the-gitbook-interface.md) — click **Lock live edits** or **Unlock live edits**.

When a section is in live edit mode, its header shows an **Editor** tab. When locked, it shows a **Read-only** tab instead — from there, you'll need to open a change request to edit content, or unlock live edits.

### When live editing isn't available

You can't unlock live editing if:

1. The section is published with **Public** or **Unlisted** visibility.
2. The section has [GitHub or GitLab Sync](../git-sync/README.md) enabled.

{% hint style="info" %}
Only [administrators and creators](roles-permissions-inheritance.md) can lock or unlock live edits.
{% endhint %}
