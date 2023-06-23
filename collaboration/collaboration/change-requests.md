---
description: Learn about editing with change requests
---

# Change requests

<figure><img src="../../.gitbook/assets/Change requests collab.png" alt=""><figcaption><p>The change requests panel</p></figcaption></figure>

When a space is **locked** for live editing, the main branch of content is read-only, and the only way to contribute to it is by creating and submitting a **change request**.

Change requests are GitBook's way of handling collaboration around branched content.

## Why branched content?

Branches are used heavily in software development, giving contributors ways to keep main code branches protected, with abstracted branches used for proposing or implementing specific changes.

GitBook brings this approach to content and documentation – allowing for content to be branched as many times as required, protecting the main branch of content from changes, giving a clear version history, and allowing for review-focused dynamics around **what** changes make their way into the main branch of content and **why** they're being proposed.

## Creating a change request

In a space that is **locked** for live edits, hit the 'Edit' button in the space header to start a new change request.

<figure><img src="../../.gitbook/assets/start a change request.png" alt=""><figcaption><p>Click the "Edit" button in the top right corner to start a change request</p></figcaption></figure>

This will take you into the change request straight away.

While you're in a change request, you might notice it's all pretty familiar if you've used a live edit space already. Your changes are sync'ed automatically, you can collaborate on change request with real-time collaboration, and you have the same editor experience.

The main difference is that **this is a branch of the main content** – your edits are made specifically to the change request.

Once you're happy with your changes, you can **submit** the change request.

## Submitting a change request

<figure><img src="../../.gitbook/assets/submit for review.png" alt=""><figcaption><p>Submit your change request for review in the bottom right corner of the editor</p></figcaption></figure>

Change requests are submitted when you want to indicate to collaborators that the change request is ready for review (or you just want to review it yourself!)

Upon submitting, a change request will have its status changed to **in review** and members of the space will be notified.

<figure><img src="../../.gitbook/assets/change-request-notification.png" alt="A screenshot showing a GitBook space with the notifications panel open. There is one unread notification, notifying the user that a change request has been submitted for review."><figcaption><p>A notification that a change request has been submitted for review</p></figcaption></figure>

## Reviewing a change request

It's up to you and your team how you want to handle reviews; GitBook is not opinionated or forceful in this regard. Some folks have a very loose review process, others have strict procedures using advanced permission roles.

Most reviews will take place in the change request's [comments](../comments-discussion.md); where collaborators can share feedback and discussions against specific content blocks, or against the change request as a whole.

### Diff mode

You can toggle diff mode on or off for any change request. This will give you an in-context comparison of the primary content and the changes made in the change request.

<figure><img src="../../.gitbook/assets/diff.png" alt="A screenshot showing diff mode enabled on a space. Content that has been removed is highlighted in red, and content that has been added is highlighted in green."><figcaption><p>Diff mode enabled on a space</p></figcaption></figure>

{% hint style="info" %}
When talking about change requests, it's important to understand how specific roles can affect review dynamics. Members with an [**editor**](../../account-management/member-management/roles.md#editor) role will be able to create and submit requests, but only members with [**reviewer**](../../account-management/member-management/roles.md#reviewer) or above roles are able to merge change requests. When setting your permissions, keep in mind the type of edit and review dynamic you want to achieve!
{% endhint %}

## Merging a change request

<figure><img src="../../.gitbook/assets/merge.png" alt="A screenshot showing a GitBook space with the merge button, located near the bottom-right corner of the screen, highlighted."><figcaption><p>Use the merge button when a change request has been reviewed</p></figcaption></figure>

Once a change request has been reviewed, it's time to merge! Merging a change request will 'put' the change request's changes into the main branch of content, creating an updated main branch and a new item in the space's version history.

### Handling merge conflicts

Sometimes, when you want to merge a change request, there'll be conflicts between your primary content and the content you're trying to merge. In the simplest form, a conflict is a piece of content that could not be merged automatically. Silly computers.

In the event of a conflict, you'll be presented with a conflict alert, and a list of the conflicts:

### Resolving merge conflicts

You have two options when it comes to resolving a merge conflict, **manually** **editing the content** to ensure that it ends up how you intended, or **automatically selecting a version** either 'yours' or 'theirs'.

#### Manually editing

To resolve a merge conflict by manually editing, go ahead and edit the content directly. You'll be able to delete the blocks you don't need, or even rewrite them entirely. Once you're happy with the changes, you can move on to the next conflict, if it exists!

#### Automatically merging a version

If you've ever dealt with merge conflicts in Git (we feel you) then you might be familiar with the 'yours' and 'theirs' approach. This is essentially a binary choice between one change and another, you either want to keep 'your' work, or you want to keep 'theirs'. If you're dealing with a merge conflict that can be resolved this way, you can select the change you want to keep, and the other change will be deleted.

## Archiving a change request

If you decide not to merge a change request and want to remove it from the review queue, you can archive it.

<figure><img src="../../.gitbook/assets/archive.png" alt="A screenshot of a GitBook space. A menu icon near the bottom-right corner is highlighted. Clicking on this icon opens a menu, and from this menu you can click on archive."><figcaption><p>Archiving a change request</p></figcaption></figure>

To archive a change request, open the context menu next to the **merge** button near the bottom-right corner of your change request. Click on **archive**. Once you confirm, the change request will no longer be listed as active. If you need, you can find it later in the archive section of your space's change request listing panel, and you can reopen it at any time.
