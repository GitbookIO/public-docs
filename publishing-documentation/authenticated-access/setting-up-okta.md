---
description: Set up an Okta login screen for visitors to your docs.
---

# Setting up Okta

{% hint style="warning" %}
This guide takes you through setting up a protected sign-in screen for your docs. Before going through this guide, make sure you’ve first gone through "[Enabling authenticated access](enabling-authenticated-access.md)".
{% endhint %}

To setup your GitBook site with authenticated access using Okta, the process looks as follows:

{% stepper %}
{% step %}
### Create a new Okta application

Create an Okta application from your Okta dashboard.
{% endstep %}

{% step %}
### Install and configure the Okta integration

Install the Okta integration and add the required configuration.
{% endstep %}

{% step %}
### Configure Okta for adaptive content (optional)

Configure Okta to work with adaptive content in GitBook.
{% endstep %}
{% endstepper %}

### Create a new Okta application

First, sign in to Okta platform (the admin version) and create a new app integration (or use an existing one) by clicking the Applications button in the left sidebar.&#x20;

<figure><img src="../../.gitbook/assets/Screen Shot 2023-10-30 at 1.32.55 PM.png" alt=""><figcaption></figcaption></figure>

Click Create App Integration and select OIDC - OpenID Connect as the Sign-In method. And then select Web Application as the application type.

<figure><img src="../../.gitbook/assets/Screen Shot 2023-10-30 at 1.39.15 PM.png" alt=""><figcaption></figcaption></figure>

Name it appropriately and don't edit any other setting on that page. For assignments, choose the appropriate checkbox. Click Save.

On the next screen, copy Client ID and Client Secret. Copy the Okta Domain right below your email address by clicking the dropdown in the top right.&#x20;

<figure><img src="../../.gitbook/assets/Screen Shot 2023-10-30 at 4.52.14 PM.png" alt=""><figcaption></figcaption></figure>

We will need these values to configure the Okta Integration.

### Install and configure the Okta integration

Navigate to the Integrations tab in the site you want to publish and locate the Okta integration or navigate directly to this [https://app.gitbook.com/integrations/VA-Okta](https://app.gitbook.com/o/d8f63b60-89ae-11e7-8574-5927d48c4877/s/zq8ynchcecIscc4uulgN/).

<figure><img src="../../.gitbook/assets/Screen Shot 2024-12-13 at 3.21.30 PM.png" alt=""><figcaption></figcaption></figure>

Install the integration on your site.

Upon installation on site, you will see a screen asking you enter the Client ID, Okta Domain, and Client Secret.

<figure><img src="../../.gitbook/assets/Screen Shot 2024-12-13 at 3.34.37 PM.png" alt=""><figcaption></figcaption></figure>

For Client ID, Okta Domain (remove `https://`prefix, if any)  and Client Secret, paste in the value you copied from Okta Dashboard.&#x20;

Click Save.

Copy the URL displayed in the modal and enter it as a Sign-In redirect URI in Okta (as shown in the below screenshot). Hit Save.

<figure><img src="../../.gitbook/assets/Screen Shot 2024-01-14 at 7.55.08 PM.png" alt=""><figcaption></figcaption></figure>

Now, in GitBook, close the integrations modal and click on the Manage site button. Navigate to Audience, select Authenticated Access, and choose Okta as the backend. Then, click Update audience. Go to the site's screen and click Publish.\
\
The site is now published behind Authenticated Access controlled by your Okta application. To try it out, click on Visit. You will be asked to sign in with Okta, which confirms that your site is published behind Authenticated Access using Okta.

### Configure Okta for adaptive content

{% include "../../.gitbook/includes/adaptive-content-development-hint.md" %}
