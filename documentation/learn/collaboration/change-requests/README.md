---
description: "The change request workflow: propose, review, and merge content changes."
---

# Change requests

A change request is a copy of your main content, based on the concept of branching — familiar if you've used pull requests in GitHub or merge requests in GitLab.

In a change request, you edit, update, or delete content, request reviews, then merge back into your main version.

### Review changes in diff view

Open the **Changes** tab in a change request to review edits — either all pages in context, or changed pages only.

{% hint style="info" %}
By default, changes show in split view: the left side shows the "before" version, the right shows "after." To view changes inline in a single column, click the diff-mode button at the top-right of the table of contents panel.
{% endhint %}

### The lifecycle, at a glance

{% stepper %}
{% step %}
#### Open a change request

Click **Edit** in the top right of a section, ask GitBook Agent to create one, or let GitBook Agent create one automatically when it detects a documentation gap. See [Create a change request](create.md).
{% endstep %}

{% step %}
#### Make your changes

Edit directly, or work with GitBook Agent. Keep editing until you're ready to request a review.
{% endstep %}

{% step %}
#### Request a review

Tag reviewers from the **Overview** tab — or merge directly if your permissions and merge rules allow it. See [Review and merge](review-and-merge.md).
{% endstep %}

{% step %}
#### Merge

Once approved, click **Merge**. GitBook applies the changes to your live docs immediately, checking any [merge rules](merge-rules.md) first. Merging can't be undone — open a new change request to revert or adjust.
{% endstep %}
{% endstepper %}

### Browsing change requests across your site

The change requests screen lets you view and manage every active change request across your site — open, merge, or collaborate with GitBook Agent on updates, all in one place. Open it from **Change requests**, under **General** in the site sidebar.

All change requests in your site appear there. Filter by status, or filter to show only change requests created by GitBook Agent. Click one to open an expanded view showing participants, reviewers, description, and a diff of the changes — or click **Edit** to open its section and inspect diffs in the editor's **Changes** tab instead.
