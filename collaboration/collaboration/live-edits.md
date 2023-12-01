---
description: >-
  With live editing you can start making changes to your internal documentation
  on the spot. There’s no need to create a change request first.
---

# Live edits

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/saving.png" alt="A screenshot of a GitBook space. Near the top-right corner, &#x22;saving&#x22; is highlighted, showing how GitBook automatically saves your work in live edit mode."><figcaption><p>GitBook saves your live edits automatically</p></figcaption></figure>

</div>

**Live editing** is the default mode of any newly-created GitBook space. A space in live edit mode is editable instantly by anyone with the [correct permission level](../../account-management/member-management/).

{% hint style="info" %}
Live editing is not available [in some cases](live-edits.md#when-is-live-editing-not-available).
{% endhint %}

When a space’s live edits are **unlocked**, you’ll be able to see the avatars of the team members that are currently viewing the space. This is shown at the top right corner of the page. Anyone can start editing the space, but this works on a first come first served basis. When an editor starts making changes, editing is temporarily locked for all other viewers in that space. Once the editor’s changes are saved, editing is released and made available to any of the viewers that want to start making changes.

## Toggling live edits on or off

You can lock or unlock space for live edits by selecting ’Unlock live edits’ and ’Lock live edits’ from the Space’s actions menu.

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Unlock live edits.png" alt=""><figcaption><p>Unlock live edits from the space actions menu</p></figcaption></figure>

</div>

### When is live editing _not_ available?

It is not possible to unlock live editing in the following cases:

1. When a space is published with the **In collection**, **Public**, or **Unlisted** visibility option. We hope to change this in the future.
2. When [Git Sync](../../integrations/git-sync/) is enabled.

{% hint style="info" %}
Only users with the **admin** or **creator** [roles](../../account-management/member-management/roles.md) can lock or unlock live edits.
{% endhint %}
