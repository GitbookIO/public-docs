---
description: Set up custom authentication for your published content
icon: key
---

# Authenticated access

{% include "../../.gitbook/includes/ultimate-hint.md" %}

Authenticated access allows you to publish your content while requiring authentication from any visitors who want to view it. When enabled, GitBook lets your authentication provider handle who has access to the content.

<figure><img src="../../.gitbook/assets/10_01_25_visitor_authentication.svg" alt="A screenshot showing a login screen for docs behind authenticated access" ><figcaption><p>Add a sign in to your published documentation.</p></figcaption></figure>

### Use cases

Common use cases for authenticated access include:

* Publishing sensitive product documentation that should only be accessible to paying customers, sales prospects or partners.
* Publishing internal knowledge base content that should only be accessible to employees of your company.

### How it works

There are two methods you can choose from when setting up authenticated access:

1. Installing one of our authentication integrations — we currently support Okta, Azure, and Auth0. We **highly recommend** this option if you’re using an authentication provider we support.
2. Create and host your own server to handle the authentication. Many different technologies can be used, but it’s up to you to code and maintain the solution you choose.&#x20;

Head to [Enabling authenticated access](enabling-authenticated-access.md) to start setting up protected access for your site.
