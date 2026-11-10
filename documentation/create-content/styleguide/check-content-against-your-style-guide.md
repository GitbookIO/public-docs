---
description: >-
  Review a page, a change request, or whole spaces against your style guide with
  GitBook Agent.
---

# Check content against your style guide

GitBook Agent follows your style guide whenever it writes or edits content. To check content that already exists, or changes before they're merged, use one of three checks:

| Check                                                                                                               | Covers                          | What the Agent does                                 | Use it when                                         |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| [Page check](check-content-against-your-style-guide.md#check-a-page)                                                | One page                        | Leaves comments and changes nothing                 | You're working on a page                            |
| [Change request review](check-content-against-your-style-guide.md#request-a-style-guide-review-on-a-change-request) | The changes in a change request | Requests changes and cites the rules they break     | Your changes are ready for review                   |
| [Site check](check-content-against-your-style-guide.md#run-a-style-guide-check-across-your-site)                    | Up to three spaces at a time    | Fixes what it finds in one change request per space | You want existing content to follow the style guide |

{% hint style="info" %}
Checks use GitBook AI, so it must be enabled for your organization.
{% endhint %}

## Check a page

While you're working on a page, use **Check consistency against style guide** in the **Improve** menu, or ask GitBook Agent in chat. The Agent reviews the page against your style guide and leaves comments summarizing what it found. It doesn't change the page.

## Request a style guide review on a change request

When your site has a style guide, GitBook Agent appears as a suggested reviewer on your change requests, tagged **Style guide review**.

1. In your change request, click **Request review**.
2. Add a title and description for your changes, or click **Generate** to have the Agent write them.
3. Under **Reviewers**, click **Request** next to **GitBook Agent**. You can add other reviewers alongside it, or leave the list empty to notify all reviewers in your organization.

The Agent reviews your changes against the style guide. If it finds violations, it requests changes and cites the rule behind each one.

## Run a style guide check across your site

A site check reviews every page of the spaces you choose and fixes what it finds. You need edit permissions on the site and on each space you check.

1. Open your style guide, go to the **Checks** tab, and click **Run a check**.
2. Choose the spaces to check. You can check up to three spaces at a time.
3. Review and merge the change request GitBook Agent opens for each space.

If a check fixes something, it marks its change request ready for review. If it finds nothing, it archives its change request, so you aren't left with an empty draft.

The **Checks** tab lists your site's spaces in the site's own structure, with the state of each space's check:

* The change request's status, or a spinner while the check is running
* When the check last ran
* A **Style guide edited since** badge when you've changed the style guide after the check

Click a row to open its change request.

Each space has one check change request at a time. If you run a check again while a space's change request is still open, the Agent updates that change request and checks the pages as they are now. A new change request opens only after the previous one is merged or archived.

## Troubleshooting

### A rule isn't flagged

GitBook Agent flags only rules it can enforce. Check that the rule:

* Has a numbered ID, or is a definite, checkable instruction
* Doesn't still contain placeholder text
* Doesn't have an exception that covers the text

If the rule is on a page other than the first, the Agent reads it only when a task touches that page's topic. Move core rules to the first page.

### Rules in custom instructions aren't enforced in reviews

GitBook Agent reviews for style only against your style guide. Move the writing rules you want flagged from your custom instructions into your style guide. For more, see [Style guides and custom instructions](how-gitbook-agent-enforces-your-style-guide.md#style-guides-and-custom-instructions).

### A review shows only a few issues

The Agent aims for around five flags per pass, starting with the most important. If more issues exist, it gives a count. Fix the flagged issues and request another review to see the rest.
