---
description: Learn how to monitor changes, roll back to a previous point in time, and more.
---

# Version control

You can easily monitor all changes submitted to your content thanks to the `Activity` tab. Here, your changes are split into two sections: **Feed** – where you can see the day-to-day actions that have occurred within a given space, and **Change History** – where you can specifically track changes to your space's content.

{% hint style="info" %}
**Permissions**

Only Administrators can access the Activity tab to view actions and change history in a space.
{% endhint %}

## Feed <a href="#see-all-the-activities" id="see-all-the-activities"></a>

The space is feed is where you can get a bird's eye view of what's been going on in any given space. This is useful if you've been away from the action for a few days and want to catch up. It's also useful if you're curious about anything that's happened in the space, e.g., when a specific member was added to the space, or when [live edits](../getting-started/collaboration/live-edits.md#toggling-live-edit-on-or-off) were locked or unlocked.

![](../.gitbook/assets/app.gitbook-alpha.com\_o\_YNVh6VKj6PtILeXzO7M9\_home.png)

## Change History <a href="#see-the-activity-of-a-specific-draft" id="see-the-activity-of-a-specific-draft"></a>

The change history of a space is where you can specifically see actions that result in content changing. These include:

* When [live edits](../getting-started/collaboration/live-edits.md) have been made on the space.
* When a [change request](../getting-started/collaboration/change-requests.md) has been merged.
* When a Git Sync operation has been performed.

### Viewing specific changes

You can click on any item in the change history list to view your content at the point this change was made. This is very similar to how [change requests](../getting-started/collaboration/change-requests.md) are viewed.

![](<../.gitbook/assets/History View.png>)

### Rolling back to a previous version

Rolling back lets admins revert a space's content to a previous point in time. It's great if you've accidentally made a breaking change and need to quickly get back to the last 'working' version of your content.

Admin users can hit the 'Rollback' button while viewing a specific history item to roll the space back to this point in time.

{% hint style="info" %}
**Good to know:** no content is ever deleted on GitBook. All content is versioned and immutable.
{% endhint %}
