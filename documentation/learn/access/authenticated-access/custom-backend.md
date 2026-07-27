---
description: Sign visitors in with your own authentication backend.
---

# Set up a custom backend

{% hint style="warning" %}
Before following this guide, make sure you've first gone through [Enabling authenticated access](README.md#enable-authenticated-access).
{% endhint %}

{% hint style="info" %}
Using a supported provider, or have an [OIDC](https://auth0.com/docs/authenticate/protocols/openid-connect-protocol)-compliant backend? [Auth0](auth0.md), [Azure AD](azure-ad.md), [Okta](okta.md), [AWS Cognito](aws-cognito.md), and [OIDC](oidc.md) all have more streamlined setup guides.
{% endhint %}

This guide walks through protecting your GitBook documentation site with your own custom authentication backend.

{% stepper %}
{% step %}
#### Create a custom backend to authenticate your users

Implement a backend that prompts users to log in and authenticates them.
{% endstep %}

{% step %}
#### Sign and pass a JWT token to GitBook

Create a JWT token and sign it with your site's private key.
{% endstep %}

{% step %}
#### Configure a login URL

Configure a URL to use when an unauthenticated visitor accesses your site.
{% endstep %}

{% step %}
#### Set up multi-tenant authenticated access (optional)

Configure your backend to handle authentication across multiple GitBook sites.
{% endstep %}

{% step %}
#### Configure your backend for adaptive content (optional)

Configure your backend to work with adaptive content in GitBook.
{% endstep %}
{% endstepper %}

### 1. Create a custom backend to authenticate your users

Set up a server that handles login and authentication before visitors reach your documentation. Your backend should:

* Prompt users to log in using your preferred authentication method.
* Validate user credentials and authenticate them.
* Generate and sign a JSON Web Token (JWT) on successful authentication.
* Redirect users to GitBook with the JWT included in the URL.

### 2. Sign and pass a JWT token to GitBook

Once authenticated, your backend must generate a JWT and pass it to GitBook when redirecting the user to your site. Sign the token with the **private key** from your site's audience settings, generated when you [enabled authenticated access](README.md#enable-authenticated-access).

```typescript
import { Request, Response } from 'express';
import * as jose from 'jose';

import { getUserInfo } from '../services/user-info-service';
import { getFeatureFlags } from '../services/feature-flags-service';

const GITBOOK_VISITOR_SIGNING_KEY = process.env.GITBOOK_VISITOR_SIGNING_KEY!;
const GITBOOK_DOCS_URL = 'https://mycompany.gitbook.io/myspace';

export async function handleAppLoginRequest(req: Request, res: Response) {
    // Your business logic for handling the login request
    // For example, checking credentials and authenticating the user
    //
    // e.g.:
    // const loggedInUser = await authenticateUser(req.body.username, req.body.password);

    // Generate a signed JWT
    const gitbookVisitorJWT = await new jose.SignJWT({})
        .setProtectedHeader({ alg: 'HS256' })
        .setIssuedAt()
        .setExpirationTime('2h') // Arbitrary 2-hour expiration
        .sign(new TextEncoder().encode(GITBOOK_VISITOR_SIGNING_KEY));

    // Redirect the user to GitBook with the JWT token in the URL
    const redirectURL = `${GITBOOK_DOCS_URL}/?jwt_token=${gitbookVisitorJWT}`;
    res.redirect(redirectURL);
}
```

#### Log visitors out of their GitBook session

Redirect them to your site URL with `~gitbook/auth/logout` appended:

`https://mycompany.gitbook.io/myspace/~gitbook/auth/logout`

This only signs the visitor out of GitBook — handle signing them out of your own identity provider separately.

### 3. Configure a login URL

The login URL is where GitBook redirects unauthenticated visitors. It should point to a handler in your custom backend that prompts login, authenticates the user, and redirects them back to your site with the JWT included in the URL.

For instance, if your login screen is at `https://example.com/login`, use that as the login URL. Configure it in your site's audience settings, under the **Authenticated access** tab.

#### Use GitBook's login endpoint

For a sign-in link on your published site, link to `<publishedSiteURL>/~gitbook/auth/login`. This redirects the visitor to the site's configured authentication backend, adding a `location` query parameter matching the page they started from — useful for header links and other entry points where you want visitors back at the same page after sign-in.

```javascript
const gitbookVisitorJWT = await new jose.SignJWT({})
    .setProtectedHeader({ alg: 'HS256' })
    .setIssuedAt()
    .setExpirationTime('2h') // Arbitrary 2-hour expiration
    .sign(new TextEncoder().encode(GITBOOK_VISITOR_SIGNING_KEY));

// Redirect to the original GitBook docs URL with the JWT included as jwt_token query parameter
// If a location is provided, the user will be redirected back to their original destination
const redirectURL = `${GITBOOK_DOCS_URL}/${req.query.location || ''}?jwt_token=${gitbookVisitorJWT}`;
res.redirect(redirectURL);
```

{% hint style="warning" %}
Because GitBook relies on the `location` search parameter, you can't use it in your login URL — `https://auth.gitbook.com/?location=something` isn't valid.
{% endhint %}

#### Use GitBook's logout endpoint

For a sign-out link, link to `<publishedSiteURL>/~gitbook/auth/logout` — this signs the visitor out of their GitBook session.

### 4. Set up multi-tenant authenticated access (optional)

If you use GitBook to serve content to multiple customers, your authentication backend needs to handle authentication across multiple sites — with a few small tweaks to your custom backend code.

#### Adding all tenants to your authentication server

Your backend needs to know the JWT signing key and URL for every GitBook site it handles:

```typescript
const CUSTOMER_A = {
  jwtSigningKey: 'aaa-aaa-aaa-aaa',
  url: 'https://mycompany.gitbook.io/customer-a'
};

const CUSTOMER_B = {
  jwtSigningKey: 'bbb-bbb-bbb-bbb',
  url: 'https://mycompany.gitbook.io/customer-b'
};
```

#### Giving your authentication server additional context

When GitBook can't authenticate a request, it redirects to your login URL, which authenticates the user and redirects them back to the requested content. To support multiple tenants, your backend needs to know which GitBook site the user is meant to access — pass this in the login URL, then check it when redirecting:

```javascript
const customerInfo = req.query.site === 'customer-a' ? CUSTOMER_A : CUSTOMER_B;

const gitbookVisitorJWT = await new jose.SignJWT({})
    .setProtectedHeader({ alg: 'HS256' })
    .setIssuedAt()
    .setExpirationTime('2h') // Arbitrary 2-hour expiration
    .sign(new TextEncoder().encode(customerInfo.jwtSigningKey));

// Redirect to the original GitBook docs URL with the JWT included as jwt_token query parameter
// If a location is provided, the user will be redirected back to their original destination
const redirectURL = `${customerInfo.url}/${req.query.location || ''}?jwt_token=${gitbookVisitorJWT}`;
res.redirect(redirectURL);
```

### 5. Configure your backend for adaptive content (optional)

To use [adaptive content](../configure-adaptive-content.md), include additional user attributes (claims) in the payload of the JWT your custom backend generates when redirecting the user to the site. GitBook uses these to [adapt content](../write-content-conditions.md) dynamically for your visitors.

```typescript
import { Request, Response } from 'express';
import * as jose from 'jose';

import { getUserInfo } from '../services/user-info-service';
import { getFeatureFlags } from '../services/feature-flags-service';

const GITBOOK_VISITOR_SIGNING_KEY = process.env.GITBOOK_VISITOR_SIGNING_KEY!;
const GITBOOK_DOCS_URL = 'https://mycompany.gitbook.io/myspace';

export async function handleAppLoginRequest(req: Request, res: Response) {
    // Your business logic for handling the login request
    // For example, checking credentials and authenticating the user
    //
    // e.g.:
    // const loggedInUser = await authenticateUser(req.body.username, req.body.password);

    // For the purpose of this example, assume a logged-in user object
    const loggedInUser = { id: '12345' }; // Replace with actual authentication logic

    // Retrieve user information to pass to GitBook
    const userInfo = await getUserInfo(loggedInUser.id);

    // Generate a signed JWT and include the user attributes as claims
    const gitbookVisitorClaims = {
        firstName: userInfo.firstName,
        lastName: userInfo.lastName,
        isBetaUser: userInfo.isBetaUser,
        products: userInfo.products.map((product) => product.name),
        featureFlags: await getFeatureFlags({ userId: loggedInUser.id })
    };

    const gitbookVisitorJWT = await new jose.SignJWT(gitbookVisitorClaims)
        .setProtectedHeader({ alg: 'HS256' })
        .setIssuedAt()
        .setExpirationTime('2h') // Arbitrary 2-hour expiration
        .sign(new TextEncoder().encode(GITBOOK_VISITOR_SIGNING_KEY));

    // Redirect the user to GitBook with the JWT token in the URL
    const redirectURL = `${GITBOOK_DOCS_URL}/?jwt_token=${gitbookVisitorJWT}`;
    res.redirect(redirectURL);
}
```

Once configured, see [Write content conditions](../write-content-conditions.md) to continue configuring your site.
