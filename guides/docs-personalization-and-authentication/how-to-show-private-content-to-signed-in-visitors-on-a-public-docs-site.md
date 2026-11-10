---
description: >-
  Show public documentation to everyone and private content to signed-in
  visitors.
---

# Showing private content to signed-in visitors on a public docs site

Keep your docs site public. Adaptive content uses visitor claims to show extra content to signed-in visitors.

Configure authenticated access, define visitor claims, and apply conditions to private content.

### Enabling adaptive content

1. In your docs site, go to **Settings → Audience**.
2. Under **Access**, select **Public**.
3. Under **Access**, select **Click to enable adaptive content**.

### Configuring authenticated access

If you use a supported provider, install its integration:

1. In your docs site, go to **Settings → Integrations**.
2. Install the integration for your provider.
3. Follow your provider’s setup guide.

Choose your provider’s setup guide:

* [setting-up-auth0.md](../../documentation/publish/site-audience/authenticated-access/setting-up-auth0.md "mention").
* [setting-up-azure-ad.md](../../documentation/publish/site-audience/authenticated-access/setting-up-azure-ad.md "mention").
* [setting-up-okta.md](../../documentation/publish/site-audience/authenticated-access/setting-up-okta.md "mention").
* [setting-up-aws-cognito.md](../../documentation/publish/site-audience/authenticated-access/setting-up-aws-cognito.md "mention").
* [setting-up-oidc.md](../../documentation/publish/site-audience/authenticated-access/setting-up-oidc.md "mention").
* [setting-up-a-custom-backend.md](../../documentation/publish/site-audience/authenticated-access/setting-up-a-custom-backend.md "mention").

If you use your own authentication service, see [Using your own login page](how-to-show-private-content-to-signed-in-visitors-on-a-public-docs-site.md#using-your-own-login-page).

### Using your own login page

Set up your login page with [setting-up-a-custom-backend.md](../../documentation/publish/site-audience/authenticated-access/setting-up-a-custom-backend.md "mention"). It covers the sign-in flow, the private key, and the login URL.

To use the claims from this guide, include them in the token your backend signs. This login handler sends the `isCustomer` claim from the visitor schema below, and returns the visitor to the page they started from:

{% code title="login.ts" %}
```typescript
import { Request, Response } from 'express';
import * as jose from 'jose';

const GITBOOK_VISITOR_SIGNING_KEY = process.env.GITBOOK_VISITOR_SIGNING_KEY!;
const GITBOOK_DOCS_URL = 'https://docs.example.com';

export async function handleLogin(req: Request, res: Response) {
    // Sign the visitor in with your own logic, for example:
    // const user = await authenticateUser(req.body.email, req.body.password);
    const user = { isCustomer: true }; // Replace with your authentication logic

    // Include claims that match your visitor schema
    const token = await new jose.SignJWT({ isCustomer: user.isCustomer })
        .setProtectedHeader({ alg: 'HS256' })
        .setIssuedAt()
        .setExpirationTime('2h')
        .sign(new TextEncoder().encode(GITBOOK_VISITOR_SIGNING_KEY));

    // Send the visitor back to the page they started from
    const location = typeof req.query.location === 'string' ? req.query.location : '';
    res.redirect(`${GITBOOK_DOCS_URL}/${location}?jwt_token=${token}`);
}
```
{% endcode %}

### Defining your visitor schema

Add each claim that your provider sends to the visitor schema:

1. In your docs site, go to **Settings → Audience**.
2. Under **Visitor schema**, add a property for each claim.
3. Set each property’s type.
4. Click **Save**.

Use `boolean` for true or false values. Use `string` with an `enum` for a fixed set of values.

For example, this schema expects a claim that identifies a customer:

```json
{
  "type": "object",
  "properties": {
    "isCustomer": {
      "type": "boolean",
      "description": "Whether the visitor is a customer."
    }
  },
  "additionalProperties": false
}
```

[#set-your-visitor-schema](../../documentation/publish/adaptive-content/enabling-adaptive-content/#set-your-visitor-schema "mention").

### Adding conditions to private content

Open the condition editor for the content you want to keep private:

* For a section, go to **Settings → Structure**. In the section actions menu, click **Add condition**.
* For a page, in the page actions menu, click **Add condition**.
* For part of a page, use the inline palette to add a **Conditional content** block. Click the condition badge on the block.

Then apply the condition:

1. Enter a condition that uses visitor claims, such as `visitor.claims.isCustomer == true`.
2. Click **Save**.

GitBook shows conditional content only when a signed-in visitor’s claims match the condition. All other content remains public.

[adapting-your-content.md](../../documentation/publish/adaptive-content/adapting-your-content.md "mention").

### Adding sign-in and sign-out links

The sign-in and sign-out endpoints are:

* Sign in: `https://<your-docs-site-url>/~gitbook/auth/login`.
* Sign out: `https://<your-docs-site-url>/~gitbook/auth/logout`.

Add these links to your site header:

1. In the sidebar, open your docs site and select **Layout**.
2. Under the header settings, add a header link.
3. Enter `Sign in` as the link name.
4. Enter the sign-in endpoint as the link URL.
5. Add a second header link.
6. Enter `Sign out` as the link name.
7. Enter the sign-out endpoint as the link URL.
8. Select a text link, primary button, or secondary button for each link.
9. Click **Save**.

### Testing the sign-in flow

1. Open your docs site in a private browser window. Check that public content shows and private content doesn’t.
2. Click **Sign in** and sign in as a visitor whose claims match your conditions.
3. Check that you return to the page you started from and that the private content now shows.
4. Click **Sign out** and check that the private content is hidden again.
