---
description: Reference for personal account and organization settings.
---

# Personal and organization settings

Account and organization settings share one screen, grouped into **Account** and **Organization** in the left-hand sidebar. To get there, go back to your organization **Home** and click **Settings**, under **Admin** in the sidebar. Click **Back to app** to return to your content.

## Personal (account) settings

Your personal settings live under **Account**.

<details>

<summary>General</summary>

**Your profile** — update your profile picture and full name.

**Login details** — update the email address and password used to log into GitBook. If you created your account on or after October 9, 2021, your account doesn't have a password — you'll use a magic link to sign in instead.

**Third-party login** — you can also log in with Google and/or GitHub credentials.

**Publishing** — each published section in your personal library gets a domain in two parts: `[something].gitbook.io` (your GitBook subdomain) and `/[spaceURL]` (set within that section's own settings). You can update the subdomain here, along with the default content shown when visitors navigate to it directly.

**Preferences** — choose your interface theme (dark, light, or system). This only affects your experience in the GitBook app — it doesn't change your published content.

**Troubleshooting** — optionally enable advanced logs, which help our team troubleshoot issues more effectively.

**Account actions** — sign out, or delete your account.

{% hint style="danger" %}
Deleting your account is permanent — all associated data is deleted too.
{% endhint %}

</details>

<details>

<summary>Notifications</summary>

Notifications tell you about activity on GitBook from sections owned by you or an organization you're a member of. You can receive them in-app and/or by email — enable or disable each type from this settings screen.

**App notifications** appear at the top of the sidebar. In the notifications pop-up, two icons in the top-right corner let you mark everything as read or jump to your notification settings.

**Email notifications** are on by default. GitBook sends one email per notification type, to the email address on your personal account, from `no-reply@gitbook.io via sendgrid.net`.

**Notification types** currently include:

* Sections — comments posted in a section
* Change requests — reviews requested by collaborators
* Comments — replies to your comments
* Mentions — when you're mentioned in a comment
* Organizations — upgrade requests from collaborators

<details>

<summary>Not receiving an expected email notification?</summary>

* Check your spam folder or other protection mechanisms — make sure `no-reply@gitbook.io` isn't blocked.
* Emails that bounce repeatedly get automatically blocked by our mail service — wait it out if you're aware of a temporary delivery issue.
* Double-check you've enabled the right notification type in your [notification settings](https://app.gitbook.com/account/notification).
* Confirm you're checking the email address on your [personal account](https://app.gitbook.com/account).
* If all else fails, [contact support](../resources/get-support.md) with the email address you expect the notification at, the notification type, and exactly what should have triggered it, plus links to anything relevant.

</details>

</details>

<details>

<summary>Organizations</summary>

Your personal account can belong to any number of organizations — this tab is a shortcut to each one's organization settings. You can also create a new organization from here.

</details>

<details>

<summary>Developer tools</summary>

Manage and create access tokens for the [GitBook API](https://developer.gitbook.com/).

</details>

### Reset or set a password

If your account was created after October 10, 2021, it doesn't have a password — log in with a magic link instead:

1. Visit [https://app.gitbook.com](https://app.gitbook.com).
2. Enter the email address on your account and click **Continue**.
3. Click **Send a link** (check your spam folder if it doesn't arrive).

If you do want to reset a password:

1. Visit [https://app.gitbook.com](https://app.gitbook.com).
2. Follow the **Forgot your password?** link at the bottom of the page.
3. Enter the email address on your account and click **Send a link** (check your spam folder if it doesn't arrive).

## Organization settings

{% hint style="info" %}
Only Admins in an organization can access organization settings.
{% endhint %}

Manage your GitBook organization's members, sign-in methods, merge rules, billing, and plans.

<details>

<summary>General</summary>

**Organization profile** — update your organization's logo and name.

**GitBook AI features** — [GitBook AI](../learn/gitbook-ai/ai-search.md)-powered search lets members ask questions about your content in natural language. You can also enable GitBook AI for published content in your site's [customization settings](../learn/customization/README.md).

**Actions** — delete your organization from this section.

{% hint style="danger" %}
Deleting an organization is permanent — GitBook deletes all associated data. To keep organization-owned content, [move it to another organization](../learn/creating-content/content-structure.md) first.
{% endhint %}

</details>

<details>

<summary>Members</summary>

Add and remove [members](../learn/collaboration/invite-and-manage-members.md). You can also update each member's [role](../learn/collaboration/roles-permissions-inheritance.md).

</details>

<details>

<summary>Merge rules</summary>

Control how change requests are reviewed and merged across your organization. Organization rules apply to every section by default, and each section can inherit, replace, or disable them. Learn more about [merge rules](../learn/collaboration/change-requests/merge-rules.md).

</details>

<details>

<summary>GitBook Agent</summary>

Manage organization-level settings for [GitBook Agent](../learn/gitbook-ai/agent/README.md).

</details>

<details>

<summary>Integrations</summary>

Check which integrations are installed for your organization, and [install new ones](../learn/custom-components/install-and-manage.md).

</details>

<details>

<summary>OpenAPI</summary>

Manage the OpenAPI specifications your organization's sites use for API references.

</details>

<details>

<summary>Translations</summary>

Manage organization-wide settings for auto-translations.

</details>

<details>

<summary>Invite links</summary>

Create and manage links that let people join your organization.

</details>

<details>

<summary>Teams</summary>

[Teams](../learn/collaboration/invite-and-manage-members.md) group organization members — grant access to members of a team at once.

</details>

<details>

<summary>SSO</summary>

**Email domains** — for each domain you add, people with an email address on that domain can access the organization after creating a GitBook account. Choose their default [role](../learn/collaboration/roles-permissions-inheritance.md).

**SAML** — on the Enterprise plan, configure SAML single sign-on with your identity provider. See [SSO and SAML](sso-and-saml.md), or [contact sales](mailto:sales@gitbook.com) to upgrade to Enterprise.

</details>

<details>

<summary>Billing</summary>

View your current plan and switch plans. Toggle between annual pricing (2 months free) and monthly pricing, then use the upgrade or downgrade button under each plan.

See [Plans and billing policy](plans-and-billing-policy.md) to learn how charges are calculated when you change plans mid-cycle.

Click **Manage Billing** to open Stripe, where you manage your payment method and billing information. You can also [cancel your plan](cancel-a-subscription.md) — if you renew before the billing period ends, your plan continues without interruption.

</details>
