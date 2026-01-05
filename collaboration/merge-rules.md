---
description: Define requirements that must be met before change requests can be merged
icon: file-shield
---

# Merge rules

{% include "../.gitbook/includes/pro-and-enterprise-hint.md" %}

Merge rules allow you to define requirements that must be met before change requests can be merged, such as needing a review from a specific user, or requiring a subject or description for the change request.

These rules help maintain content quality and ensure proper review processes across your documentation workflow.

When you have merge rules configured, they’ll automatically evaluate change requests before they can be merged. If a rule isn’t satisfied, the merge will be blocked until the requirements are met.&#x20;

This provides an automated way to enforce your team’s collaboration and review standards.

## Using merge rules

You can configure merge rules at different levels to match your team’s workflow:

### Organization-level configuration

Organizations can set default merge rules that all spaces inherit. This provides consistency across multiple spaces while still allowing individual spaces to customize their rules as needed.

To configure merge rules for your organization, open the organization menu  at the top of the sidebar and choose **Settings** <picture><source srcset="../.gitbook/assets/10_01_25_10_01_25_settings_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/10_01_25_10_01_25_settings_icon_light.svg" alt=""></picture>. In the Settings screen, select **Merge rules** under the **Organization** section of the sidebar. Here you can specify merge rules for your entire organization.

Choose between unrestricted merging, or select from the list of presets to apply to change requests across your entire organization.

### Space-level configuration

Whether or not you have enabled organization-wide merge rules, each space can have its own merge requirements tailored to its content and team structure.

This gives you the flexibility to have stricter rules for important documentation and more relaxed rules for draft content.

When setting up merge rules for a space, you can choose to:

* **Inherit** merge rules from your organization
* **Define custom rules** specific to that space
* **Disable merge rules** entirely

{% hint style="info" %}
If you inherit organization rules, any changes to the organization’s merge rules will automatically apply to the space.
{% endhint %}

To configure merge rules for your organization, open the **Actions menu** <i class="fa-ellipsis">:ellipsis:</i> in the top left of the editor, and then select **Merge rules**. Here you can specify whether to inherit the merge rules from your organization or configure new ones specific to that space.

## Rule evaluation

### How rules work

When someone wants to merge a change request, GitBook will evaluate all the configured rules in order:

* All rules in a configuration must pass for a merge to be allowed
* Rules are evaluated in the order they appear in your configuration
* If any rule fails, the merge is blocked with an appropriate error message
* Rules with bypass capabilities can override previous failures

### Bypass rules

Some rules have bypass capabilities (like **Allow specified actors to bypass requirements**). These special rules can override other rule failures. If a bypass rule evaluates to true, the merge will be allowed even if other rules have failed.

## Best practices

When setting up merge rules, consider these recommendations:

* **Start simple**: Begin with basic rules like requiring at least one review.
* **Scale gradually**: Add more specific requirements as your team grows and workflows mature.
* **Use bypass carefully**: Only grant bypass permissions to trusted administrators.
* **Review regularly**: Adjust rules based on your team’s actual workflow patterns.
* **Test first**: When possible, test rule changes in a test space before applying to production spaces.

## Available rule types

### Review requirements

<table><thead><tr><th width="279.703125">Rule</th><th>Description</th></tr></thead><tbody><tr><td><strong>Require at least one review</strong></td><td>Ensures that at least one team member has reviewed the change request before it can be merged.</td></tr><tr><td><strong>Require all reviews approved</strong></td><td>All <strong>completed</strong> (not requested) reviews must be approvals. If any reviewer has requested changes or rejected the change request, the merge will be blocked.</td></tr><tr><td><strong>Require review by specified actors</strong></td><td>Requires approval from all specified users. You can select specific team members who must review and approve the change request before it can be merged.</td></tr><tr><td><strong>Require review by one of specified actors</strong></td><td>Requires approval from at least one of the specified users. This is useful when you have multiple qualified reviewers but only need one approval from the group.</td></tr><tr><td><strong>Require Docs Agent review (coming soon)</strong></td><td>Requires a review from the GitBook AI agent. This ensures automated quality checks are performed on content changes before merging.</td></tr></tbody></table>

### Change request requirements

<table><thead><tr><th width="279.703125">Rule</th><th>Description</th></tr></thead><tbody><tr><td><strong>Require up to date change request</strong></td><td>The change request must be current with the primary content branch. If the primary content has been updated since the change request was created, you’ll need to rebase or update it before merging.</td></tr><tr><td><strong>Require subject</strong></td><td>The change request must have a descriptive subject/title. Empty subjects will block the merge.</td></tr><tr><td><strong>Require description</strong></td><td>The change request must include a description explaining what changes were made and why.</td></tr></tbody></table>

### Advanced options

<table><thead><tr><th width="279.703125">Rule</th><th>Description</th></tr></thead><tbody><tr><td><strong>Allow specified actors to bypass requirements</strong></td><td>You can designate specific users who are allowed to bypass all other merge rule requirements. This is useful for administrators or emergency situations where rules need to be overridden.</td></tr><tr><td><strong>Custom expression</strong></td><td>You can create advanced merge rules using custom JavaScript expressions. This allows you to define complex logic based on the evaluation context, with access to properties of the change request, reviews, and the user attempting to merge.</td></tr></tbody></table>

#### Custom Expressions

When you create a custom expression, it will be evaluated each time someone tries to merge a change request. If the expression returns `true`, the merge is allowed. If it returns `false`, the merge is blocked.

{% hint style="info" %}
Custom expressions support standard JavaScript syntax (ES2022) and have a maximum length of 1024 characters.
{% endhint %}

**Available context variables:**

* `changeRequest.subject` - The subject/title of the change request
* `changeRequest.description` - The description of the change request
* `changeRequest.outdated` - Whether the change request is outdated (boolean)
* `changeRequest.createdBy.id` - ID of the user who created the change request
* `reviews` - Array of review objects, each containing:
  * `reviews[].status` - Review status (`"approved"` or `"changes_requested"`)
  * `reviews[].reviewer.id` - ID of the reviewer
* `actor.id` - ID of the user attempting to merge

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
