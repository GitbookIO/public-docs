---
description: Configure Auth0 as the identity provider for authenticated access.
---

# Set up Auth0

{% hint style="warning" %}
Before following this guide, make sure you've first gone through [Enabling authenticated access](README.md#enable-authenticated-access).
{% endhint %}

{% stepper %}
{% step %}
#### Create a new application in Auth0

Create an Auth0 application in your Auth0 dashboard.
{% endstep %}

{% step %}
#### Install and configure the Auth0 integration

Install the Auth0 integration and add the required configuration to your GitBook site.
{% endstep %}

{% step %}
#### Configure Auth0 for adaptive content (optional)

Configure Auth0 to work with adaptive content in GitBook.
{% endstep %}
{% endstepper %}

### 1. Create a new application in Auth0

This application lets the GitBook Auth0 integration request tokens to validate user identity before granting access to your site.

1. Sign in to your Auth0 [dashboard](https://manage.auth0.com/dashboard/).
2. Go to **Applications > Applications** in the left sidebar.
3. Click **+ Create Application**, and give your app a name.
4. Under **Choose an application type**, select **Regular Web Applications**.
5. In the **Quickstart** screen of the new app, select **Node.js (Express)**, then **I want to integrate my app**.
6. On the configuration screen, click **Save Settings And Continue**.
7. Click the **Settings** tab.
8. Copy and note the **Domain**, **Client ID**, and **Client Secret**.

{% hint style="warning" %}
Make sure you have at least one connection enabled for your Auth0 application, under the **Connections** tab.
{% endhint %}

### 2. Install and configure the Auth0 integration

1. Go to the site where you've enabled authenticated access and want to use Auth0 as the identity provider.
2. Click **Integrations** in the top right of your site's settings.
3. Click **Authenticated Access** in the categories sidebar.
4. Select the **Auth0** integration.
5. Click **Install on this site**.
6. On the integration's configuration screen, enter the **Domain**, **Client ID**, and **Client Secret** you copied earlier — prefix the Domain with `https://`.
7. *(Optional)* Enable **Include claims in JWT token** if your site uses [adaptive content](../configure-adaptive-content.md).
8. Copy the **Callback URL** shown at the bottom of the dialog.
9. Click **Save**.
10. Back in the Auth0 dashboard, go to **Applications > Applications** → your app → **Settings**.
11. Scroll to **Application URIs**, and paste the Callback URL into **Allowed Callback URLs**.
12. Click **Save**.
13. Back in GitBook, close the integration dialogs, open the site's **Settings** tab.
14. Go to **Audience** → **Authenticated access** (if not already selected).
15. Select **Auth0** in the **Authentication backend** dropdown.
16. Click **Update audience**.
17. Go to the site's overview screen and click **Publish**, if not already published.

Your site is now published behind authenticated access using Auth0 as the identity provider. Click **Visit** to confirm — you should be asked to sign in with Auth0.

### 3. Configure Auth0 for adaptive content (optional)

To use [adaptive content](../configure-adaptive-content.md) on your authenticated site, [configure the Auth0 application](https://auth0.com/docs/secure/tokens/json-web-tokens/create-custom-claims) to include additional user information in the auth token as claims. These claims (key-value pairs) pass to GitBook and can be used to [adapt content](../write-content-conditions.md) dynamically for your site visitors.
