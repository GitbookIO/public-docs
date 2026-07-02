---
description: "Learn about collaborating on a single change request in a space —\_including how to review, resolve conflicts and merge"
---

# Change requests in a space

When you’re within a [space](../../resources/concepts.md#space), you can make changes by opening a new change request, or browse existing change requests to see what other people are working on.

### Creating a change request

Click the **Edit** button in the [space header](../../resources/gitbook-ui/#space-header) to start a new change request.

This will open a new change request, where you can edit or delete content as needed. Your changes are saved automatically, and other people can join you in a change request to collaborate in real-time.

When creating a change request, you can add a title and description to provide more context about the changes you’re making.

You can also link the change request to a source, including:

* Linear issues
* GitHub pull requests or issues
* Jira tickets
* General URLs

These links appear on the change request, so reviewers can trace the work back to its origin.

Once you’re happy with your changes, you can use the button in the header bar to [**Request a review**](change-requests-in-a-space.md#request-a-review-on-a-change-request) of your change request, or [**Merge**](change-requests-in-a-space.md#merging-a-change-request) it directly into the main branch.

#### Creating a change request with GitBook Agent

[GitBook Agent](../../gitbook-agent/what-is-gitbook-agent.md) is an AI teammate that can [plan and implement change requests](../../gitbook-agent/write-and-edit-with-ai.md#implement-a-change-request-with-gitbook-agent) based on any instructions you give it.

To open a new change request with GitBook Agent, click the GitBook Agent icon in the upper right corner next to the “Edit” button, and ask GitBook to implement any changes you want.

Some things you can ask it to do include:

* Add usage examples
* Improve page SEO
* Enhance clarity
* Check for consistency
* Fix typos and spelling errors
* Link related content
* \+ more

Head to [Writing with GitBook Agent](../../gitbook-agent/write-and-edit-with-ai.md) to learn more.

### Previewing a change request

You can preview the changes you’ve made in a change request by clicking the **Preview** option in the [space header](../../resources/gitbook-ui/#space-header). This will switch to a preview of your published docs with the proposed changes included, so you can see your changes in the entire context of your published documentation.

Below the **Preview** button is a URL for your site preview. Click this and your site preview will open in full in a new tab.

When you open a preview URL in a new tab, you will also see [the Preview toolbar](../../resources/gitbook-ui/toolbar-on-published-sites-and-site-previews.md) at the bottom of the browser window. This toolbar lets you quickly jump back into GitBook to view, edit, or comment on the change request, or open the live version of your site.

{% hint style="info" %}
You can only preview change requests for spaces added to a [published docs site](../../docs-site/publish-a-docs-site/).
{% endhint %}

{% hint style="warning" %}
If your content is published using share links or authenticated access, the preview function won't appear.
{% endhint %}

### Request a review on a change request

Request a review on your change request when you want to ask members of your team to check your content before you merge the changes into the main branch.

Select the **Overview** tab in the space header bar to open an overview of your change request — including all the changes you’ve made in diff view.

Here you can add a description to your change request to give your reviewers some context, and tag specific people that you want to check your work.

When you click **Request a review**, the change request’s status will change to **In review**, and anyone you tagged in your review request will get a notification.

If your changes don’t require a review, you have the appropriate [permissions](../member-management/roles.md), and you don’t have any blocking [merge rules](../merge-rules.md), you can merge your changes into the main version directly instead.

{% hint style="info" %}
[Add GitBook Agent as a reviewer](../../gitbook-agent/review-change-requests-with-gitbook-agent.md) to your change request and it can check your content for spelling, grammar and style guide errors, suggest improvements and more.
{% endhint %}

{% hint style="warning" %}
If you don’t tag anyone in your review request, everyone with reviewer permissions in the space gets a notification. If the space has no reviewers, the next role above reviewer gets the notification.
{% endhint %}

#### Diff view <a href="#diff-mode" id="diff-mode"></a>

When you open the **Changes** tab in the space header, the diff view will appear. Diff view highlights every page and block that’s been edited in a change request. It will highlight any edited pages in the table of contents, and on the pages it will show the specific blocks that have been added, edited or removed.

If a page contains diffs, GitBook also shows a floating centered indicator. Click it to scroll to the first changed block or element.

There are two options when using diff view:

1. **Show all pages** – This is the default mode for diff view, which will show both modified and non-modified pages in the table of contents. This is good for seeing which pages have been edited in the context of the entire space.
2. **Show only changed pages** – This mode will show only the modified pages in the table of contents, which helps you focus on the changed content. This is particularly helpful in larger spaces with many pages and sub-pages.

You can switch to the **Changes** tab to check the diff view in any change request.

### Merging a change request

Merging a change request will add the change request’s changes into the main branch of content, creating an updated version and a new entry in the space’s [version history](../../creating-content/version-control.md#see-the-activity-of-a-specific-draft).

You might not be able to merge a change request if you don’t have the right [permissions](../member-management/permissions-and-inheritance.md), or if your change request hasn’t passed your organization or space’s [merge rules](../merge-rules.md).

### Updating a change request

As you're working inside a change request, other contributors may be modifying the main branch of the space. When this happens, your change request is considered "out of date" - there is content on the main branch that you don't see inside your change request.

You may want to pull in this new content into your change request. This can be useful if:

* You want to see how your changes and the content on main look once everything is together.
* You need to make changes to the pulled content as part of your change request.

You can do this by pressing **Update** in the header of the change request screen.

Once you press **Update**, all content from the main branch is pulled into your change request. You may get conflicts when you update - you'll be able to resolve them inside the change request. Once conflicts have been resolved, the change request is considered up-to-date and the Update button disappears.

If the main branch changes again, your change request will again be out-of-date and the Update button will appear.

Asking editors to have their change requests up-to-date before merging is a good quality control - it helps authors check the exact content that will go into the main branch once their change request is merged. You can enforce this with a [merge rule](../merge-rules.md).

### Resolving merge conflicts

Sometimes, when you want to merge a change request, you may discover conflicts between the main content and the content you’re trying to merge. In the simplest form, a conflict is a piece of content that could not be merged automatically.

If this happens, you’ll be presented with a conflict alert, and a list of the conflicts you’ll need to resolve before continuing the merge.

You have two options when it comes to resolving a merge conflict — **selecting a version to merge** or **manually** **editing the content**.

#### Selecting a version to merge

You can resolve a merge conflict by selecting a version you want to merge — either your incoming content, or the content that was previously there. This allows you to choose between one change and another — either your recent work, or the original content.

If you’re dealing with a merge conflict that can be resolved this way, you can select the version you want to keep, and the other version will be deleted.

#### Manually editing

If you don’t want to choose between versions, you can resolve a merge conflict by manually editing the conflict. You’ll be able to delete the blocks you don’t need, or even rewrite them entirely. Once you’re happy with the changes, you can move on to the next conflict until they’re all resolved.

### Archiving a change request

You can't delete a change request in GitBook, but you can archive it instead.

To archive a change request:

1. Open the **Change requests** tab.
2. Select the change request you want to archive.
3. Click the **Actions** menu <picture><source srcset="../../.gitbook/assets/25_02_04_actions_horizontal.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/25_02_04_actions_horizontal_1.svg" alt="The Actions menu icon in GitBook"></picture> next to the change request's title and choose **Archive**.

To find and reopen an archived change request, open the **Change requests** menu and select the **Archived** tab.
