---
description: "Change requests in GitBook make it easier for your whole team contribute to the documentation process —\_whether they’re editing pages, reviewing changes, or just leaving feedback"
---

# Make your documentation process more collaborative with change requests

Here at GitBook, the [change request workflow](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/collaborate/change-requests) is at the core of the collaborative documentation process.

Change requests are a great way to collaborate on edits with your team in a branch, before merging those changes with your published content. It doesn’t just give you peace of mind when editing docs that are already published — it brings more people into that process, and helps you get feedback in context.

Ultimately, we believe that developers’ asynchronous workflows are the future for knowledge sharing. And we want to make it as simple as possible for everyone in your team to collaborate and create documentation using GitBook. That’s why you can work together in GitBook just like you do in GitHub or GitLab.

Here’s how to build a collaborative docs workflow with change requests at the center.

### Tips for working with change requests <a href="#new-change-request-improvements" id="new-change-request-improvements"></a>

#### Use diff view to see what’s changed

Just like in GitHub and GitLab, [diff view](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/collaborate/change-requests#diff-mode) shows you everything that’s been added, deleted or edited in a change request. When you enable the **View changes** toggle at the top of a change request, you’ll notice that markers appear next to pages and lines will appear next to blocks on your page to show everything that’s different.&#x20;

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2FNS6hUu0VKIg5KPX7JBJ0%2Fdiff%20view.mp4?alt=media&token=af66a88b-538e-465a-ad7e-3082b31f9564?autoplay=1" %}
Diff view is perfect when you’re reviewing a change request, as it helps you see precisely what’s been edited.
{% endembed %}

In the **View changes** menu, you can switch between showing every edited page, or just the pages with edits in this specific change request. The latter is ideal when you’re reviewing a change request and just want to jump right to what’s new.

#### Check the preview to see changes in context

The only way to edit content that’s published as part of a docs site is through a change request. But how do you know what the edits you’re making will look when you update the published docs?&#x20;

Simply hit **Preview** in the space header bar and GitBook will load [a deploy preview](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/collaborate/change-requests#preview-a-change-request) to show how your docs site will look with the current changes. You can view it as many times as you like, and hit the refresh button in the bottom bar to update the preview when you make new edits.

<figure><img src="../.gitbook/assets/deploy-preview.jpg" alt=""><figcaption><p>The deploy preview will show you what you published page will look like once you merge your change request. You can update the preview or jump back to the change request using the controls at the bottom of the window.</p></figcaption></figure>

#### Use Git Sync so you can make edits from GitHub or GitLab

[Git Sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync) is a super powerful tool that lets you sync your docs with a GitHub or GitLab repository, so changes you make in one place will sync with the other.&#x20;

When you set up Git Sync, you can make changes to your docs in either location — either by creating a change request in GitBook or opening a pull request in GitHub. This will create a new branch in each location, so your developers can make edits in their IDE while technical writers work in the GitBook editor. And everything stays completely in sync.

It’s a powerful collaborative tool, so we definitely recommend setting it up to encourage more people to contribute to your docs.&#x20;

#### Set up reviewers to approve and merge your content

[Permissions](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/collaborate/member-management/permissions-and-inheritance) in GitBook give you tons of control over who can do what with your docs. You can give each user [a specific role](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/collaborate/member-management/roles) in your organization — and then override them at a content-level.&#x20;

You can view and change space-level permissions from the **Share** menu. Here you can see everyone with access and change their permissions, or invite more users.

<figure><img src="../.gitbook/assets/permissions-share-menu.jpg" alt=""><figcaption><p>Permissions are inherited from the collection or organization by default, but you can change or revoke the permissions of any member, or invite guests from the <strong>Share</strong> menu.</p></figcaption></figure>

So if you want specific people to review every change request in a space before it’s merged into the primary version of your documentation, you can set the space permissions so they are the only users who can review and merge. Or you can invite specific users as commenters, so they can only leave feedback on the changes without being able to edit the page directly.&#x20;

#### Check changes and roll back using the version history

Want to see how a change request evolved over time? With the [version history](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/version-control) you can see snapshots of your documentation over time, and click any one to revisit it and see the content at that point. Want to roll back to that version? No problem — you can do that from the revision’s Actions menu, and that rollback will be recorded in the history as well.

***

Collaboration is a key part of creating great product documentation. Give change requests a try and see how they can improve your docs workflow.

[**→ Read more about change requests**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/collaborate/change-requests)

[**→ How to handle merge conflicts in GitBook**](../editing-and-publishing-documentation/how-to-handle-merge-conflicts-in-gitbook.md)

[**→ The complete guide to publishing docs in GitBook**](../editing-and-publishing-documentation/complete-guide-to-publishing-docs-gitbook.md)
