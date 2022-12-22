---
description: >-
  Auto-provision users and teams from your company directory with directory sync
  (backed by SCIM)
---

# SCIM & directory sync

Directory sync allows you to automatically provision/deprovision users and teams from your company directory into your GitBook organization.

As users join your directory, they will be created and added to your GitBook organization.

You can also have teams in GitBook synchronize to your directory groups, and have all user memberships synchronize automatically.

{% hint style="warning" %}
Directory sync is not currently publicly available in GitBook. If your organization is struggling to manually manage its members and teams in GitBook, we recommend using [the GitBook API](https://developer.gitbook.com/api/resources/organizations/members) to programmatically add/remove members and teams as your directory changes. Most identity providers offer ways to hook into these events.

If you have further questions, please [get in touch](mailto:sales@gitbook.com).
{% endhint %}
