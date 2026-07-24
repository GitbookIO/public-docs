---
description: >-
  Use the Docs Embed with sites that require authentication by passing visitor
  tokens or using authenticated access
---

# Authentication

If your GitBook documentation requires authentication, Docs Embed needs a GitBook visitor token to access content.

There are two approaches:

1. **Pass the token directly** (recommended) - Initialize the embed with a GitBook visitor token.
2. **Use cookie-based detection** - Check for the GitBook visitor token before loading.

## Approach 1: Pass token directly (Recommended)

When initializing the embed, pass the GitBook visitor token as `visitor.token`.

`visitor.token` isn't a raw access token or ID token from your identity provider. It is the GitBook visitor token that GitBook issues for authenticated docs access. The `your-jwt-token` values in these examples represent that GitBook-issued token.

{% tabs %}
{% tab title="Standalone Script" %}
```html
<script src="https://docs.company.com/~gitbook/embed/script.js?jwt_token=your-jwt-token"></script>
<script>
  window.GitBook(
    "init",
    { siteURL: "https://docs.company.com" },
    { visitor: { token: "your-jwt-token" } }
  );
  window.GitBook("show");
</script>
```
{% endtab %}

{% tab title="NPM Package" %}
```javascript
import { createGitBook } from "@gitbook/embed";

const gitbook = createGitBook({
  siteURL: "https://docs.company.com",
});

const iframe = document.createElement("iframe");
iframe.src = gitbook.getFrameURL({
  visitor: {
    token: "your-jwt-token",
    unsignedClaims: { userId: "123", plan: "premium" },
  },
});
```
{% endtab %}

{% tab title="React Components" %}
```jsx
<GitBookProvider siteURL="https://docs.company.com">
  <GitBookFrame
    visitor={{
      token: "your-jwt-token",
      unsignedClaims: { userId: "123" },
    }}
  />
</GitBookProvider>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The Embed config API has not changed. Pass GitBook-issued visitor tokens as `visitor.token`.

For authenticated sites, GitBook forwards this token to the site as `jwt_token` in the iframe/script URL. If you load the standalone script from an authenticated site, you must include `jwt_token` in the `<script src>` URL.
{% endhint %}

## OIDC-backed sites

Docs Embed accepts the GitBook visitor-token flow using HS256. You can't change or configure this algorithm to accept RS256 identity-provider tokens.

Don't pass an OIDC provider's access token or ID token as `visitor.token`. Auth0 and Descope tokens that use RS256 are incompatible and Docs Embed rejects them because of their signing algorithm. Don't pass through, re-sign, or mint a GitBook visitor token from an identity-provider token.

For an OIDC-backed docs site, use this flow:

1. Send the user to your protected docs-site URL, such as `https://docs.example.com`.
2. Complete the normal interactive OIDC sign-in on the docs site.
3. After GitBook establishes the docs-site session and stores `gitbook-visitor-token`, retrieve that token.
4. Pass the token with the cookie-based or direct-token approach on this page.

This flow needs a prior successful docs-site sign-in. It also needs the required cookie and domain availability.

{% hint style="warning" %}
Docs Embed can't start, redirect through, or silently complete the docs site's OIDC authorization handshake. If a first-time authenticated visitor needs access entirely inside the embed, no supported integration path exists. Send them through an explicit docs-site sign-in step before loading the authenticated embed.
{% endhint %}

## Approach 2: Cookie-based detection

If your docs site stores the visitor token in cookies (as `gitbook-visitor-token`), you can check for it before loading the embed.

After a user signs in to your authenticated docs site, GitBook stores a visitor token in their browser cookies under the key `gitbook-visitor-token`. The embed needs this token to fetch content from your docs.

**The flow:**

1. The user signs in to your docs site.
2. GitBook stores the visitor token in browser cookies.
3. Your app checks for the token.
4. If the token exists, load the embed and pass the token.
5. If the token doesn't exist, send the user to your docs site to sign in.

{% tabs %}
{% tab title="Standalone Script" %}
**Copy-paste snippet**

Use this snippet only after the user completes docs-site sign-in:

```html
<script>
  (function () {
    // Check for the visitor token in cookies
    function getCookie(name) {
      var value = "; " + document.cookie;
      var parts = value.split("; " + name + "=");
      if (parts.length === 2) return parts.pop().split(";").shift();
    }

    var token = getCookie("gitbook-visitor-token");

    if (!token) {
      console.warn("[Docs Embed] Sign in at https://docs.example.com before loading the embed.");
      return;
    }

    // Token exists, load the embed
    var script = document.createElement("script");
    script.src =
      "https://docs.example.com/~gitbook/embed/script.js?jwt_token=" +
      encodeURIComponent(token);
    script.async = true;
    script.onload = function () {
      window.GitBook(
        "init",
        { siteURL: "https://docs.example.com" },
        { visitor: { token: token } }
      );
      window.GitBook("show");
    };
    document.head.appendChild(script);
  })();
</script>
```

{% hint style="warning" %}
Replace `docs.example.com` with your actual docs site URL.
{% endhint %}

**Alternative: Prompt users to sign in**

If the token is missing, send the user to the protected docs-site URL. This starts the supported interactive OIDC sign-in flow:

```html
<script>
  (function () {
    function getCookie(name) {
      var value = "; " + document.cookie;
      var parts = value.split("; " + name + "=");
      if (parts.length === 2) return parts.pop().split(";").shift();
    }

    var token = getCookie("gitbook-visitor-token");

    if (!token) {
      // Redirect to docs or show a message
      alert("Please sign in to your docs to access help.");
      window.location.href = "https://docs.example.com";
      return;
    }

    // Load the embed with token
    var script = document.createElement("script");
    script.src =
      "https://docs.example.com/~gitbook/embed/script.js?jwt_token=" +
      encodeURIComponent(token);
    script.async = true;
    script.onload = function () {
      window.GitBook(
        "init",
        { siteURL: "https://docs.example.com" },
        { visitor: { token: token } }
      );
      window.GitBook("show");
    };
    document.head.appendChild(script);
  })();
</script>
```
{% endtab %}

{% tab title="NPM Package" %}
When using the NPM package, check for the token before initializing:

```javascript
import { createGitBook } from "@gitbook/embed";

function initializeEmbed() {
  // Check for token in cookies
  const getCookie = (name) => {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) return parts.pop().split(";").shift();
  };

  const token = getCookie("gitbook-visitor-token");

  if (!token) {
    console.warn("[Docs Embed] Sign in to the docs site before loading the embed.");
    return null;
  }

  const gitbook = createGitBook({
    siteURL: "https://docs.example.com",
  });

  const iframe = document.createElement("iframe");
  iframe.src = gitbook.getFrameURL({
    visitor: { token: token },
  });
  const frame = gitbook.createFrame(iframe);

  document.getElementById("embed-container").appendChild(iframe);
  return frame;
}

initializeEmbed();
```
{% endtab %}

{% tab title="React Components" %}
For React apps, conditionally render the embed after docs-site sign-in creates the visitor token:

```jsx
import { useEffect, useState } from "react";
import { GitBookProvider, GitBookFrame } from "@gitbook/embed/react";

function App() {
  const [token, setToken] = useState(null);

  useEffect(() => {
    // Check for token in cookies
    const getCookie = (name) => {
      const value = `; ${document.cookie}`;
      const parts = value.split(`; ${name}=`);
      if (parts.length === 2) return parts.pop().split(";").shift();
    };

    const visitorToken = getCookie("gitbook-visitor-token");
    setToken(visitorToken);
  }, []);

  if (!token) {
    return (
      <div>
        <p>Please sign in to access help.</p>
        <a href="https://docs.example.com">Sign in</a>
      </div>
    );
  }

  return (
    <GitBookProvider siteURL="https://docs.example.com">
      <YourAppContent />
      <GitBookFrame visitor={{ token: token }} />
    </GitBookProvider>
  );
}
```
{% endtab %}
{% endtabs %}

## Common pitfalls

* **Using an identity-provider token** – Don't use an OIDC access token or ID token as `visitor.token`. Use the GitBook-issued HS256 visitor token after docs-site authentication.
* **Loading the embed before sign-in** – Send first-time visitors to the docs site to complete sign-in before loading the script or components.
* **Token not persisting across domains** – Cookies don't persist across different domains due to browser security policies. Your app and docs must be on the same domain or subdomain, or pass the token directly.
* **Token expired** – Tokens can expire. If the embed returns authentication errors, prompt users to sign in again.
* **Using wrong cookie name** – The token is stored as `gitbook-visitor-token`, not `gitbook-token` or other variations.
* **Not passing token to init/getFrameURL** – When using the cookie-based approach, make sure to pass the token to `GitBook('init', ..., { visitor: { token } })` or `getFrameURL({ visitor: { token } })`.

## Debugging

To verify the token is present, open your browser console and run:

```javascript
document.cookie.split(";").find((c) => c.includes("gitbook-visitor-token"));
```

If this returns `undefined`, the user hasn't signed in to your docs yet.

## Next steps

* [Customizing the Embed](configuration/customizing-docs-embed.md) – Add welcome messages and actions
* [Creating custom tools](configuration/creating-custom-tools.md) – Integrate with your product APIs
* [Docs Embed documentation](./) – Complete embedding guide
