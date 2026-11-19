---
description: >-
  Review who changed what across your GitBook organization, filter events, and
  export them as CSV.
---

# Audit logs

{% hint style="info" %}
Audit logs are available on the [Enterprise plan](https://www.gitbook.com/pricing). Only organization [admins](../../collaborate/member-management/roles.md) can view them.
{% endhint %}

Audit logs record changes made across your organization: who made each change, when, what they did, and what it affected. Use them to answer security and compliance questions, trace a configuration change back to the person or workflow behind it, or confirm what happened during an incident.

## Open audit logs

Go to **Settings → Audit logs**.

Each row in the table is one event, newest first, with these columns:

* **Time:** when the event happened.
* **Action:** what changed, such as **Updated site integration** or **Started Git Sync**.
* **Target:** the site, space, member, or other resource the action affected.
* **Actor:** the member, integration, or automated workflow that made the change. When GitBook Support acts on a member’s behalf, the event shows an **Impersonated** badge.
* **Source:** where the change came from, such as the app, an integration, or a workflow.

## What audit logs record

Audit logs cover administrative and configuration changes, including:

* **Organization administration:** organization settings, merge rules, SAML and SCIM configuration, SSO enforcement, invite links, teams, billing and plan changes, translation settings, and custom fonts.
* **Members:** joins, including members added by their first SAML sign-in, role changes, SSO assignments, and removals. An accepted email invitation is recorded as the member joining.
* **Sites:** structure, settings, customization, publishing, AI and MCP server settings, and user and team permissions.
* **Spaces:** creation, duplication, deletion, restoration, settings, and default access.
* **Collections:** creation, settings, moves, ownership transfers, and deletion.
* **Access and routing:** site share links, custom domains attached to sites, redirects, and verified organization domains.
* **Integrations and workflows:** integrations connected to sites, Git Sync for sites, OpenAPI processing, and context sync, including changes these workflows make in the background.

Coverage may expand as GitBook adds more actions. For every action audit logs can record, see [Audit log actions](actions.md).

Audit logs don’t record changes to page content, page views, or file downloads. To review edits to content, use [version control](../../create-content/version-control.md).

## Filter events

The **Time**, **Action**, and **Actor** columns each have a filter in their header.

* **Time:** show events from the last 24 hours, 7 days, or 30 days, or pick a custom date range.
* **Action:** search for and select one or more actions.
* **Actor:** select members, or automated actors such as Git Sync, OpenAPI processing, context sync, custom domain validation, and GitBook Agent.

Click **Clear filters** to show all events again.

## View event details

Click a row to open the event in a side panel. The panel shows:

* Changed values as before → after. For settings whose values aren’t recorded, the panel lists the setting names.
* Technical IDs for the event, actor, target, and related workflow, under **Event information**. Use the copy buttons to share them with GitBook Support.

Use the up and down buttons to move between events on the current page. Press <kbd>Esc</kbd> to close the panel.

Each event has its own URL. Copy the URL from your browser’s address bar while an event is open to share a link to it with another admin.

## Export events as CSV

1. Apply any filters you want. The export includes only the events that match.
2. Click **Export as CSV**.

An export includes up to 10,000 events. To export more, narrow the **Time** filter and export your history in batches.

The CSV includes the time, action, actor, impersonator, source, target, and event ID for each event.

## Access audit logs with the API

To pull audit events into your own tools, such as a SIEM, use the [List organization audit events](https://gitbook.com/docs/developers/gitbook-api/api-reference/organizations/list-organization-audit-events) endpoint in the GitBook API.

## Retention

GitBook keeps audit events for 1 year.

## If you change plans

GitBook keeps recording audit events after an organization leaves the Enterprise plan. Admins can’t view or export them until the organization returns to Enterprise. When it does, events from the last year are available again.
