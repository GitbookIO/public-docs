---
description: Set up an AWS Cognito login screen for visitors to your docs.
---

# Setting up AWS Cognito

{% hint style="warning" %}
This guide takes you through setting up a protected sign-in screen for your docs. Before going through this guide, make sure you’ve first gone through the process of [enabling authenticated access](enabling-authenticated-access.md).
{% endhint %}

To setup your GitBook site with authenticated access using AWS Cognito, the process looks as follows:

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

Go to your desired User Pool in Cognito, and click on App integration. Make a note of the Cognito domain, we will need it to configure the integration.

Scroll to the bottom and click "Create app client". For the app type, select "Confidential client." Scroll down to Hosted UI settings. In allowed Callback URLs, enter the Callback URL you got from GitBook upon installing the integration on a space.

Scroll further down to "OAuth 2.0 grant types"- make sure "Authorization code grant" is selected.

For "OpenID connect scopes", make sure OpenID is selected.

Scroll down and click "Create app client".

Click on the created app client and make a note of the Client ID and Client Secret.

### Install and configure the AWS Cognito integration

Navigate to integrations within the GitBook app, select authenticated access as the category, and install the AWS Cognito integration.

<figure><img src="../../.gitbook/assets/Screen Shot 2024-12-13 at 3.37.39 PM.png" alt="A GitBook screenshot showing the AWS Cognito integration install screen"><figcaption></figcaption></figure>

Once you've installed it on your site, go to configuration and make a note of the Callback URL right above the Save button. We will need it to set up Cognito.

Open up the Cognito integration's configuration screen for the space you installed the integration on.

It should look like the following image:

<figure><img src="../../.gitbook/assets/Screen Shot 2024-12-13 at 3.41.57 PM.png" alt="A GitBook screenshot showing the AWS Cognito configuration screen"><figcaption></figcaption></figure>

For Client ID, Cognito Domain, and Client Secret, paste in the values you got from Cognito.

Hit Save.

Now, in GitBook, close the integrations modal and click on the Manage site button. Navigate to **Audience**, select **Authenticated access**, and choose Cognito as the backend. Then, click **Update audience**. Go to the site’s screen and click **Publish**.\
\
The site is now published behind authenticated access controlled by your Auth0 application. To try it out, click on Visit. You will be asked to sign in with Cognito, which confirms that your site is published behind authenticated access using Auth0.

### Configure AWS Cognito for adaptive content

To leverage Adaptive Content with authenticated access in GitBook, you’ll need to configure your Amazon Cognito user pool to include custom claims in the ID token.

This is typically done by creating a [Cognito Lambda trigger](https://docs.aws.amazon.com/cognito/latest/developerguide/user-pool-lambda-pre-token-generation.html)—specifically a _Pre Token Generation_ Lambda—that returns a JSON payload overriding or appending custom claims. These claims might include user roles, subscription tiers, or any other metadata relevant to your content.

Here’s an example of what that could look like:

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

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-30 at 17.31.23.png" alt=""><figcaption></figcaption></figure>

Once added, these key-value pairs are included in the authentication token and passed to GitBook, allowing your site to dynamically adapt its content based on the authenticated user’s profile.
