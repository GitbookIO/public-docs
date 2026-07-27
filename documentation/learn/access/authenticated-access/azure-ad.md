---
description: Configure Azure AD as the identity provider for authenticated access.
---

# Set up Azure AD

{% hint style="warning" %}
Before following this guide, make sure you've first gone through [Enabling authenticated access](README.md#enable-authenticated-access).
{% endhint %}

{% hint style="info" %}
There's a known limitation with the Azure integration where heading URL fragments are removed on authentication — the visitor lands on the correct page, but at the top rather than the linked heading. This is due to a Microsoft security measure, and doesn't recur once a user is authenticated for the session.
{% endhint %}

### Overview

{% stepper %}
{% step %}
#### Create an app registration in Azure AD

Create an Azure AD application registration in your Microsoft Entra ID admin dashboard.
{% endstep %}

{% step %}
#### Install and configure the Azure AD integration on your site

Install the Azure AD integration and add the required configuration to your GitBook site.
{% endstep %}

{% step %}
#### Configure Azure AD for adaptive content (optional)

Configure Azure AD to work with adaptive content in GitBook.
{% endstep %}
{% endstepper %}

### 1. Create an app registration in Azure AD

This registration lets the GitBook Azure AD integration request tokens to validate user identity before granting access to your site.

1. Sign in to your Microsoft Entra ID admin [dashboard](https://entra.microsoft.com/).
2. Go to **Identity > Applications > App registrations** in the left sidebar.
3. Click **+ New registration**, and give it a name.
4. Under **Supported account types**, select **Accounts in this organizational directory only (Default Directory only - Single tenant)**.
5. Leave the Redirect URI field empty for now.
6. Click **Register**.
7. On the app's **Overview** screen, copy and note the **Application (client) ID** and **Directory (tenant) ID**.
8. Click **Add a certificate or secret**.
9. Click **+ New client secret**.
10. Enter a description and click **Add**.
11. Copy and note the secret's **Value** field (not the Secret ID).

### 2. Install and configure the Azure AD integration

1. Go to the site where you've [enabled authenticated access](README.md#enable-authenticated-access) and want to use Azure AD as the identity provider.
2. Click **Integrations** in the top right of your site's settings.
3. Click **Authenticated Access** in the categories sidebar.
4. Select the **Azure** integration.
5. Click **Install on this site**.
6. On the integration's configuration screen, enter the **Client ID**, **Tenant ID**, and **Client Secret** you copied earlier, and click **Save**.
7. Copy the **URL** shown at the bottom of the dialog.
8. Back in the Microsoft Entra ID dashboard, go to your app registration → **Manage > Authentication**.
9. Click **+ Add a platform**, and select **Web**.
10. Paste the GitBook integration URL into **Redirect URI**, and click **Configure**.
11. Back in GitBook, close the integration dialogs, open the site's **Settings** tab.
12. Go to **Audience** → **Authenticated access** (if not already selected).
13. Select **Azure** in the **Authentication backend** dropdown.
14. Click **Update audience**.
15. Go to the site's overview screen and click **Publish**, if not already published.

Your site is now published behind authenticated access using Azure AD as the identity provider. Click **Visit** to confirm — you should be asked to sign in with Azure.

{% hint style="info" %}
After logging in with Azure credentials, a visitor might see a "Request approval" screen. An admin can grant this by visiting the published content URL, logging in, and approving on behalf of the organization.
{% endhint %}

### 3. Configure Azure AD for adaptive content (optional)

To use [adaptive content](../configure-adaptive-content.md) on your authenticated site, configure the Azure AD app registration to include additional user information in the auth token as claims. These claims (key-value pairs) pass to GitBook and can be used to [adapt content](../write-content-conditions.md) dynamically.

Azure AD supports different levels of claims, each set up differently:

* **Standard claims** — common claims that may be included but aren't always present by default.

{% hint style="info" %}
Azure AD keeps token sizes optimized, so many claims aren't included by default and must be explicitly requested. To ensure claims like `email`, `groups`, or `roles` are included, request them as **optional claims**.
{% endhint %}

* **Optional claims** — additional predefined claims you can enable for an application.
* **Custom claims** — claims sourced from custom user attributes in Azure AD, or an external system via a custom claims provider.

For details on including these in your Azure AD app's tokens, see Microsoft's guides on [user attributes](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-add-attributes-to-token), [optional claims](https://learn.microsoft.com/en-us/entra/identity-platform/optional-claims?toc=%2Fentra%2Fexternal-id%2Ftoc.json&bc=%2Fentra%2Fexternal-id%2Fbreadcrumb%2Ftoc.json&tabs=appui), and [custom claims](https://learn.microsoft.com/en-us/entra/identity-platform/custom-claims-provider-overview).

Once configured, see [Write content conditions](../write-content-conditions.md) to continue configuring your site.
