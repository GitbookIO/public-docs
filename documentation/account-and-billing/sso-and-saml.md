---
description: Set up single sign-on for your organization.
icon: building-lock
---

# SSO and SAML

{% hint style="info" %}
SAML SSO is available on the [Enterprise plan](https://www.gitbook.com/pricing).
{% endhint %}

Manually managing organization members works fine for smaller teams, but larger ones usually want something more automated. GitBook supports two approaches: a basic email-domain SSO, and a more complete SAML integration.

## Single sign-on via email domain

When you create or manage your organization, you can add a list of email domains allowed to access it. Anyone with a verified email address matching a configured domain can join your organization automatically.

Enable this in the **SSO** section of your organization's **Settings** — enter a comma-separated list of allowed email domains.

{% hint style="info" %}
Anyone who joins via an SSO email domain defaults to guest access. You can change their role at any time from the members section of your organization settings.
{% endhint %}

## SAML SSO

SAML SSO gives members access to GitBook through an identity provider (IdP) of your choice. GitBook integrates with your existing IdP so employees can log in with the same credentials and experience as your other service providers.

With SSO enabled, employees log in through your IdP's interface instead of GitBook's login page — their browser is then forwarded to GitBook. The IdP grants access, and GitBook's own login mechanism is deactivated, shifting authentication security to your IdP.

### Prerequisites

* Your identity provider must support the **SAML 2.0** standard.
* You need administrative permission on the IdP.
* You need to be an [organization admin](../learn/collaboration/roles-permissions-inheritance.md) on the GitBook organization where you're setting up SAML.

### Set up on GitBook

After configuring SSO on your IdP, enter its metadata in GitBook. On success, admins see a confirmation dialog along with the SSO login URL for end users.

{% hint style="warning" %}
GitBook doesn't send announcement emails when setup completes — it's the administrator's responsibility to notify employees and share the login URL.
{% endhint %}

{% hint style="info" %}
Organization admins can still sign in with non-SSO methods (Google, GitHub, or email), even with **Enforce SSO** enabled. This is expected — it prevents a lockout from your organization after a bad SSO setup, since admins can always sign in to remove or fix SSO settings.
{% endhint %}

You'll need the following from your IdP metadata to register a SAML provider:

* A **label** — anything you like, shown on the login page
* An **entity ID**
* A **Single Sign On URL**
* An **X.509 certificate** — copy and paste the whole certificate

### Set up on the IdP

Most SAML 2.0 identity providers need the same information about the service provider (GitBook). These values are specific to your GitBook organization, available under **Settings → SSO**, and can usually be copied directly into your IdP.

GitBook requires the **NameID** to contain the user's email address — technically, `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress` as the Name-ID format. Many providers (like Google) let you set this via an **EMAIL** format option.

#### Custom attributes

GitBook pulls the following custom attributes from the SAML assertion response when creating a user:

| Field | Description |
|---|---|
| `first_name` | Combined with `last_name` to produce the user's display name in GitBook |
| `last_name` | Combined with `first_name` to produce the user's display name in GitBook |

### Creating end-user accounts

To add members, create accounts for them in your IdP. The first time a new member logs in to GitBook via the IdP, GitBook creates their account automatically, with organization-member access.

{% hint style="danger" %}
Setup requires lowercase email addresses — don't use mixed case.
{% endhint %}

### Removing accounts

Removing a member from the IdP prevents them from signing in to their GitBook account, but doesn't remove the account from GitBook itself. Also remove the account from the GitBook organization directly.

### Controlling access

Once SAML SSO is set up, the IdP controls who can access your GitBook account.

### Security notice

If someone has an existing GitBook account under the same email address your IdP returns, but isn't a member of the organization they're trying to sign into, GitBook won't automatically add them for security reasons. They have two options:

1. Delete the existing GitBook account, then log in to the organization with SAML — GitBook creates a new account and adds them to the organization.
2. Ask an admin to invite them instead:
   * Without **Enforce SSO** enabled, an admin can invite them from the organization's Members page.
   * With **Enforce SSO** enabled, an admin needs to use GitBook's `invites` API endpoint:
     ```
     curl --request POST --header "Authorization: Bearer <your_access_token>" --url "https://api.gitbook.com/v1/orgs/<org_id>/invites" --header 'Content-Type: application/json' --data-raw '{ "sso": true, "role": "<role>", "emails":["<email>"] }'
     ```

## SSO members vs. non-SSO members

Users who created a GitBook account with an email address that's also used in your SAML identity provider — or who joined your organization before SAML was configured — may see their SSO login blocked with a message prompting them to "Log in with your existing credentials."

### Why this happens

GitBook's SAML implementation is security-first. If an account exists for `bob@company.com` and Bob later logs in through company SAML, GitBook can't verify that the email address returned by the IdP is the same, trusted `bob@company.com` — so it can't automatically authenticate him as that account.

To avoid silently creating a second account for the same email address, GitBook tells the user to log in with their original account instead, and leaves the resolution to the organization administrator. Enabling SSO on a user's account is how an admin tells GitBook that the relationship between that account's email and the SAML identity can be trusted.

### Remediation

**If the user is already a member of the organization**, an admin can either:

* Enable SSO on their organization membership from the admin dashboard — their next login will use the SSO flow, or
* Have the user log in with their original credentials (for example, **Continue with email** for a sign-in link). SSO login isn't automatically enabled this way — an admin still needs to enable it explicitly afterward.

**If the user isn't yet a member of the organization**, an admin should invite their email address from the admin dashboard — SSO login can then be enabled directly for their account.

### Enabling SSO login for members

Organization administrators enable SSO login for members by linking their accounts to SSO. This tells GitBook the account can be trusted as connected to the corresponding identity in your provider.
