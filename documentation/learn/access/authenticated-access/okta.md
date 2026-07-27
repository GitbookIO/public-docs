---
description: Configure Okta as the identity provider for authenticated access.
---

# Set up Okta

{% hint style="warning" %}
Before following this guide, make sure you've first gone through [Enabling authenticated access](README.md#enable-authenticated-access).
{% endhint %}

{% stepper %}
{% step %}
#### Create a new Okta application

Create an Okta application from your Okta dashboard.
{% endstep %}

{% step %}
#### Install and configure the Okta integration

Install the Okta integration and add the required configuration.
{% endstep %}

{% step %}
#### Configure Okta for adaptive content (optional)

Configure Okta to work with adaptive content in GitBook.
{% endstep %}
{% endstepper %}

### Create a new Okta application

Sign in to the Okta admin dashboard and create a new app integration (or use an existing one) via **Applications** in the left sidebar.

Click **Create App Integration**, select **OIDC - OpenID Connect** as the sign-in method, and **Web Application** as the application type. Name it appropriately, and don't change any other settings on that page. For assignments, choose the appropriate option, then click **Save**.

On the next screen, copy the **Client ID** and **Client Secret**. Copy the **Okta Domain** from the dropdown next to your email address, top right.

### Install and configure the Okta integration

Go to the **Integrations** tab in the site you want to publish, and find the **Okta** integration. Install it on your site.

On installation, you'll be asked for the **Client ID**, **Okta Domain** (remove any `https://` prefix), and **Client Secret** — paste in the values you copied. Click **Save**.

Copy the URL shown in the modal, and enter it as a **Sign-In redirect URI** in Okta. Click **Save**.

Back in GitBook, close the integrations modal, click **Manage site**, go to **Audience**, select **Authenticated access**, and choose **Okta** as the backend. Click **Update audience**. Go to the site's screen and click **Publish**.

Your site is now published behind authenticated access using Okta as the identity provider. Click **Visit** to confirm — you should be asked to sign in with Okta.

### Configure Okta for adaptive content (optional)

To use [adaptive content](../configure-adaptive-content.md) with authenticated access, configure your Okta application to include relevant user data as claims in the auth token — key-value pairs GitBook can use to dynamically [adapt content](../write-content-conditions.md) based on role, plan, location, or other attributes.

Okta supports:

* **Standard claims** — common claims (`email`, `name`, `groups`) that may be included by default, but often need to be explicitly added for consistent availability.
* **Custom claims** — defined using [custom user attributes](https://help.okta.com/en-us/content/topics/users-groups-profiles/usgp-add-custom-user-attributes.htm) or expression-based logic, for values like plan tier, account ID, or internal team flags.
* **Groups as claims** — pass Okta groups as claims, useful for audience segments like "enterprise users" or "beta testers," filterable in your authorization server's claim configuration.

To add or customize claims:

1. Open your Okta Admin Console.
2. Go to **Security > API > Authorization Servers**.
3. Edit the authorization server used for your GitBook site.
4. Under the **Claims** tab, add rules to include the desired claims in the token.
5. Confirm your GitBook site reads and maps those claims correctly.

Once claims are flowing into GitBook, see [Write content conditions](../write-content-conditions.md) to define what content shows to whom.
