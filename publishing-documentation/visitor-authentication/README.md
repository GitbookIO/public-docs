---
icon: key
description: Set up custom authentication for your published content
---

# Visitor Authentication

{% hint style="info" %}
This feature is available on the [Ultimate site plan](https://www.gitbook.com/pricing).
{% endhint %}

Visitor authentication allows you to publish your content while requiring authentication from any visitors who want to view it. When enabled, GitBook lets your authentication provider handle who has access to the content.

<figure><img src="../../.gitbook/assets/10_01_25_visitor_authentication.svg" alt=""><figcaption><p>Add a sign in to your published documentation.</p></figcaption></figure>

### Use cases

Common use cases for visitor authentication include:

* Publishing sensitive product documentation that should only be accessible to paying customers, sales prospects or partners.
* Publishing internal knowledge base content that should only be accessible to employees of your company.

### Setting up visitor authentication

There are two methods you can choose from when setting up visitor authentication:

1. Installing one of our authentication integrations — we currently support Okta, Azure, and Auth0. We **highly recommend** this option if you’re using an authentication provider we support.
2. Create and host your own server to handle the authentication. Many different technologies can be used, but it’s up to you to code and maintain the solution you choose. Read the [guides in our developer documentation](https://docs.gitbook.com/developers/visitor-authentication/custom-backend) to learn more.

### Publish with visitor authentication

To publish your docs with visitor authentication, head to the docs site you want to publish, click **Publish**, and choose the **Visitor Authentication** option.

If you’re using an external service to authenticate your users, follow the guides below to get up and running.

### **Publish as unlisted**

By default, your site will be indexed by search engines. You can alternatively choose to publish as unlisted — meaning the docs are still available to authorized, but they _won’t_ be indexed by search engines such as Google.&#x20;

Unlisted spaces can be particularly helpful if you want to publish a beta version of your docs, or do large-scale user testing without impacting your SEO with potentially duplicate content.
