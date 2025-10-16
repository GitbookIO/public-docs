---
description: Edit pages in real-time with other collaborators
icon: file-pen
---

# Live edits

With live edits enabled, members in your org can edit a space without creating [a change request](change-requests.md). When editing content, you can see the avatars of anyone currently viewing the space in the top-right corner.

GitBook supports live collaboration, meaning you’ll be able to work on the same document with multiple members at the same time.

{% hint style="info" %}
**Live edits are locked** by default in any newly created space. To edit the content, you will either need to [create a change request](change-requests.md), or toggle live edits on.
{% endhint %}

### Toggling live edit mode

You can toggle live edit mode in a space by selecting **Lock live edits** or **Unlock live edits** from the [space header’s](../resources/gitbook-ui.md#space-header) **Actions menu** <picture><source srcset="../.gitbook/assets/actions-horizontal - dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/actions-horizontal.svg" alt="The Actions menu icon in GitBook"></picture>.

When a space is in **Live edits** mode, the space header will show the **Editor** tab. When it is in **Locked live edits** mode, the space header will show a **Read-only** tab. When the Read-only tab appears in the space header, you will need to open a change request to edit the content of the page, or unlock live edits.

### When is live editing _not_ available?

You cannot unlock live editing if:

1. a space is published with the **In collection**, **Public**, or **Unlisted** visibility option.
2. a space has [GitHub or GitLab Sync](../getting-started/git-sync/) enabled.

{% hint style="info" %}
Only [administrators and creators](../account-management/member-management/roles.md) can lock or unlock live edits.
{% endhint %}
