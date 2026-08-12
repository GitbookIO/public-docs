---
description: >-
  Learn how to set up adaptive content so you can tailor your docs to individual
  readers based on user data or URL parameters
---

# How to personalize your GitBook site using cookies and adaptive content

{% hint style="info" %}
You need an [Ultimate site](https://www.gitbook.com/pricing) with a [custom domain](https://gitbook.com/docs/publishing-documentation/custom-domain) to follow this guide.
{% endhint %}

Documentation is no longer just a static reference. As your product and audience grow, your docs need to adapt — showing the right information to the right people at the right time. For example, an enterprise user visiting your docs might need much more tailored and specific information on their team’s setup vs a new user who’s just browsing your docs.

Whether you’re supporting different user roles, pricing tiers, or geographies, adaptive content helps you create more relevant, focused experiences.&#x20;

It’s not just about making docs easier to use — it’s about making them feel like part of your product, and surfacing context-specific information to users as they use your documentation.

This guide will walk you through how to enable adaptive content, pass the right data into your docs site, and start writing personalized docs that adapt to your users.

### What is adaptive content and how does it work?

Adaptive content lets you tailor what users see based on the data (or “claims”) attached to their identity. When someone visits your site with claims like their role, plan, or region, GitBook dynamically adjusts the content to match.

You can adapt different parts of your docs — such as pages, sections, content, header links, and more.&#x20;

Use adaptive content when you want to show different messaging, examples, or instructions depending on the user — without duplicating pages.

Along with broader docs, you can tailor specific experiences for specific users, such as:

* A marketing page for free users vs. tailored guides with specific steps for paid users
* API keys and technical guides for developers vs. business metrics and information business users
* Organization guides and workflows for admins vs. product guides for end users

### Enable adaptive content for your site

To get started, you’ll first need to enable adaptive content for your site. You can do this in your site’s settings, within the **Audience** section.&#x20;

Enabling adaptive content will return a “visitor token signing key”, which is something you’ll need later on in this guide. After copying your key, you can choose a method of passing data.

{% hint style="info" %}
You can always find your visitor token signing key in your Audience settings if you ever need to remember it.
{% endhint %}

### Choose a method to pass data

Adaptive content works by attaching data (claims) to the user visiting your docs. In order to do this, you’ll need to choose the method(s) you’d like to use to attach data to a user.

<table><thead><tr><th valign="top">Method</th><th valign="top">Description</th><th valign="top">Example</th></tr></thead><tbody><tr><td valign="top"><a href="https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/url">URL</a></td><td valign="top">Pass visitor data into your docs through URL query parameters.</td><td valign="top">A user visiting <code>https://docs.acme.org/?visitor.plan=enterprise</code> would see adapted content for enterprise docs</td></tr><tr><td valign="top"><a href="https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/cookies">Cookies</a></td><td valign="top">Pass visitor data into your docs through a public or signed cookie from your product’s login.</td><td valign="top">A user who’s already signed into your product and is an enterprise customer would automatically see adapted content for enterprise docs when they visit your documentation. No extra authentication is required.</td></tr><tr><td valign="top"><a href="https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/feature-flags">Feature flags</a></td><td valign="top">Pass visitor data into your docs through LaunchDarkly or Bucket.</td><td valign="top">If using a feature flag provider like LaunchDarkly to gate enterprise features, any user who has access to enterprise features through LaunchDarkly would see adapted content for enterprise docs when they visit your documentation. No extra authentication is required.</td></tr><tr><td valign="top"><a href="https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/authenticated-access">Authenticated access</a></td><td valign="top">Pass visitor data into your docs through an authenticated access provider.</td><td valign="top">If using an authenticated access provider like Auth0 to enforce a login before accessing your docs, any user with access to enterprise features (defined in Auth0) would see adapted content for enterprise docs when they visit your documentation after logging in.</td></tr></tbody></table>

Passing data through cookies is a secure, common, and flexible way to pass data to GitBook when using adaptive content.&#x20;

The rest of this guide will focus on setting up adaptive content through a cookie.

{% hint style="info" %}
You can find information on configuring adaptive content for [URLs](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/url), [feature flags](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/feature-flags), and [authenticated access](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/authenticated-access) in our documentation.
{% endhint %}

### Set up an adaptive schema

Before you’re able to read data from our cookie, you’ll need to set up something called an [**adaptive schema**](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content#set-your-adaptive-schema). This schema tells your site to know what data to look for when someone visits your site. Setting your adaptive schema keeps your site performant, and is **required** before your site is able to read  any data from your users.

To keep things simple, this guide will focus on the enterprise use case used in the examples above. To set up an adaptive schema for an enterprise user, you can paste the schema below:

```json
{
  "type": "object",
  "properties": {
    "isEnterpriseUser": {
      "type": "boolean",
      "description": "Whether the visitor is an enterprise user."
    },
  },
  "additionalProperties": false
}
```

After setting your adaptive schema, you’re ready to pass in your user data to your site.

### Store and pass user data in a cookie

In order to pass data securely through a cookie, you’ll need to send the data as a [JSON Web Token](https://jwt.io/introduction) from your application in a cookie named `gitbook-visitor-token` tied to your domain.&#x20;

This will require adding a snippet of code to your product's existing login functionality.

{% hint style="info" %}
If your product uses an OAuth provider for its login, head to our [docs on authenticated access](https://gitbook.com/docs/publishing-documentation/authenticated-access) to follow a specific guide for your provider.
{% endhint %}

The TypeScript example below signs and attaches user data to a cookie named `gitbook-visitor-token`.

```typescript
import * as jose from 'jose';
import { Request, Response } from 'express';
import { getUserInfo } from '../services/user-info-service';

const GITBOOK_VISITOR_SIGNING_KEY = process.env.GITBOOK_VISITOR_SIGNING_KEY;
const GITBOOK_VISITOR_COOKIE_NAME = 'gitbook-visitor-token';

export async function handleAppLoginRequest(req: Request, res: Response) {
   // Your business logic for handling the login request
   // For example, checking credentials and authenticating the user
   //
   // e,g:
   // const loggedInUser = await authenticateUser(req.body.username, req.body.password);

   // After authenticating the user, retrieve user information that you wish
   // to pass to GitBook from your database or user service.
   const userInfo = await getUserInfo(loggedInUser.id);
      
   // Build the JWT payload with the user's information
   const gitbookVisitorClaims = {
       isEnterpriseUser: userInfo.isEnterpriseUser
   }
   
   // Generate a signed JWT using the claims
   const gitbookVisitorJWT = await new jose.SignJWT(gitbookVisitorClaims)
     .setProtectedHeader({ alg: 'HS256' })
     .setIssuedAt()
     .setExpirationTime('2h') // abritary 2 hours expiration
     .sign(GITBOOK_VISITOR_SIGNING_KEY);
     
  // Include a `gitbook-visitor-token` cookie including the encoded JWT in your
  // login handler response
  res.cookie(GITBOOK_VISITOR_COOKIE_NAME, gitbookVisitorJWT, {
     httpOnly: true,
     secure: process.env.NODE_ENV === 'production',
     maxAge: 2 * 60 * 60 * 1000, // abritary 2 hours expiration
     domain: '.acme.org' //
  });
  
  // Rest of your login handler logic including redirecting the user to your app
  res.redirect('/'); // Example redirect
}
```

There are a few key pieces to point out in the example above:

* `GITBOOK_VISITOR_SIGNING_KEY` is your visitor signing key from your audience settings
* The name of the cookie **must** be `gitbook-visitor-token`
* You can store any keys you’d like in the cookie, as long as they are first defined in your [adaptive schema](setting-up-adaptive-content.md#set-up-an-adaptive-schema).

After you’ve successfully attached your user data to a secure cookie, you’re ready to adapt your content.

### Working with adaptive content in GitBook

Following the example of adapting content for an enterprise user, we’re going to explore how to hide a section in our docs that only enterprise customers can see. As long as they’ve got access through your product to enterprise features, and have logged in, they will be able to see this section in your docs whenever they visit.

{% hint style="info" %}
GitBook supports adapting sections, pages, page groups, header links, and much more. [Head to our documentation](https://gitbook.com/docs/publishing-documentation/adaptive-content/adapting-your-content) to learn more.
{% endhint %}

To hide the enterprise section — assuming you’ve already created it and [added it as a section](https://gitbook.com/docs/publishing-documentation/site-structure/site-sections) in your docs — head to your site’s settings, choose the **Structure** section and locate the site section.

Launch the condition editor for your section by opening the **Actions menu** ![](https://gitbook.com/docs/~gitbook/image?url=https%3A%2F%2F1050631731-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FNkEGS7hzeqa35sMXQZ4X%252Fuploads%252F89MTSo5XRpPMVr1T0rxS%252Factions.svg%3Falt%3Dmedia%26token%3D2b5d001e-560a-4f29-8d22-de8163725ca1\&width=300\&dpr=4\&quality=100\&sign=45b786a9\&sv=2) for this section, and choosing **Add condition**.

The condition editor allows you to define when to show or hide your section. Any data being passed to GitBook will automatically be nested under a `visitor.claims` object, and will be suggested through autocomplete. Any claims you’ve passed on this object will also be suggested through autocomplete — thanks to the adaptive schema you just set up.

To only show this page to enterprise users, all you need to do is add:

```javascript
visitor.claims.isEnterpriseUser == true
```

After adding your condition, hit **Save**.

### Testing adaptive content

At this point, adaptive content is set up and ready to use. Any enterprise visitors visiting your site will be able to see your enterprise section, and any other user will not see, or have access to this section in your docs.

You can always test your conditions in the [editor preview](https://gitbook.com/docs/collaboration/change-requests#preview-a-change-request), using segments. Segments are defined “testing views” that let you imitate a user with specific claims when previewing your site, for instance, as an enterprise user in the US.&#x20;

By default, the preview will load with the default experience — which in our example means the enterprise section will **not** appear.

When inside the editor preview, click the dropdown in the top bar that says **Default experience** and add a new segment. In the editor that appears, add the following JSON:

```json
{
  "isEnterpriseUser": true
}
```

The claims you add here are already represented as data, meaning you only need to add the keys you are passing to GitBook.

Now, head back to the preview and switch to your enterprise segment. You can see and explore your docs through the eyes of an enterprise user.

### Next steps

This is just one way to adapt your docs content to a single user type — but the possibilities are huge. Find out how to set up different data methods and [explore more use cases](https://gitbook.com/docs/publishing-documentation/adaptive-content) in our documentation, or start experimenting with your own project.

Adaptive content is a powerful way to help your documentation grow alongside your product — offering the right information to the right people, automatically.

From onboarding new users, to helping power users dive deeper, to supporting enterprise teams, adaptive content allows your docs to scale.

[**→ Get started with GitBook for free**](http://app.gitbook.com/join)

[**→ Read our adaptive content documentation**](https://gitbook.com/docs/publishing-documentation/adaptive-content)
