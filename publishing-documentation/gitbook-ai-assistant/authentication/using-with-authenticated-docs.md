---
description: >-
  Embed GitBook Assistant on sites that require authentication by dynamically
  loading the script after users sign in
if: visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Authentication

If your GitBook documentation requires authentication (e.g., visitor authentication via OIDC, Auth0, or a custom backend), the embedded Assistant cannot access your docs content unless the user's authentication token is available.

## How it works

When a user signs in to your authenticated docs, GitBook stores a visitor token in their browser cookies under the key `gitbook-visitor-token`. The Assistant needs this token to fetch content from your docs.

**The recommended flow:**

1. User signs in to your docs site
2. GitBook stores the visitor token in browser cookies
3. Your app checks for the token
4. If the token exists, load the Assistant
5. If the token doesn't exist, prompt the user to sign in

## Copy-paste snippet

Use this snippet to load the Assistant only after a user has signed in:

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
      console.warn("[GitBook Assistant] Please sign in to your docs first.");
      return;
    }

    // Token exists, load the Assistant
    var script = document.createElement("script");
    script.src = "https://docs.example.com/~gitbook/embed/script.js";
    script.async = true;
    script.onload = function () {
      window.GitBook("show");
    };
    document.head.appendChild(script);
  })();
</script>
```

**Important:** Replace `docs.example.com` with your actual docs site URL.

## Alternative: Prompt users to sign in

If the token is missing, you can prompt users to sign in:

```html
<script>
  (function () {
    function getCookie(name) {
      var value = "; " + document.cookie;
      var parts = value.split("; " + name + "=");
      if (parts.length === 2) return parts.pop().split(";").shift();
    }

    if (!getCookie("gitbook-visitor-token")) {
      // Redirect to docs or show a message
      alert("Please sign in to your docs to access help.");
      window.location.href = "https://docs.example.com";
      return;
    }

    // Load the Assistant
    var script = document.createElement("script");
    script.src = "https://docs.example.com/~gitbook/embed/script.js";
    script.async = true;
    script.onload = function () {
      window.GitBook("show");
    };
    document.head.appendChild(script);
  })();
</script>
```

## Using with React

For React apps, conditionally render the Assistant based on token presence:

```jsx
import { useEffect, useState } from "react";
import { GitBookProvider, GitBookAssistantFrame } from "@gitbook/embed/react";

function App() {
  const [hasToken, setHasToken] = useState(false);

  useEffect(() => {
    // Check for token in cookies
    const getCookie = (name) => {
      const value = `; ${document.cookie}`;
      const parts = value.split(`; ${name}=`);
      if (parts.length === 2) return parts.pop().split(";").shift();
    };

    const token = getCookie("gitbook-visitor-token");
    setHasToken(!!token);
  }, []);

  if (!hasToken) {
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
      <GitBookAssistantFrame />
    </GitBookProvider>
  );
}
```

## Using with Node.js/NPM

When using the NPM package, check for the token before initializing:

```javascript
import { createGitBook } from "@gitbook/embed";

function initializeAssistant() {
  // Check for token in cookies
  const getCookie = (name) => {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) return parts.pop().split(";").shift();
  };

  if (!getCookie("gitbook-visitor-token")) {
    console.warn("[GitBook Assistant] User must sign in first.");
    return null;
  }

  const gitbook = createGitBook({
    siteURL: "https://docs.example.com",
  });

  const iframe = document.createElement("iframe");
  iframe.src = gitbook.getFrameURL();
  const frame = gitbook.createFrame(iframe);

  document.getElementById("assistant-container").appendChild(iframe);
  return frame;
}

initializeAssistant();
```

## Common pitfalls

* **Loading the Assistant before sign-in** – Always check for the token before loading the script or components.
* **Token not persisting across domains** – Cookies don't persist across different domains due to browser security policies. Your app and docs must be on the same domain or subdomain.
* **Token expired** – Tokens can expire. If the Assistant returns authentication errors, prompt users to sign in again.
* **Using wrong cookie name** – The token is stored as `gitbook-visitor-token`, not `gitbook-token` or other variations.

## Debugging

To verify the token is present, open your browser console and run:

```javascript
document.cookie.split(";").find((c) => c.includes("gitbook-visitor-token"));
```

If this returns `undefined`, the user hasn't signed in to your docs yet.

## Next steps

* [Customizing the Assistant](../configuration/customizing-gitbook-assistant.md) – Add welcome messages and buttons
* [Creating custom tools](../configuration/creating-custom-tools.md) – Integrate with your product APIs
