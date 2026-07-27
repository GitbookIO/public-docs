---
description: Protect your docs behind a sign-in with your identity provider.
---

# Authenticated access

{% hint style="info" %}
Authenticated access is available on the Ultimate plan.
{% endhint %}

Authenticated access lets you publish your content while requiring authentication from anyone who wants to view it. When enabled, GitBook lets your authentication provider handle who has access.

### Use cases

* Publishing sensitive product documentation that should only be accessible to paying customers, sales prospects, or partners.
* Publishing internal knowledge base content restricted to employees.

### How it works

Choose one of two approaches:

1. **Install one of our authentication integrations** — Auth0, Azure AD, Okta, AWS Cognito, or a generic OIDC provider. Recommended if you're using a provider we support.
2. **Create and host your own server** to handle authentication — any technology works, but you're responsible for coding and maintaining it. See [Set up a custom backend](custom-backend.md).

### Built-in login and logout URLs

GitBook provides built-in URLs for sign-in and sign-out on your published site:

* `<publishedSiteURL>/~gitbook/auth/login`
* `<publishedSiteURL>/~gitbook/auth/logout`

Use the login URL anywhere you want a sign-in link, such as a header link. When a visitor opens it, GitBook redirects them to the site's configured authentication backend — this works with both integration and custom backends. GitBook also adds a `location` query parameter matching the page the visitor started from, so your backend can send them back there after sign-in.

Use the logout URL to sign a visitor out of their GitBook session.

## Enable authenticated access

Head to your [site's settings](../../customization/site-settings-reference.md), and choose **Authenticated access** from your site's audience settings. This generates a **private key**, which you'll need later in setup.

### Choose an authentication method

* [Set up Auth0](auth0.md)
* [Set up Azure AD](azure-ad.md)
* [Set up Okta](okta.md)
* [Set up AWS Cognito](aws-cognito.md)
* [Set up OIDC](oidc.md)
* [Set up a custom backend](custom-backend.md)
