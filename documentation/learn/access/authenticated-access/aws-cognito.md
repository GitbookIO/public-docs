---
description: Configure AWS Cognito as the identity provider for authenticated access.
---

# Set up AWS Cognito

{% hint style="warning" %}
Before following this guide, make sure you've first gone through [Enabling authenticated access](README.md#enable-authenticated-access).
{% endhint %}

{% stepper %}
{% step %}
#### Create a new AWS Cognito application

Create an AWS Cognito application from your AWS dashboard.
{% endstep %}

{% step %}
#### Install and configure the AWS Cognito integration

Install the AWS Cognito integration and add the required configuration.
{% endstep %}

{% step %}
#### Configure AWS Cognito for adaptive content (optional)

Configure AWS Cognito to work with adaptive content in GitBook.
{% endstep %}
{% endstepper %}

### Create a new AWS Cognito application

Go to your desired User Pool in Cognito, and click **App integration**. Note the Cognito domain — you'll need it to configure the integration.

Scroll down and click **Create app client**. For the app type, select **Confidential client**. Scroll to **Hosted UI settings**, and in **Allowed Callback URLs**, enter the Callback URL you'll get from GitBook when installing the integration on a section.

Under **OAuth 2.0 grant types**, make sure **Authorization code grant** is selected. Under **OpenID Connect scopes**, make sure **OpenID** is selected. Click **Create app client**.

Open the created app client and note its **Client ID** and **Client Secret**.

### Install and configure the AWS Cognito integration

Go to Integrations in the GitBook app, select **Authenticated access** as the category, and install the **AWS Cognito** integration.

Once installed on your site, open its configuration and note the **Callback URL** above the Save button — you'll need it to set up Cognito.

For **Client ID**, **Cognito Domain**, and **Client Secret**, paste in the values from Cognito, then click **Save**.

Back in GitBook, close the integrations modal, click **Manage site**, go to **Audience**, select **Authenticated access**, and choose **Cognito** as the backend. Click **Update audience**. Go to the site's screen and click **Publish**.

Your site is now published behind authenticated access using AWS Cognito as the identity provider. Click **Visit** to confirm — you should be asked to sign in with Cognito.

### Configure AWS Cognito for adaptive content (optional)

To use [adaptive content](../configure-adaptive-content.md) with authenticated access, configure your Amazon Cognito user pool to include custom claims in the ID token — typically via a [Cognito Lambda trigger](https://docs.aws.amazon.com/cognito/latest/developerguide/user-pool-lambda-pre-token-generation.html), specifically a **Pre Token Generation** Lambda that returns a JSON payload overriding or appending custom claims (user roles, subscription tiers, or other metadata).

```javascript
export const handler = async (event, context) => {
  // Retrieve user attribute from event request
  const userAttributes = event.request.userAttributes;

  // Add additional claims to event response
  event.response = {
    "claimsAndScopeOverrideDetails": {
      "idTokenGeneration": {},
      "accessTokenGeneration": {
        "claimsToAddOrOverride": {
          "products": ['api', 'sites', 'askAI'],
          "isBetaUser": true,
          "isAlphaUser": true,
        }
      }
    }
  };
  // Return to Amazon Cognito
  context.done(null, event);
};
```

Once added, these key-value pairs are included in the auth token and passed to GitBook, letting your site dynamically [adapt content](../write-content-conditions.md) based on the authenticated user's profile.
