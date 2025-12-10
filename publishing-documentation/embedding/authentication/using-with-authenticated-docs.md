---
description: >-
  Use the Docs Embed with sites that require authentication by passing visitor
  tokens or using authenticated access
---

# Authentication

If your GitBook documentation requires authentication (e.g., visitor authentication via OIDC, Auth0, or a custom backend), the embed cannot access your docs content unless the user's authentication token is provided.

There are two approaches:

1. **Pass the token directly** (recommended) - Initialize the embed with the visitor token
2. **Use cookie-based detection** - Check for the token in cookies before loading

## Approach 1: Pass token directly (Recommended)

When initializing the embed, pass the visitor token directly:

{% tabs %}
{% tab title="Standalone Script" %}
```html
<script src="https://docs.company.com/~gitbook/embed/script.js"></script>
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

## Approach 2: Cookie-based detection

If your docs site stores the visitor token in cookies (as `gitbook-visitor-token`), you can check for it before loading the embed.

When a user signs in to your authenticated docs, GitBook stores a visitor token in their browser cookies under the key `gitbook-visitor-token`. The embed needs this token to fetch content from your docs.

**The flow:**

1. User signs in to your docs site
2. GitBook stores the visitor token in browser cookies
3. Your app checks for the token
4. If the token exists, load the embed and pass the token
5. If the token doesn't exist, prompt the user to sign in

{% tabs %}
{% tab title="Standalone Script" %}
#### Copy-paste snippet

Use this snippet to load the embed only after a user has signed in:

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
      console.warn("[Docs Embed] Please sign in to your docs first.");
      return;
    }

    // Token exists, load the embed
    var script = document.createElement("script");
    script.src = "https://docs.example.com/~gitbook/embed/script.js";
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

#### Alternative: Prompt users to sign in

If the token is missing, you can prompt users to sign in:

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
    script.src = "https://docs.example.com/~gitbook/embed/script.js";
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
    console.warn("[Docs Embed] User must sign in first.");
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
For React apps, conditionally render the embed based on token presence:

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

* **Loading the embed before sign-in** – Always check for the token before loading the script or components, or pass the token directly when initializing.
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

* [Customizing the Embed](../configuration/customizing-docs-embed.md) – Add welcome messages and actions
* [Creating custom tools](../configuration/creating-custom-tools.md) – Integrate with your product APIs
* [Docs Embed documentation](../) – Complete embedding guide
