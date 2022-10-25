---
description: Use JWT token to authorize anonymous access to private content.
---

# Visitor authentication

{% hint style="info" %}
This feature is currently accessible to all **Pro and Enterprise** customers. If you are interested in the [Enterprise plan](../../billing-and-admin/plans/#enterprise-plan), please contact [sales@gitbook.com](mailto:sales@gitbook.com) for a quote.
{% endhint %}

GitBook provides different solutions to handle access management:

* Private content accessible to members only
* SAML SSO
* public content accessible to anyone

With visitor authentication, GitBook lets your server-side code handle who has access to the content.

## How does it work?

<img src="../../.gitbook/assets/file.drawing (1).svg" alt="" class="gitbook-drawing">

## Setup Guide

{% hint style="info" %}
A complete example repository for Node.JS is available on GitHub: [https://github.com/GitbookIO/example-visitor-authentication](https://github.com/GitbookIO/example-visitor-authentication)
{% endhint %}

### Step 1: enable visitor authentication

In your space or collection, open the visibility menu and select **visitor authentication**. (If you're not on an Enterprise plan, you'll be prompted to upgrade.)

![](<../../.gitbook/assets/Publish – VA.png>)

Once enabled, you'll have access to a private signing key for this space. Each space has a unique signing key. You should keep this key secret - make sure not to commit it into your source control repository. We recommend referencing it through a production secrets system in your deployed backend.

![](<../../.gitbook/assets/Publish – VA - Link Settings.png>)

### Step 2: sign a JWT token and grant access to a visitor

Here's an example of creating a JWT token by signing the access data with the private key using the library [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) for Node JS.

```javascript
const jwt = require('jsonwebtoken');

const gitbookSignKey = '<key copied from GitBook>'

const token = jwt.sign({ data: 'foobar' }, gitbookSignKey, { expiresIn: '1h' });
const redirectURL = `https://mycompany.gitbook.io/myspace/?jwt_token=${token}`;
```

Once you've created the key, you need to include it as the value of a query parameter named `jwt_token` the URL of the GitBook content you wish the user to have access to (see `redirectURL`)

Here's a very simple Express application for signing keys and redirecting users:

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();
const port = 3000;

const gitbookSignKey = '<key copied from GitBook>'

app.get('/', (req, res) => {
 // --> Validate user access here <--

  const token = jwt.sign({ data: 'foobar' }, gitbookSignKey, { expiresIn: '1h' });
  const redirectURL = `https://mycompany.gitbook.io/myspace/?jwt_token=${token}`;

  res.redirect(redirectURL);
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
});
```

### Step 3: configure a fallback URL

Finally, within **link and domain settings** in the visibility menu, you can configure a fallback URL.

When someone directly accesses your space without the necessary token, GitBook uses the fallback URL to redirect the visitor to a custom URL so that you can authenticate them.

![](<../../.gitbook/assets/Publish – VA - Link Settings.png>)

When redirecting to the fallback URL, GitBook is passing a `location` query parameter, it can be used to redirect to the original location of the user:

```javascript
// Route handler for the fallback url
app.get('/', (req, res) => {
 // --> Validate user access here <--

  const token = jwt.sign({ data: 'foobar' }, gitbookSignKey, { expiresIn: '1h' });
  const redirectURL = `https://mycompany.gitbook.io/myspace/${req.query.location || ''}?jwt_token=${token}`;

  res.redirect(redirectURL);
```
