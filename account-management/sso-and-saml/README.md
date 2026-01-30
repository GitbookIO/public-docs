---
description: Learn how to share your GitBook content via SSO & SAML
icon: building-lock
---

# SSO & SAML

{% include "../../.gitbook/includes/enterprise-hint.md" %}

While manually managing your organization members is fine for smaller teams or folks who want tonnes of control, sometimes you just need to open things up in a more automated way. GitBook allows you to configure this in a couple of ways, through a basic email domain SSO, and a more complex SAML integration.

## Single sign-on via email domain

When you create or manage your organization, you can add a list of email domains that you want to allow to access your GitBook organization. This means that anyone with a verified email address that matches your configured SSO domains will be allowed to join your organization.

You can enable email domain SSO in the **SSO** section of your organization’s **Settings**; enter a comma-separated list of email domains you’d like to allow SSO access for and you’re good to go.

<figure><img src="../../.gitbook/assets/25_01_10_sso.svg" alt="A GitBook screenshot showing how to configure SSO"><figcaption><p>Set up SSO for your organization.</p></figcaption></figure>

{% hint style="info" %}
Anyone who joins via an SSO email domain will default to guest access, you can change their role at any time in the members section of your organization settings.
{% endhint %}

**SAML-based Single Sign-On** (SSO) gives members access to GitBook through an identity provider (IdP) of your choice.‌

GitBook easily integrates with your existing identity provider (IdP) so you can provide your employees with single sign-on to GitBook using the same credentials and login experience as your other service providers.‌

By using SSO, your employees will be able to log into GitBook using the familiar identity provider interface, instead of the GitBook login page. The employee’s browser will then forward them to GitBook. The IdP grants access to GitBook when SSO is enabled and GitBook’s own login mechanism is deactivated. In this way, authentication security is shifted to your IdP and coordinated with your other service providers.‌​

## ​Prerequisites for SSO with GitBook <a href="#prerequisites-for-sso-with-gitbook" id="prerequisites-for-sso-with-gitbook"></a>

* Your company’s identity provider (IdP) must support the **SAML 2.0** standard.
* You must have administrative permission on the IdP.
* You must be an administrator of the GitBook organization you want to set SAML up on.

### ​Set up on GitBook <a href="#setup-on-gitbook" id="setup-on-gitbook"></a>

You must be an [organization admin](../member-management/roles.md#admin) to enable SSO for your GitBook organization.‌

After configuring SSO on your IdP, you will be able to enter metadata. When the setup is successful, administrators will see a confirmation dialog and the URL of the SSO login for end-users will be displayed. **GitBook does not send announcement emails when set up is complete**. It is the responsibility of the administrator to notify company employees (and convey the login URL to them) so they can access GitBook via SSO.‌

{% hint style="info" %}
Organization admins can still sign in with non-SSO methods, so you may still see Google, GitHub, or email buttons. This is expected, even with **Enforce SSO** enabled.&#x20;

This prevents a lockout from your organization after a bad SSO setup. Admins can always sign in and remove or fix SSO settings.
{% endhint %}

You’ll need the following from your IdP metadata to register a SAML provider:

* A **label** – this can be anything, it’ll be displayed on the login page
* An **entity ID**
* A **Single Sign On URL**
* An **X.509 certificate** – make sure you copy and paste the whole certificate!

### ​Set up on the IdP <a href="#setup-on-the-idp" id="setup-on-the-idp"></a>

Most SAML 2.0 compliant identity providers require the same information about the service provider (GitBook, in this case) for set up. These values are specific to your GitBook organization and are available in the **Settings -> SSO** tab of the GitBook organization where you want to enable SSO.‌

Most of these values can be copied directly into your IdP to complete configuration of SAML.

GitBook requires that the **NameID** contain the user’s email address. Technically we are looking for: `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress` as the Name-ID format – many providers (such as Google) will allow you set a format such as **EMAIL**.

### Custom attributes

GitBook will pull the following custom attributes from the SAML assert response and use them when creating the user.

| Field        | Description                                                                                              |
| ------------ | -------------------------------------------------------------------------------------------------------- |
| `first_name` | `first_name` and `last_name` fields will be combined to produce the display name for the user in GitBook |
| `last_name`  | `first_name` and `last_name` fields will be combined to produce the display name for the user in GitBook |

## ​Creating end-user accounts <a href="#creating-end-user-account" id="creating-end-user-account"></a>

To add members, create accounts for them in your IdP. The first time a new member logs in to GitBook via the IdP, a GitBook account will be created for them via automatic IdP provisioning. The user will have access to organization resources as an organization member.

{% hint style="danger" %}
Set-up requires lower case email addresses. Do not use mixed case email addresses.‌
{% endhint %}

## ​Removing accounts <a href="#removing-end-user-accounts" id="removing-end-user-accounts"></a>

Removing a member from the IdP will prevent the user from being able to sign in to the corresponding GitBook account, **but will not remove the account from GitBook**. We advise also removing the account from the GitBook organization.

## Controlling access

Once you have set up SAML SSO, the onus is on the IdP to control who can access your GitBook account.

## ​Security notice <a href="#security-notice" id="security-notice"></a>

If you have an existing GitBook account under the same email address as the one we get from Identity Provider and you are not a member of the organization you're trying to sign into, we will not be able to automatically add you to the organization with the SAML configuration due to security reasons. You have two options:

1. Delete your existing GitBook account and then log into your desired organization with SAML. GitBook will then create a new account for you and you will be added to the organization
2. Or, ask your admin to invite you to the organization:

If your organization does not have "Enforce SSO" enabled, an admin of your organization can invite users through the Members page in your organization's settings.

If your organization has enabled "Enforce SSO", an admin will have to use GitBook's `invites` API endpoint to invite users to the organization. A call to this API would look like the following;

```
curl --request POST --header "Authorization: Bearer <your_access_token>" --url "https://api.gitbook.com/v1/orgs/<org_id>/invites" --header 'Content-Type: application/json' --data-raw '{ "sso": true, "role": "<role>", "emails":["<email>"] }'
```
