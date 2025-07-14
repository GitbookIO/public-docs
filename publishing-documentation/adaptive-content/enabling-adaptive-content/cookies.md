---
description: Pass visitor data into your docs through a public or signed cookie.
---

# Cookies

You can pass visitor data to your docs through your visitors browser cookies. Below is an overview of the different methods.

<table data-full-width="false"><thead><tr><th width="335.125">Method</th><th width="266.6015625">Use-cases</th><th width="206.58984375">Ease of setup</th><th width="202">Security</th><th>Format</th></tr></thead><tbody><tr><td>Signed cookie <code>gitbook-visitor-token</code></td><td>API test credentials, customer identification</td><td>Require signing and a custom domain</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span> Properties can only be defined by the backend</td><td>JWT</td></tr><tr><td>Public cookie <code>gitbook-visitor-public</code></td><td>Feature flags, roles</td><td>Easy to set up</td><td><span data-gb-custom-inline data-tag="emoji" data-code="274c">❌</span> Visitor can override the properties</td><td>JSON</td></tr></tbody></table>

{% hint style="info" %}
This method only works if your site is served under a [custom domain](../../custom-domain.md).
{% endhint %}

### Public cookie

To pass data to GitBook from a public cookie, you’ll need to send the data from your application by setting a public `gitbook-visitor-public` cookie.

Below is a simple JavaScript example:

```javascript
import Cookies from 'js-cookie';

const cookieData = {
  isLoggedIn: true,
  isBetaUser: false,
};

Cookies.set('gitbook-visitor-public', JSON.stringify(cookieData), {
  secure: true,
  domain: '*.acme.org',
})
```

{% hint style="warning" %}
Data passed through public cookies must be defined in your visitor schema through an [unsigned](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content#setting-unsigned-claims) object.
{% endhint %}

### Signed cookie

To pass data to GitBook more securely, you’ll need to send the data as a [JSON Web Token](https://jwt.io/introduction) from your application in a cookie named `gitbook-visitor-token` tied to your domain.

To set this up, you'll need to adjust your application’s login flow to include the following steps:

{% stepper %}
{% step %}
**Generate a JWT when users logs in to your application**

Whenever a user logs in to your product, generate a JWT that contains selected attributes of your authenticated user's info.
{% endstep %}

{% step %}
**Sign the JWT using the site's visitor signing key**

Then, make sure to sign the JWT using the site's **visitor signing key**, which you can find in your site’s audience settings after enabling Adaptive Content.
{% endstep %}

{% step %}
**Store the JWT in a wildcard session cookie**

Finally you need to store the signed JWT containing your user's info into a wildcard session cookie **under your product domain**.

For example, if your application is served behind the `app.acme.org` domain, the cookie will need to be created under the `.acme.org` wildcard domain.
{% endstep %}
{% endstepper %}

Below is a simple TypeScript example:

```typescript
import * as jose from 'jose';

import { Request, Response } from 'express';

import { getUserInfo } from '../services/user-info-service';
import { getFeatureFlags } from '../services/feature-flags-service';

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
       firstName: userInfo.firstName,
       lastName: userInfo.lastName,
       isBetaUser: userInfo.isBetaUser
       products: userInfo.products.map((product) => product.name),
       featureFlags: await getFeatureFlags({userId: loggedInUser.id})
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
