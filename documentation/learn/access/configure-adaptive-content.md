---
description: Enable adaptive content and feed claims via URL, cookies, or feature flags.
---

# Configure adaptive content

To start customizing your documentation experience for readers, enable adaptive content and decide how visitor data reaches GitBook.

### Enable adaptive content

Before you can pass user data to GitBook, configure your site to use adaptive content. Head to your [site's settings](../customization/site-settings-reference.md), and enable **Adaptive content** from your site's audience settings. This generates a **visitor token signing key**, which you'll need to continue setup.

### Set your visitor schema

Next, define a schema for the claims you expect GitBook to receive when a visitor arrives — matching how those claims are structured when sent. For example, if a visitor might be a beta user:

```json
{
  "type": "object",
  "properties": {
    "isBetaUser": {
      "type": "boolean",
      "description": "Whether the visitor is a Beta user."
    }
  },
  "additionalProperties": false
}
```

This also powers autocomplete in the [condition editor](write-content-conditions.md#the-condition-editor). Visitor schemas support:

{% tabs %}
{% tab title="Strings" %}
GitBook accepts dynamic strings — a user's name, developer tokens, and similar data. Strings can carry an optional `enum` key, restricting values to a fixed set:

```json
{
  "type": "object",
  "properties": {
    "language": {
          "type": "string",
          "description": "The language of the visitor",
          "enum": ["en", "fr", "it"]
  },
  "additionalProperties": false
}
```

{% hint style="warning" %}
Dynamic strings (no `enum` key) only work for [inline expressions](../creating-content/reusable-content-and-variables.md). Conditional expressions for visibility (pages, sections, blocks) only work with strings that have an `enum` key.
{% endhint %}
{% endtab %}

{% tab title="Booleans" %}
```json
{
  "type": "object",
  "properties": {
    "isBetaUser": {
      "type": "boolean",
      "description": "Whether the visitor is a Beta user."
    }
  },
  "additionalProperties": false
}
```
{% endtab %}

{% tab title="Objects" %}
Nest claims to group related values:

```json
{
  "type": "object",
  "properties": {
    "access": {
      "type": "object",
      "description": "User's access to product feature",
      "properties": {
        "isAlphaUser": {
          "type": "boolean",
          "description": "Whether the visitor is a Alpha user."
        },
        "isBetaUser": {
          "type": "boolean",
          "description": "Whether the visitor is a Beta user."
        }
      },
      "additionalProperties": false
    }
  },
  "additionalProperties": false
}
```
{% endtab %}
{% endtabs %}

#### Set an unsigned claim

Unsigned claims identify claims that might not be signed by a client application. Claims passed through URL parameters, unsigned cookies, or feature flags **must** be declared under an `unsigned` property alongside your signed claims:

```json
{
  "type": "object",
  "properties": {
    "isBetaUser": {
      "type": "boolean",
      "description": "Whether the visitor is a Beta user."
    },
    "unsigned": {
      "type": "object",
      "description": "Unsigned claims of the site visitor.",
      "properties": {
        "language": {
          "type": "string",
          "description": "The language of the visitor",
          "enum": ["en", "fr", "it"]
        }
      },
      "additionalProperties": false
    }
  },
  "additionalProperties": false
}
```

### Pass visitor data to GitBook

Once your schema is defined, choose how visitor data reaches GitBook:

{% tabs %}
{% tab title="Cookies" %}
{% hint style="warning" %}
This method only works if your site is served under a [custom domain](../publishing/custom-domain/README.md).
{% endhint %}

| Method | Use cases | Ease of setup | Security | Format |
|---|---|---|---|---|
| Signed cookie `gitbook-visitor-token` | API test credentials, customer identification | Requires signing and a custom domain | ✅ Properties can only be defined by the backend | JWT |
| Public cookie `gitbook-visitor-public` | Feature flags, roles | Easy to set up | ❌ Visitor can override the properties | JSON |

**Public cookie** — send data from your application by setting a public `gitbook-visitor-public` cookie:

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
Data passed through public cookies must be declared in your visitor schema as [unsigned](#set-an-unsigned-claim).
{% endhint %}

**Signed cookie** — send data more securely as a [JSON Web Token](https://jwt.io/introduction), in a cookie named `gitbook-visitor-token` tied to your domain:

{% stepper %}
{% step %}
#### Generate a JWT on login

Whenever a user logs in to your product, generate a JWT containing selected attributes of their info.
{% endstep %}

{% step %}
#### Sign it with the visitor signing key

Sign the JWT using the site's visitor signing key, found in your site's audience settings after enabling adaptive content.
{% endstep %}

{% step %}
#### Store it in a wildcard session cookie

Store the signed JWT in a wildcard session cookie under your product domain. If your app is served behind `app.acme.org`, create the cookie under the `.acme.org` wildcard domain.
{% endstep %}
{% endstepper %}

```typescript
import * as jose from 'jose';
import { Request, Response } from 'express';
import { getUserInfo } from '../services/user-info-service';
import { getFeatureFlags } from '../services/feature-flags-service';

const GITBOOK_VISITOR_SIGNING_KEY = process.env.GITBOOK_VISITOR_SIGNING_KEY;
const GITBOOK_VISITOR_COOKIE_NAME = 'gitbook-visitor-token';

export async function handleAppLoginRequest(req: Request, res: Response) {
   // Your business logic for handling the login request, e.g:
   // const loggedInUser = await authenticateUser(req.body.username, req.body.password);

   // After authenticating, retrieve the user info you want to pass to GitBook
   const userInfo = await getUserInfo(loggedInUser.id);

   // Build the JWT payload with the user's information
   const gitbookVisitorClaims = {
       firstName: userInfo.firstName,
       lastName: userInfo.lastName,
       isBetaUser: userInfo.isBetaUser,
       products: userInfo.products.map((product) => product.name),
       featureFlags: await getFeatureFlags({userId: loggedInUser.id})
   }

   // Generate a signed JWT using the claims
   const gitbookVisitorJWT = await new jose.SignJWT(gitbookVisitorClaims)
     .setProtectedHeader({ alg: 'HS256' })
     .setIssuedAt()
     .setExpirationTime('2h') // arbitrary 2 hours expiration
     .sign(GITBOOK_VISITOR_SIGNING_KEY);

  // Include a `gitbook-visitor-token` cookie including the encoded JWT in your
  // login handler response
  res.cookie(GITBOOK_VISITOR_COOKIE_NAME, gitbookVisitorJWT, {
     httpOnly: true,
     secure: process.env.NODE_ENV === 'production',
     maxAge: 2 * 60 * 60 * 1000, // arbitrary 2 hours expiration
     domain: '.acme.org'
  });

  res.redirect('/');
}
```
{% endtab %}

{% tab title="URL" %}
| Method | Use cases | Ease of setup | Security | Format |
|---|---|---|---|---|
| Query parameters `visitor.<prop>=` | Feature flags, roles | Easy to use | ❌ Visitor can override the properties | JSON |

Pass data through URL parameters in the format `visitor.<prop>`:

```
https://docs.acme.org/?visitor.language=fr
```

This becomes available in the [condition editor](write-content-conditions.md#the-condition-editor) under the unsigned object:

```javascript
visitor.claims.unsigned.language === "fr"
```

{% hint style="warning" %}
Data passed through query parameters must be declared in your visitor schema as [unsigned](#set-an-unsigned-claim). Query parameters can be changed easily by the visitor, so they're best suited to non-sensitive information.
{% endhint %}
{% endtab %}

{% tab title="Feature flags" %}
{% hint style="warning" %}
Using adaptive content with feature flags requires adding code to your application. Currently, the GitBook helper only supports React-based setups.
{% endhint %}

GitBook provides helper functions and integrations for popular feature flag providers, letting you read the feature flags a user has access to in your product as they read your docs — useful for showing documentation only for features available to a specific group.

**LaunchDarkly** — sends feature flag access as claims through [`launchdarkly-react-client-sdk`](https://launchdarkly.com/docs/sdk/client-side/react/react-web) and GitBook's `@gitbook/adaptive` package.

{% stepper %}
{% step %}
#### Install the LaunchDarkly integration

[Install it](https://app.gitbook.com/integrations/launchdarkly) on your GitBook site.
{% endstep %}

{% step %}
#### Set up your project and access keys

Add your project key and service access token from your [LaunchDarkly settings](https://app.launchdarkly.com/settings) to the integration's configuration.
{% endstep %}

{% step %}
#### Install the GitBook helper

```bash
npm install @gitbook/adaptive
```
{% endstep %}

{% step %}
#### Configure your application

Use the `withLaunchDarkly` helper with the LaunchDarkly React SDK:

```javascript
import { render } from 'react-dom';
import { withLaunchDarkly } from '@gitbook/adaptive';
import { asyncWithLDProvider, useLDClient } from 'launchdarkly-react-client-sdk';
import MyApplication from './MyApplication';

function PassFeatureFlagsToGitBookSite() {
    const ldClient = useLDClient();
    React.useEffect(() => {
        if (!ldClient) {
            return;
        }
        return withLaunchDarkly(ldClient);
    }, [ldClient]);
    return null;
}
(async () => {
    const LDProvider = await asyncWithLDProvider({
        clientSideID: 'client-side-id-123abc',
        context: {
            kind: 'user',
            key: 'user-key-123abc',
            name: 'Sandy Smith',
            email: 'sandy@example.com'
        },
        options: { /* ... */ }
    });
    render(
        <LDProvider>
            <PassFeatureFlagsToGitBookSite />
            <MyApplication />
        </LDProvider>,
        document.getElementById('reactDiv'),
    );
})();
```
{% endstep %}

{% step %}
#### Check your visitor schema

A [visitor schema](#set-your-visitor-schema) is required for your claims to be readable on your published site — installing and configuring the LaunchDarkly integration sets this automatically.
{% endstep %}

{% step %}
#### Personalize your content

Every LaunchDarkly flag becomes available under `visitor.claims.unsigned.launchdarkly`. See [Write content conditions](write-content-conditions.md).
{% endstep %}
{% endstepper %}

**Reflag** — sends feature flag access as claims through [`@reflag/react-sdk`](https://www.npmjs.com/package/@reflag/react-sdk) and GitBook's `@gitbook/adaptive` package.

{% stepper %}
{% step %}
#### Install the Reflag integration

[Install it](https://app.gitbook.com/integrations/bucket) on your GitBook site.
{% endstep %}

{% step %}
#### Set up your secret key

Add your secret key from your [Reflag settings](https://app.reflag.com/envs/current/settings/app-environments) to the integration's configuration.
{% endstep %}

{% step %}
#### Install the GitBook helper

```bash
npm install @gitbook/adaptive
```
{% endstep %}

{% step %}
#### Configure your application

Use the `withReflag` helper with the Reflag React SDK:

```javascript
import { withReflag } from '@gitbook/adaptive';
import { ReflagProvider, useClient } from '@reflag/react-sdk';
import MyApplication from './MyApplication';

function PassFeatureFlagsToGitBookSite() {
    const client = useClient();
    React.useEffect(() => {
        if (!client) {
            return;
        }
        return withReflag(client);
    }, [client]);
    return null;
}
export function Application() {
    const currentUser = useLoggedInUser();
    const appConfig = useAppConfig();
    return (
        <ReflagProvider
            publishableKey={appConfig.reflagCom.publishableKey}
            user={{
                id: currentUser.uid,
                email: currentUser.email ?? undefined,
                name: currentUser.displayName ?? '',
            }}
            company={{
                id: currentUser.company.id,
            }}
        >
            <PassFeatureFlagsToGitBookSite />
            <MyApplication />
        </ReflagProvider>
    );
}
```
{% endstep %}

{% step %}
#### Check your visitor schema

Installing and configuring the Reflag integration sets your [visitor schema](#set-your-visitor-schema) automatically.
{% endstep %}

{% step %}
#### Personalize your content

Every Reflag flag becomes available under `visitor.claims.unsigned.reflag`. See [Write content conditions](write-content-conditions.md).
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Feature flag values are evaluated client-side — avoid using this method for sensitive or security-critical data.
{% endhint %}
{% endtab %}

{% tab title="Authenticated access" %}
GitBook's authenticated-access integrations (Auth0, Azure AD, Okta, AWS Cognito, OIDC) can also drive adaptive content — configure each provider to include additional user information in the auth token as claims, which GitBook then uses to [adapt content](write-content-conditions.md).

If you use your own auth flow instead, [Set up a custom backend](authenticated-access/custom-backend.md) covers login, fallback redirects, logout, and passing claims.

See [Authenticated access](authenticated-access/README.md) for the full provider list and setup guides.
{% endtab %}
{% endtabs %}
