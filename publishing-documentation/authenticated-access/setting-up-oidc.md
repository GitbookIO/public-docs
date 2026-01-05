---
description: Set up an OIDC login screen for visitors to your docs
---

# Setting up OIDC

{% hint style="warning" %}
This guide takes you through setting up a protected sign-in screen for your docs. Before going through this guide, make sure you’ve first gone through the process of [enabling authenticated access](enabling-authenticated-access.md).
{% endhint %}

To setup your GitBook site with authenticated access using OIDC, the process looks as follows:

{% stepper %}
{% step %}
#### Create a new application with your identity provider

Create an application from your identity provider’s dashboard.
{% endstep %}

{% step %}
#### Install and configure the OIDC integration

Install the Auth0 integration and add the required configuration.
{% endstep %}
{% endstepper %}

OIDC stands for OpenID Connect, and it's an identity layer built on top of OAuth. Many identity providers abide by OIDC, and GitBook's OIDC integration for authenticated access allows you to publish your space behind authenticated access, and access to the content is controlled by your Identity Provider

{% hint style="info" %}
Since this guide is a generic guide meant for all identity providers, some details may vary depending on your Identity Provider. For illustration purposes, we are using Google as the identity provider in this guide.
{% endhint %}

### Create a new application with your identity provider

There are some things that you need to set up on your Identity Provider in order to get the integration to work.

You need to create a new app inside your Identity Provider. Its type should be "Web Application." In Google, you create these under "API and Services", "Credentials", and then under "OAuth 2.0 Client IDs."\\

<figure><img src="../../.gitbook/assets/25_04_10_setting_up_oidc_1.png" alt="A screenshot showing creation of an OAuth client in an identity provider"><figcaption></figcaption></figure>

Click on Create Credentials, select OAuth Client ID, select Web Application as the type, name it appropriately, and under Authorized Redirect URIs, enter the Callback URL you got from GitBook.

Click Create. Make a note of the Client ID and Client Secret. We will need these to finish configuring of our integration in GitBook.

### Install and configure the OIDC integration

Navigate to integrations within the GitBook app, select authenticated access as the category, and install the OIDC integration. Install the OIDC integration on your chosen docs site.

<figure><img src="../../.gitbook/assets/25_04_10_setting_up_oidc_2.png" alt="A GitBook screenshot showing the OIDC integration installation"><figcaption></figcaption></figure>

Once you've installed it on your site, go to configuration and make a note of the Callback URL right above the Save button. We may need it to set up the Identity Provider.

Open up the OIDC integration's configuration screen for the space you installed the integration on.

It should look like the following image

<figure><img src="../../.gitbook/assets/25_04_10_setting_up_oidc_3.png" alt="A GitBook screenshot showing the OIDC configuration screen"><figcaption></figcaption></figure>

For Client ID and Client Secret, paste in the values you got for your identity provider.

Now, you will need to find the Authorization Endpoint and Access Token Endpoint for your Identity Provider. For Google, these are `https://accounts.google.com/o/oauth2/v2/auth` and `https://oauth2.googleapis.com/token` respectively.

{% hint style="info" %}
If you are not using Google, these endpoints will be different for you. Please look into the documentation of your identity provider to locate these endpoints
{% endhint %}

For OAuth Scope, its value will be again be different depending on your Identity Provider. In case of Google, you can enter `openid`.

{% hint style="info" %}
Please look at the list of allowed scopes in your Identity Provider's documentation, and enter the value of the least permissive scope. We only use the Access Token to verify that the user is authenticated, and we do not use the Access Token to fetch any further information. So, entering the least permissive scope is the best security recommendation.
{% endhint %}

Hit Save.

Now, in GitBook, close the integrations modal and click on the Manage site button. Navigate to **Audience**, select **Authenticated access**, and choose OIDC as the backend. Then, click **Update audience**. Go to the site’s screen and click **Publish**.\
\
The site is now published behind authenticated access controlled by your Auth0 application. To try it out, click on Visit. You will be asked to sign in with OIDC, which confirms that your site is published behind authenticated access using Auth0.
