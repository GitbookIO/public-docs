---
description: Review, comment on, and merge a change request.
---

# Review and merge

### Request a review

Request a review when you want teammates to check your content before merging into the main branch.

Click the **Overview** tab in the section header bar to see your change request's changes in diff view, add context, and tag reviewers. To inspect diffs in the editor instead, switch to the **Changes** tab — pages with diffs show an indicator, and a floating diff navigation control helps you jump between changed blocks.

Add a description to give reviewers context, and tag specific people you want to check your work. Click **Request a review**, and the change request's status becomes **In review** — anyone tagged gets a notification.

If your changes don't need a review, you have the right [permissions](../roles-permissions-inheritance.md), and there's no blocking [merge rule](merge-rules.md), you can merge directly instead.

{% hint style="info" %}
Add [GitBook Agent as a reviewer](../../gitbook-ai/agent/review-change-requests.md) and it can check your content for spelling, grammar, and style guide errors, and suggest improvements.
{% endhint %}

{% hint style="warning" %}
If you don't tag anyone, everyone with reviewer permissions in the section gets notified. If the section has no reviewers, the next role above reviewer is notified instead.
{% endhint %}

### Reviewing a change request

When someone requests your review — whether from the section itself or from the [change requests screen](README.md#browsing-change-requests-across-your-site) — you can edit content and leave feedback directly, then request more changes or approve to signal it's ready to merge.

Most reviews happen in the change request's comments, where collaborators discuss specific blocks or the change request as a whole. You can also ask [GitBook Agent](../../gitbook-ai/agent/review-change-requests.md) to review a change request — it can check, plan, and continue working on changes alongside your team.

#### Diff view

If a page has diffs, GitBook shows a floating centered indicator — click it to jump to the first changed block. Pages with diffs also show an indicator in the table of contents, making large change requests easier to scan.

Opening the **Changes** tab shows every edited page and block, with the previous version on the left and the updated version on the right for side-by-side comparison. Two display options:

1. **Show all pages** — changed and unchanged pages together, for reviewing in context.
2. **Show only changed pages** — just the modified pages, to focus on edits.

### Merging a change request

Merging adds the change request's changes to the main branch, creating an updated version and a new entry in the section's [version history](../../creating-content/version-history-and-page-tags.md).

You might not be able to merge if you lack the right [permissions](../roles-permissions-inheritance.md), or if the change request hasn't passed your organization's or section's [merge rules](merge-rules.md).

### Updating a change request

While you're working in a change request, other contributors may modify the main branch. When that happens, your change request is "out of date" — there's content on main that you don't see inside it.

Pull in the new content by clicking **Update** in the header. This is useful if you want to see your changes alongside main's latest content, or need to edit the pulled-in content as part of your change request.

Updating may surface conflicts, which you resolve inside the change request. Once resolved, the change request is up to date and the **Update** button disappears — until main changes again.

Requiring change requests to be up to date before merging is good quality control, since it lets authors verify the exact content that will land on merge. Enforce it with a [merge rule](merge-rules.md).

### Resolving merge conflicts

A conflict is a piece of content that couldn't be merged automatically. If GitBook finds one, you'll see a conflict alert with a list of what needs resolving.

You have two options:

* **Select a version to merge** — choose either your incoming content or what was previously there; the other version is discarded.
* **Manually edit** — delete unneeded blocks, or rewrite them entirely, then move to the next conflict until they're all resolved.

### Archiving a change request

You can't delete a change request, but you can archive one:

1. Open the **Change requests** tab.
2. Click the change request you want to archive.
3. Open its **Actions** menu and choose **Archive**.

To find and reopen an archived change request, open the **Change requests** menu and click the **Archived** tab.
