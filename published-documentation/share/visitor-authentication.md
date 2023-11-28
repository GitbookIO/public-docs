---
description: Set up custom authentication for your published content.
---

# Visitor Authentication

{% hint style="info" %}
This feature is currently accessible to all **Pro and Enterprise** customers. If you are interested in the [Enterprise plan](../../account-management/plans/#enterprise-plan), please contact [sales@gitbook.com](mailto:sales@gitbook.com) for a quote.
{% endhint %}

Visitor Authentication allows you to publish your content while requiring authentication from any visitors. When enabled, GitBook lets your server-side code handle who has access to the content.

In order to set up Visitor Authentication, you will need to create and host your own server to handle the authentication. Many different technologies can be used, but it's up to you to code and maintain the solution you go with.

### How it works

After enabling Visitor Authentication, your users will need to go through an authentication flow that validates the user before granting them access to the published content.

In the authentication process, your program will need to sign and return a [JSON Web Token](https://jwt.io/) to the user, that can be successfully validated by GitBook in the form of a code.&#x20;

Once the code has been validated, the user will have access to your published content.

### Enable Visitor Authentication

In your space or collection, open the visibility menu and select **Visitor Authentication**.

<figure><img src="../../.gitbook/assets/visitor-authentication.png" alt=""><figcaption><p>Set up Visitor Authentication for your GitBook Space.</p></figcaption></figure>

Once enabled, you'll have access to a private signing key for this space. You will need this in the server you create to handle the authentication.

See the section below to find guides on setting up Visitor Authentication for some common providers.

### Guides

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Node.js</strong></td><td><a href="../../.gitbook/assets/1 (1).png">1 (1).png</a></td><td><a href="https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node">https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node</a></td></tr><tr><td><strong>Next.js &#x26; Clerk</strong></td><td><a href="../../.gitbook/assets/3 (1).png">3 (1).png</a></td><td><a href="https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-next.js-and-clerk">https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-next.js-and-clerk</a></td></tr><tr><td><strong>Node.js &#x26; Okta</strong></td><td><a href="../../.gitbook/assets/6 (1).png">6 (1).png</a></td><td><a href="https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node-and-okta">https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node-and-okta</a></td></tr></tbody></table>

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Node.js &#x26; Auth0</strong></td><td><a href="https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node-and-auth0">https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node-and-auth0</a></td><td><a href="../../.gitbook/assets/8 (1).png">8 (1).png</a></td></tr><tr><td><strong>Node.js &#x26; Azure Active Directory</strong></td><td><a href="https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node-and-azure-ad">https://developer.gitbook.com/getting-started/guides/implement-visitor-authentication-using-node-and-azure-ad</a></td><td><a href="../../.gitbook/assets/7 (1).png">7 (1).png</a></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

##
