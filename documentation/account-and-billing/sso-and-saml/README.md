---
description: Learn how to share your GitBook content via SSO & SAML
---

# SSO & SAML

Control organization access with email domains or SAML single sign-on (SSO). Configure both in your organization’s **Settings** → **Access**.

## Single sign-on via email domain

Add email domains to let people with matching verified email addresses join your organization when they sign in.

To configure email domains:

1. In the organization menu, click **Settings**.
2. Under **Organization**, select **Access**.
3. Under **Allowed email domains**, add each domain you want to allow, such as `mycompany.com`.
4. Under **New members**, choose the **Default role** for people who join automatically.

Only work email domains are accepted. Personal email domains, such as `gmail.com`, can’t be added.

<figure><img src="/broken/files/24MDcfP7o1mWV965PxTc" alt="The Access management settings showing allowed email domains, the default role for new members, and the option to register a SAML identity provider"><figcaption><p>Set up SSO for your organization.</p></figcaption></figure>

{% hint style="info" %}
The default role also applies to members who join through your identity provider. You can change a member’s role at any time under **Organization → Members**.
{% endhint %}

## SAML single sign-on

SAML SSO gives members access through your identity provider (IdP).

GitBook uses your IdP for member authentication. Organization admins can still sign in with another method. This prevents lockouts after an incorrect SSO configuration.

### Prerequisites <a href="#prerequisites-for-sso-with-gitbook" id="prerequisites-for-sso-with-gitbook"></a>

SAML SSO is available on the Enterprise plan.

* Your company’s identity provider (IdP) must support the **SAML 2.0** standard.
* You must have administrative permission on the IdP.
* You must be an admin of the GitBook organization.

### Set up SAML in GitBook <a href="#setup-on-gitbook" id="setup-on-gitbook"></a>

You must be an [organization admin](../../collaborate/member-management/roles.md#admin) to configure SAML.

To configure SAML:

1. In the organization menu, click **Settings**.
2. Under **Organization**, select **Access**.
3. Under **SAML**, click **Register identity provider** and enter the details from your IdP.
4. Save the configuration, then share the SSO sign-in URL with your members.

GitBook doesn't send an announcement email after you save the configuration.

{% hint style="info" %}
Organization admins can still sign in with non-SSO methods, even with **Enforce SSO** enabled. You might still see Google, GitHub, or email options.

This prevents a lockout from your organization after a bad SSO setup. Admins can always sign in and remove or fix SSO settings.
{% endhint %}

You need these details from your IdP:

* **Label** — displayed on the sign-in page.
* **Entity ID**.
* **Single Sign On URL**.
* **X.509 certificate** — include the complete certificate.

### Set up the IdP <a href="#setup-on-the-idp" id="setup-on-the-idp"></a>

Most SAML 2.0-compliant IdPs need service provider details. In GitBook, open **Settings → Organization → Access** and find the values for your organization under **SAML**.

Copy those values into your IdP to finish the SAML configuration.

GitBook needs the **NameID** to contain the member’s email address. Use `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress` for the NameID format. Many IdPs offer this format as **EMAIL**.

### Custom attributes

GitBook reads these custom attributes from the SAML assertion when creating an account.

| Field        | Description                                                                                              |
| ------------ | -------------------------------------------------------------------------------------------------------- |
| `first_name` | `first_name` and `last_name` fields will be combined to produce the display name for the user in GitBook |
| `last_name`  | `first_name` and `last_name` fields will be combined to produce the display name for the user in GitBook |

## ​Creating end-user accounts <a href="#creating-end-user-account" id="creating-end-user-account"></a>

To add members, create accounts for them in your IdP. The first time a new member logs in to GitBook via the IdP, a GitBook account will be created for them via automatic IdP provisioning. The user will have access to organization resources as an organization member.

{% hint style="danger" %}
Setup requires lowercase email addresses. Do not use mixed-case email addresses.‌
{% endhint %}

## ​Removing accounts <a href="#removing-end-user-accounts" id="removing-end-user-accounts"></a>

Removing a member from the IdP will prevent the user from being able to sign in to the corresponding GitBook account, **but will not remove the account from GitBook**. We advise also removing the account from the GitBook organization.

## Controlling access

Once you have set up SAML SSO, the onus is on the IdP to control who can access your GitBook account.

## ​Security notice <a href="#security-notice" id="security-notice"></a>

GitBook never links an existing account to your identity provider on an admin's behalf. Only the account owner can link it, by signing in through your IdP.

If someone already has a GitBook account under the email address your IdP sends, signing in with SAML doesn't add them to your organization automatically. To give them access:

1. Invite them to your organization.
   * If **Enforce SSO** isn't enabled, invite them from **Members** in your organization's settings.
   *   If **Enforce SSO** is enabled, use the `invites` API endpoint with `"sso": true`:

       ```bash
       curl --request POST \
         --url "https://api.gitbook.com/v1/orgs/<org_id>/invites" \
         --header "Authorization: Bearer <your_access_token>" \
         --header "Content-Type: application/json" \
         --data-raw '{ "sso": true, "role": "<role>", "emails": ["<email>"] }'
       ```
2. Ask them to sign in to GitBook with their existing account and open your organization. When GitBook prompts them, they sign in through your IdP, which links their account to your SSO.

The invite adds an existing account as a member straight away. The API response lists it under `failedSSOEmails`, because the account isn't linked to your IdP yet. Accounts created by the invite are linked immediately.

{% hint style="info" %}
A GitBook account can be linked to one organization's SSO at a time. If the account is already linked to another organization, its owner can't open content in an organization that has **Enforce SSO** enabled.
{% endhint %}

Alternatively, the person can delete their existing GitBook account, then sign in to your organization with SAML. GitBook creates a new account and adds it to your organization. Deleting an account removes its access to every other organization.
