---
description: Set up an Auth0 login screen for visitors to your docs
---

# Setting up Auth0

{% hint style="info" %}
Head to our guides to find a [full walk-through](https://gitbook.com/docs/guides/product-guides/how-to-personalize-your-gitbook-site-using-auth0-and-adaptive-content) on setting up authenticated access and adaptive content with Auth0.
{% endhint %}

{% hint style="warning" %}
This guide takes your through setting up a protected sign-in screen for your docs. Before going through this guide, make sure you’ve first gone through [Enabling authenticated access](enabling-authenticated-access.md).
{% endhint %}

To setup your GitBook site with authenticated access using Auth0, the process looks as follows:

{% stepper %}
{% step %}
#### [Create a new application in Auth0](setting-up-auth0.md#id-1.-create-a-new-application-in-auth0)

Create an Auth0 application in your Auth0 dashboard.
{% endstep %}

{% step %}
#### [Install and configure the Auth0 integration](setting-up-auth0.md#id-2.-install-and-configure-the-auth0-integration)

Install the Auth0 integration and add the required configuration to your GitBook site.
{% endstep %}

{% step %}
#### [Configure Auth0 for Adaptive content (optional)](setting-up-auth0.md#id-3.-configure-auth0-for-adaptive-content-optional)

Configure Auth0 to work with adaptive content in GitBook.
{% endstep %}
{% endstepper %}

### 1. Create a new application in Auth0

Start by creating a new application in your Auth0 platform dashboard. This application will allow the GitBook Auth0 integration to request tokens to validate user identity before granting them access to your site.

1. Sign in to your Auth0 [dashboard](https://manage.auth0.com/dashboard/).
2. Head to **Applications > Applications** section from the left sidebar.
3. Click on the **+ Create Application** button, and give your app a name.
4. Under the **Choose an application type,** select **Regular Web Applications**.
5. In the **Quickstart** screen of the newly created app, select **Node.js (Express)** and then **I want to integrated my app**.
6.  You should then see a configuration screen like below.\
    Click **Save Settings And Continue**.<br>

    <figure><img src="../../.gitbook/assets/30_06_25_30_06_25_auth0_app_configure_screen.png" alt=""><figcaption></figcaption></figure>
7. Click on the **Settings** tab.
8. Copy and make note of the **Domain**, **Client ID** and **Client Secret**.

{% hint style="warning" %}
Please ensure that you have **at least one connection enabled** for your Auth0 application under the **Connections** tab.
{% endhint %}

### 2. Install and configure the Auth0 integration

Once you've created the Auth0 application, the next step is to install the Auth0 integration in GitBook and link it with your Auth0 application using the credentials you generated earlier:

1. Navigate to the site where you've enabled authenticated access and want to use Auth0 as the identity provider.
2.  Click on the **Integrations** button in the top right from your site’s settings.<br>

    <figure><img src="../../.gitbook/assets/10_04_25_10_04_25_va_site_integration_overview_screen.png" alt=""><figcaption></figcaption></figure>
3. Click on **Authenticated Access** from the categories in the sidebar.
4. Select the **Auth0** integration.
5.  Click **Install on this site**.<br>

    <figure><img src="../../.gitbook/assets/30_06_25_30_06_25_auth0_install_integration.png" alt=""><figcaption></figcaption></figure>
6.  After installing the integration on your site, you should see the integration's configuration screen:<br>

    <figure><img src="../../.gitbook/assets/30_06_25_30_06_25_auth0_configure_integration.png" alt=""><figcaption></figcaption></figure>
7. Enter the **Domain**, **Client ID** and **Client Secret** values you copied after creating the Auth0 application earlier. For Auth0 Domain, enter the Domain copied from Auth0 (make sure to prefix it with `https://`).
8. **(optional)** Enable the **Include claims in JWT token** option at the bottom of the dialog if you have enabled your site for [adaptive content](../adaptive-content/enabling-adaptive-content/).
9. Copy and make note of the **Callback** **URL** displayed **at the bottom of the dialog**.
10. Click **Save**.
11. Head back to the Auth0 application you created earlier in the Auth0 dashboard.
12. Browse to **Applications > Applications** in the sidebar and select the **Settings** tab.
13. Scroll down to the **Application URIs** section of the settings
14. Paste the **Callback URL** you copied earlier from the GitBook integration dialog into the **Allowed Callback URL** input field.
15. Click **Save.**
16. Head back to **Auth0 integration** installation screen **in GitBook**.
17. Close the integration dialogs and click on the **Settings** tab in the site screen.
18. Browse to **Audience** and select **Authenticated access** (if not already selected).
19. Select **Auth0** from the dropdown in the **Authentication backend** section.
20. Click **Update audience**.
21. Head to the site's overview screen and click **Publish** if the site is not already published.

Your site is now published behind authenticated access using your Auth0 as identity provider.

To test it out, click on **Visit**. You will be asked to sign in with Auth0, which confirms that your site is published behind authenticated access using Auth0.

### 3. Configure Auth0 for Adaptive content (optional)

{% embed url="https://www.youtube.com/embed/uhWeQkgyg8Y?si=7_kD3RF-Is_MnYhZ" %}

To leverage the Adaptive Content capability in your authenticated access site, [configure the Auth0 application](https://auth0.com/docs/secure/tokens/json-web-tokens/create-custom-claims) to include additional user information in the authentication token as claims.

These claims, represented as key-value pairs, are passed to GitBook and can be used to [adapt content](../adaptive-content/adapting-your-content.md) dynamically for your site visitors.
