---
description: Configure a generic OIDC provider for authenticated access.
---

# Set up OIDC

{% hint style="warning" %}
Before following this guide, make sure you've first gone through [Enabling authenticated access](README.md#enable-authenticated-access).
{% endhint %}

OIDC (OpenID Connect) is an identity layer built on top of OAuth. Many identity providers support it, and GitBook's OIDC integration lets you publish content behind authenticated access controlled by whichever provider you use.

{% hint style="info" %}
This guide is generic — some details vary by identity provider. For illustration, it uses Google.
{% endhint %}

{% stepper %}
{% step %}
#### Create a new application with your identity provider

Create an application from your identity provider's dashboard.
{% endstep %}

{% step %}
#### Install and configure the OIDC integration

Install the OIDC integration and add the required configuration.
{% endstep %}
{% endstepper %}

### Create a new application with your identity provider

Create a new app in your identity provider, of type **Web Application**. In Google, this is under **API and Services** → **Credentials** → **OAuth 2.0 Client IDs**.

Click **Create Credentials** → **OAuth Client ID**, select **Web Application**, name it appropriately, and under **Authorized Redirect URIs**, enter the Callback URL you'll get from GitBook. Click **Create**, and note the **Client ID** and **Client Secret**.

### Install and configure the OIDC integration

Go to Integrations in the GitBook app, select **Authenticated access** as the category, and install the **OIDC** integration on your chosen docs site.

Open its configuration and note the **Callback URL** above the Save button — you may need it for your identity provider.

For **Client ID** and **Client Secret**, paste in the values from your identity provider.

You'll also need your provider's **Authorization Endpoint** and **Access Token Endpoint**. For Google, these are `https://accounts.google.com/o/oauth2/v2/auth` and `https://oauth2.googleapis.com/token` respectively — for other providers, check their documentation.

For **OAuth Scope**, enter the least permissive scope your provider allows — for Google, `openid`. GitBook only uses the access token to verify the user is authenticated, not to fetch further information, so the least permissive scope is the best security choice.

Click **Save**.

Back in GitBook, close the integrations modal, click **Manage site**, go to **Audience**, select **Authenticated access**, and choose **OIDC** as the backend. Click **Update audience**. Go to the site's screen and click **Publish**.

Your site is now published behind authenticated access using OIDC. Click **Visit** to confirm — you should be asked to sign in through your provider.

### Enable PKCE

If your identity provider requires or recommends PKCE, turn on **Use PKCE** in the OIDC integration's configuration screen. This enables Proof Key for Code Exchange for the authorization code flow the integration initiates with your provider.
