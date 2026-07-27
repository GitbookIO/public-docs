---
description: Require reviews and other conditions before a change request can merge.
---

# Merge rules

{% hint style="info" %}
Merge rules are available on Premium and Ultimate plans.
{% endhint %}

Merge rules let you define requirements that must be met before a change request can merge — like requiring review from a specific person, or requiring a subject or description. They help maintain content quality and enforce review standards across your documentation workflow.

Configured rules automatically evaluate every change request before it can merge. If a rule isn't satisfied, the merge is blocked until the requirements are met.

## Using merge rules

Configure merge rules at different levels to match your team's workflow.

### Organization-level configuration

Organizations can set default merge rules that all sections inherit, giving you consistency across sections while still letting individual sections customize as needed.

To configure them, go back to your organization **Home** and click **Settings**, under **Admin** in the sidebar, then **Merge rules** under the **Organization** group. Choose unrestricted merging, or select from the available presets to apply across your entire organization.

### Section-level configuration

Whether or not organization-wide rules are enabled, each section can have its own requirements tailored to its content and team. This lets you have stricter rules for important documentation and more relaxed rules for drafts.

When setting up merge rules for a section, choose to:

* **Inherit** rules from your organization
* **Define custom rules** specific to that section
* **Disable merge rules** entirely

{% hint style="info" %}
If you inherit organization rules, changes to the organization's merge rules automatically apply to the section.
{% endhint %}

To configure a section's merge rules, open the **Actions menu** in the top left of the editor and click **Merge rules**.

## Rule evaluation

### How rules work

When someone tries to merge a change request, GitBook evaluates all configured rules in order:

* All rules in a configuration must pass for the merge to be allowed.
* Rules are evaluated in the order they appear in your configuration.
* If any rule fails, the merge is blocked with an appropriate error message.
* Rules with bypass capabilities can override previous failures.

### Bypass rules

Some rules (like **Allow specified actors to bypass requirements**) can override other rule failures — if a bypass rule evaluates to true, the merge is allowed even if other rules failed.

## Best practices

* **Start simple** — begin with basic rules like requiring at least one review.
* **Scale gradually** — add more specific requirements as your team and workflows mature.
* **Use bypass carefully** — only grant bypass permissions to trusted administrators.
* **Review regularly** — adjust rules based on your team's actual workflow patterns.
* **Test first** — when possible, test rule changes in a test section before applying to production.

## Available rule types

### Review requirements

| Rule | Description |
|---|---|
| **Require at least one review** | At least one team member must review the change request before it can merge. |
| **Require all reviews approved** | All completed (not just requested) reviews must be approvals — a requested-changes or rejection blocks the merge. |
| **Require review by specified actors** | Requires approval from every specified user. |
| **Require review by one of specified actors** | Requires approval from at least one of the specified users — useful with multiple qualified reviewers where only one approval is needed. |
| **Require Docs Agent review** *(coming soon)* | Requires a review from the GitBook AI agent, for automated quality checks before merging. |

### Change request requirements

| Rule | Description |
|---|---|
| **Require up to date change request** | The change request must be current with the primary content branch — rebase or update it before merging if main has changed. |
| **Require subject** | The change request must have a descriptive subject/title; empty subjects block the merge. |
| **Require description** | The change request must include a description explaining what changed and why. |

### Advanced options

| Rule | Description |
|---|---|
| **Allow specified actors to bypass requirements** | Designated users can bypass all other merge rule requirements — useful for admins or emergencies. |
| **Custom expression** | Define complex logic with a custom JavaScript expression, with access to the change request, its reviews, and the user attempting to merge. |

#### Custom expressions

A custom expression is evaluated each time someone tries to merge a change request. If it returns `true`, the merge is allowed; if `false`, it's blocked.

{% hint style="info" %}
Custom expressions support standard JavaScript syntax (ES2022) and have a maximum length of 1024 characters.
{% endhint %}

**Available context variables:**

* `changeRequest.subject` — the change request's subject/title
* `changeRequest.description` — the change request's description
* `changeRequest.outdated` — whether the change request is outdated (boolean)
* `changeRequest.createdBy.id` — ID of the user who created the change request
* `reviews` — array of review objects, each containing:
  * `reviews[].status` — review status (`"approved"` or `"changes_requested"`)
  * `reviews[].reviewer.id` — ID of the reviewer
* `actor.id` — ID of the user attempting to merge

**Common expression examples:**

{% code title="Require multiple approved reviews" %}
```javascript
reviews.filter(r => r.status === "approved").length >= 2
```
{% endcode %}

{% code title="Require approval from specific user" %}
```javascript
reviews.some(r => r.reviewer.id === "harry" && r.status === "approved")
```
{% endcode %}

{% code title="Require description for urgent changes" %}
```javascript
!changeRequest.subject.includes("[URGENT]") || !!changeRequest.description
```
{% endcode %}

{% code title="Allow self-merge only for minor changes" %}
```javascript
changeRequest.createdBy.id === actor.id ? changeRequest.subject.startsWith("[minor]") : true
```
{% endcode %}
