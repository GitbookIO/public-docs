---
description: Security advisories, fixes, and access and compliance changes in GitBook
icon: shield-halved
---

# Security bulletins

<a href="https://gitbook.com/docs/policies/privacy-and-security/security/reporting-bugs-and-vulnerabilities" class="button primary" data-icon="bug">Report a vulnerability</a><a href="https://gitbook.com/docs/policies/privacy-and-security/security" class="button secondary" data-icon="shield-halved">How GitBook handles security</a>

<h3 align="center">All bulletins</h3>

<p align="center">Every security-related update, newest first.</p>

{% updates format="full" %}
{% update date="2026-11-25" tags="access-identity" %}
## Read-only personal API tokens and IP restrictions

When you create a personal API token, you can choose its access: read only, or the same permissions as your account. The API refuses a read-only token for any operation that isn't safe for read-only access, which limits what an exposed token can do. Existing tokens keep their current access.

* Allow or deny specific IP ranges for a token, so it's refused from addresses you don't trust.
* When you rotate a token, keep the previous secret working for one hour or 24 hours while you update your integrations, or stop it right away.
* The token list shows each token's access level, time left, and a single status: active, expired, or revoked. A details dialog shows its dates and IP rules.
* GitBook improved the security of how tokens are stored.

First published in [Product updates, November 25, 2026](../).
{% endupdate %}

{% update date="2026-11-25" tags="access-identity" %}
## Space creators become Admin

Whoever creates a space is now its [Admin](https://gitbook.com/docs/collaborate/member-management/permissions-and-inheritance#space-creators), including drafts that site Editors add as a section or variant, so they can set up Git Sync on them. For a space created in a site, the Admin role ends if its creator is removed from the site. Spaces created before this change keep their current permissions.

First published in [Product updates, November 25, 2026](../).
{% endupdate %}

{% update date="2026-11-25" tags="access-identity" %}
## Published change request previews off by default for new sites

New sites have published change request previews turned off by default. When a site turns them off, links to a published change request or revision redirect to the site preview. Signed-in members can still preview changes.

First published in [Product updates, November 25, 2026](../).
{% endupdate %}

{% update date="2026-11-25" tags="access-identity" %}
## Limit AI Assistant to a visitor audience

Site admins can limit [AI Assistant](https://gitbook.com/docs/ai-for-your-readers/gitbook-ai-assistant) and AI search to visitors who match an [adaptive content](https://gitbook.com/docs/publish/adaptive-content/adapting-your-content) condition, for example only signed-in visitors.

First published in [Product updates, November 25, 2026](../).
{% endupdate %}

{% update date="2026-11-25" tags="audit-compliance" %}
## Audit logs record collection changes

Organization [audit logs](https://gitbook.com/docs/account-and-billing/audit-logs/actions) record collection creation, settings changes, moves, transfers, and deletion.

First published in [Product updates, November 25, 2026](../).
{% endupdate %}

{% update date="2026-11-25" tags="access-identity" %}
## Sign in with a passkey

Add a passkey to your GitBook account and use it to sign in instead of a password or email link. You can sign in with a passkey from the first sign-in screen, without entering your email.

* Save a passkey on this device or in a password manager, on a phone or tablet, or on a security key.
* Add, rename, and remove passkeys in your account settings.
* Use a passkey to confirm it’s you before sensitive account changes.
* GitBook emails you when a passkey is added to or removed from your account.

You need a verified email address to add a passkey. Members who must sign in with SSO can’t add one.

First published in [Product updates, November 25, 2026](../).
{% endupdate %}

{% update date="2026-11-11" tags="access-identity" %}
## Expiration dates for personal API tokens

When you create a personal API token, you can choose when it stops working: 7, 30, 60, or 90 days, a custom date, or never. New tokens expire after 90 days by default. You can also set an expiration date through the API with the `expiresAt` field.

First published in [Product updates, November 11, 2026](../).
{% endupdate %}

{% update date="2026-11-04" tags="security" %}
## Thanks to ACylaa for security research

Thank you to [ACylaa](https://github.com/ACylaa) for responsibly reporting security issues to GitBook. The reported issues are fixed.

First acknowledged in [Product updates, October 21, 2026](../) and [Product updates, November 4, 2026](../).
{% endupdate %}

{% update date="2026-10-21" tags="access-identity" %}
## Invites restricted in SAML-enforced organizations

In organizations that enforce single sign-on with SAML, you can add only existing members to sites and spaces. You can’t invite new people from there.

First published in [Product updates, October 21, 2026](../).
{% endupdate %}

{% update date="2026-09-30" tags="audit-compliance" %}
## Audit logs cover more changes and mark Support actions

* Enterprise audit logs record changes to agent instructions, custom fonts, OpenAPI specifications, and translations.
* Actions GitBook Support takes on your behalf are clearly marked.
* Sites published or unpublished during immediate billing changes are now recorded.

First published in [Product updates, September 30, 2026](../).
{% endupdate %}

{% update date="2026-09-22" tags="audit-compliance" %}
## Audit logs record redirect and channel changes

* Enterprise audit logs record site redirect and channel configuration changes.
* Member removals made during immediate billing plan changes are now recorded.

First published in [Product updates, September 22, 2026](../).
{% endupdate %}

{% update date="2026-09-16" tags="audit-compliance,access-identity" %}
## Audit log export, and GitBook Agent uses your permissions

* Export your organization’s filtered audit logs as a CSV file.
* Audit logs record custom-domain validation outcomes.
* Anyone in your organization can use GitBook Agent with their own permissions. It reads what they can read, and edits and comments only where they can.

First published in [Product updates, September 16, 2026](../).
{% endupdate %}

{% update date="2026-09-02" tags="audit-compliance" %}
## Audit log records SSO changes

The audit log records SAML provider changes and changes to organization SSO enforcement.

First published in [Product updates, September 2, 2026](../).
{% endupdate %}

{% update date="2026-08-27" tags="access-identity" %}
## Site-level permissions

Choose who can complete site-based actions and who can only edit site content, across an entire site. The same controls apply whether people edit by hand or through agents. See [site-level permissions](https://gitbook.com/docs/manage-your-site/site-permissions).

First published in [Product updates, August 27, 2026](../).
{% endupdate %}

{% update date="2026-08-06" tags="access-identity" %}
## Visitor token revalidation and bulk invite limits

* On authenticated sites, visitor tokens revalidate without a redirect, so readers stay on the same page.
* Bulk email invites are limited to 10 at a time, and the invite dialog explains SSO restrictions.

First published in [Product updates, August 6, 2026](../).
{% endupdate %}

{% update date="2026-07-07" tags="access-identity" %}
## Private agent conversations

Agent conversations in change requests can be marked private, so only the people who need them can see them.

First published in [Product updates, July 7, 2026](../).
{% endupdate %}

{% update date="2026-06-30" tags="access-identity" %}
## Clearer OAuth consent screen

The OAuth consent screen explains requested permissions more clearly before you grant access.

First published in [Product updates, June 30, 2026](../).
{% endupdate %}

{% update date="2026-05-07" tags="access-identity" %}
## Site permissions take precedence over inherited permissions

For content linked to a site, site-level permissions take precedence over permissions inherited from the organization or parent collection. Space-level overrides for individual users and teams still take precedence over everything else.

First published in [Product updates, May 7, 2026](../).
{% endupdate %}

{% update date="2026-03-19" tags="access-identity" %}
## Site-level permissions introduced

Admins can set permissions at the site level and control who can view and edit site content in one place.

First published in [Product updates, March 19, 2026](../).
{% endupdate %}

{% update date="2026-02-23" tags="advisory" %}
## GBSB-2026-001: Site customization visible without edit permission

| Field           | Detail                                 |
| --------------- | -------------------------------------- |
| Status          | Fixed in the February 23, 2026 release |
| Affected        | Site customization settings            |
| Action required | None. The fix is on GitBook’s side.    |
| Class           | Missing authorization (CWE-862)        |
| Credit          | —                                      |

Members without edit permissions could open site customization options, but not save them. They now see an “Access denied” message.

First published in [Product updates, February 23, 2026](../).
{% endupdate %}

{% update date="2025-11-11" tags="advisory" %}
## GBSB-2025-001: Content tokens could reach private API endpoints

| Field           | Detail                                      |
| --------------- | ------------------------------------------- |
| Status          | Fixed in the November 11, 2025 release      |
| Affected        | Content tokens used by published docs sites |
| Action required | None. The fix is on GitBook’s side.         |
| Class           | Incorrect authorization (CWE-863)           |
| Credit          | —                                           |

Content tokens for the published docs platform could access private API endpoints.

First published in [Product updates, November 11, 2025](../2025-product-updates.md).
{% endupdate %}

{% update date="2025-06-17" tags="access-identity" %}
## Visitor authentication renamed to authenticated access

Visitor authentication is now called authenticated access throughout the app and the docs.

First published in [Product updates, June 17, 2025](../2025-product-updates.md).
{% endupdate %}

{% update date="2024-08-27" tags="access-identity" %}
## Default team per SSO provider

Set a default team for each SSO provider, so everyone who signs in through that provider joins the team automatically.

First published in [Product updates, August 27, 2024](../2024-product-updates.md).
{% endupdate %}

{% update date="2024-08-08" tags="access-identity" %}
## Multi-factor authentication for everyone

Multi-factor authentication (MFA) is available to every GitBook user.

First published in [Product updates, August 8, 2024](../2024-product-updates.md).
{% endupdate %}

{% update date="2024-08-05" tags="access-identity,breaking-change" %}
## Authenticated access API endpoints deprecated

With the release of docs sites, space-level API endpoints for publishing, share links, and authenticated access were deprecated. Use the matching site endpoints with the site ID instead.

First published in [Product updates, August 5, 2024](../2024-product-updates.md).
{% endupdate %}

{% update date="2024-07-18" tags="access-identity" %}
## Multi-factor authentication rollout begins

GitBook began rolling out optional multi-factor authentication for signing in.

First published in [Product updates, July 18, 2024](../2024-product-updates.md).
{% endupdate %}

{% update date="2024-01-10" tags="access-identity" %}
## Visitor authentication through integrations

Set up visitor authentication without a custom backend by installing an integration that authenticates users and generates JWTs.

First published in [Product updates, January 10, 2024](../2024-product-updates.md).
{% endupdate %}

{% update date="2023-10-05" tags="audit-compliance" %}
## SOC 2 and ISO 27001 certification

GitBook achieved SOC 2 and ISO 27001 security certifications. [Read the blog post](https://www.gitbook.com/blog/gitbook-security-soc2-iso27001).

First published in [Product updates, October 5, 2023](../2023-product-updates.md).
{% endupdate %}

{% update date="2023-09-27" tags="advisory" %}
## GBSB-2023-001: Email changes in SSO-enforced organizations

| Field           | Detail                                                   |
| --------------- | -------------------------------------------------------- |
| Status          | Fixed in the September 27, 2023 release                  |
| Affected        | Account email settings in organizations that enforce SSO |
| Action required | None. The fix is on GitBook’s side.                      |
| Class           | Improper access control (CWE-284)                        |
| Credit          | —                                                        |

Members of an organization that enforces SSO could change their email address.

First published in [Product updates, September 27, 2023](../2023-product-updates.md).
{% endupdate %}

{% update date="2023-08-22" tags="access-identity" %}
## Enforce SSO across your organization

A setting makes SSO mandatory across your organization. The member list shows each member’s SSO status.

First published in [Product updates, August 22, 2023](../2023-product-updates.md).
{% endupdate %}

{% update date="2022-08-04" tags="access-identity" %}
## Default role for email-domain SSO

Choose the role members get when they sign in through email-domain SSO. It used to be fixed to Editor.

First published in [Product updates, August 4, 2022](../2022-and-earlier-product-updates.md).
{% endupdate %}
{% endupdates %}
