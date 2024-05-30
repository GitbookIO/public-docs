# Content creation FAQ

## What browsers are supported by GitBook?

GitBook supports the current versions of [Chrome](https://www.google.com/chrome/), [Firefox](http://www.mozilla.org/firefox/), [Safari](http://www.apple.com/safari/), and [Microsoft Edge](https://www.microsoft.com/en-us/windows/microsoft-edge).

## Does GitBook support RTL languages?

We have RTL support in mind, but it’s not yet ready. For now, only paragraphs and headings will automatically detect RTL text and adapt its layout. Lists and other content blocks are not aligned properly. Also, you may have noticed a poor font quality being used for your language.

## Is there a limit on the documentation import size?

GitBook currently has the following limits for imported content:

* The maximum number of pages that can be uploaded in a single import is **20.**
* The maximum number of files (images etc.) that can be uploaded in a single import is **20.**

## **How can I export my content?**

We recommend exporting your content in Markdown format by enabling [GitHub or GitLab sync](../../integrations/git-sync/). You can also export your content via PDF but you may hit some limits in case of larger spaces.

## Can I move a page from one space to another?

We do not support moving single pages between spaces at this time. We recommend you copy and paste the content as needed. In cases of larger content reorganization where you will need to move a number of pages between spaces, we recommend you contact our support team who can guide you through moving your content via GitHub or GitLab sync.

{% hint style="info" %}
To easily select multiple blocks you can use block selection mode, which is enabled by hitting the esc key. To copy an entire page of text, you can hit esc to enable block selection and then hit cmd + a to select all content on a page and then copy and paste to a new space.
{% endhint %}

## Can I move a space between organizations?

Yes, you can! [Read more about how to move a space.](../../content-editor/editor/content-structure/what-is-a-space.md#move-a-space)

## Can I export my content in Markdown format?

We don't have the ability to export pages as Markdown in the GitBook app, but you can sync a space to GitHub or GitLab and generate a markdown export that way. Note that there might be a few exceptions where customized blocks appear as HTML.

## How do I revert to the previous version of my content?

Admins and creators can click the **rollback** button while viewing a specific history item to[ roll the space back ](../../content-editor/activity-history.md#rolling-back-to-a-previous-version)to this point in time.

## Do you support offline contributions?

Not at the moment!

## Do you have a mobile or a desktop app?

No, sorry.
