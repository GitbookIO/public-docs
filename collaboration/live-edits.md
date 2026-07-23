---
description: Edit pages in real-time with other collaborators
icon: file-pen
---

# Live edits

With live edits enabled, members in your org can edit a section without creating [a change request](change-requests/). When editing content, you can see the avatars of anyone currently viewing the section in the top-right corner.

GitBook supports live collaboration, meaning you’ll be able to work on the same document with multiple members at the same time.

{% hint style="info" %}
**Live edits are locked** by default in any newly created section. To edit the content, you will either need to [create a change request](change-requests/), or toggle live edits on.
{% endhint %}

### Toggling live edit mode

You can toggle live edit mode in a section by clicking **Lock live edits** or **Unlock live edits** in the [section header’s](../resources/gitbook-ui/#space-header) **Actions menu** <picture><source srcset="../.gitbook/assets/25_02_04_actions_horizontal.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/25_02_04_actions_horizontal_1.svg" alt="The Actions menu icon in GitBook"></picture>.

When a section is in **Live edits** mode, the section header will show the **Editor** tab. When it is in **Locked live edits** mode, the section header will show a **Read-only** tab. When the Read-only tab appears in the section header, you will need to open a change request to edit the content of the page, or unlock live edits.

### When is live editing _not_ available?

You cannot unlock live editing if:

1. a section is published with the **In collection**, **Public**, or **Unlisted** visibility option. [Confirm: are these visibility options still current in the site workspace model, and what is the "In collection" option called now?]
2. a section has [GitHub or GitLab Sync](../getting-started/git-sync/) enabled.

{% hint style="info" %}
Only [administrators and creators](member-management/roles.md) can lock or unlock live edits.
{% endhint %}
