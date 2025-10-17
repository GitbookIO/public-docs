---
description: >-
  Embed GitBook Assistant on sites that require authentication by dynamically loading
  the script after users sign in
if: >-
  visitor.claims.unsigned.bucket.EMBED_ASSISTANT_PANEL == true ||
  visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Using with authenticated docs

If your GitBook documentation requires authentication (e.g., visitor authentication via OIDC, Auth0, or a custom backend), the embedded Assistant cannot access your docs content unless the user's authentication token is available.

## How it works

When a user signs in to your authenticated docs, GitBook stores a visitor token in `localStorage` under the key `gitbook-visitor-token`. The Assistant needs this token to fetch content from your docs.

**The recommended flow:**

1. User signs in to your docs site
2. GitBook stores the visitor token in `localStorage`
3. Your app checks for the token
4. If the token exists, load the Assistant
5. If the token doesn't exist, prompt the user to sign in

## Copy-paste snippet

Use this snippet to load the Assistant only after a user has signed in:

```html
<script>
  (function () {
    // Check for the visitor token
    var token = localStorage.getItem("gitbook-visitor-token");

    if (!token) {
      console.warn(
        "[GitBook Assistant] Please sign in to your docs first, then reload this page."
      );

      // Optional: Show a message to the user
      // alert("Please sign in to access the help assistant.");

      return;
    }

    // Token exists, load the Assistant
    var script = document.createElement("script");
    script.src = "https://docs.example.com/~gitbook/embed/script.js";
    script.async = true;

    script.onload = function () {
      try {
        window.GitBook("show", {
          welcomeMessage: "Welcome! How can I help you today?",
        });
      } catch (e) {
        console.error("[GitBook Assistant] Failed to show assistant:", e);
      }
    };

    script.onerror = function () {
      console.error("[GitBook Assistant] Failed to load embed script.");
    };

    document.head.appendChild(script);
  })();
</script>
```

**Important:** Replace `docs.example.com` with your actual docs site URL.

## Alternative: Prompt users to sign in

If you want to proactively guide users to sign in before loading the Assistant, use this approach:

```html
<script>
  (function () {
    var token = localStorage.getItem("gitbook-visitor-token");

    if (!token) {
      // Show a sign-in button or modal
      var signInButton = document.createElement("button");
      signInButton.textContent = "Sign in to access help";
      signInButton.style.position = "fixed";
      signInButton.style.bottom = "20px";
      signInButton.style.right = "20px";
      signInButton.style.padding = "12px 20px";
      signInButton.style.background = "#007bff";
      signInButton.style.color = "#fff";
      signInButton.style.border = "none";
      signInButton.style.borderRadius = "4px";
      signInButton.style.cursor = "pointer";
      signInButton.style.zIndex = "9999";

      signInButton.onclick = function () {
        // Redirect to your docs sign-in page
        window.open("https://docs.example.com", "_blank");
      };

      document.body.appendChild(signInButton);
      return;
    }

    // Load the Assistant (same as above)
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
    const token = localStorage.getItem("gitbook-visitor-token");
    setHasToken(!!token);

    if (!token) {
      console.warn(
        "[GitBook Assistant] User not authenticated. Redirecting to docs..."
      );
      // Optional: Redirect to docs sign-in
      // window.location.href = 'https://docs.example.com';
    }
  }, []);

  if (!hasToken) {
    return (
      <div style={{ padding: "20px", textAlign: "center" }}>
        <p>Please sign in to access the help assistant.</p>
        <a
          href="https://docs.example.com"
          target="_blank"
          rel="noopener noreferrer"
        >
          Sign in to docs
        </a>
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
  const token = localStorage.getItem("gitbook-visitor-token");

  if (!token) {
    console.warn(
      "[GitBook Assistant] No visitor token found. User must sign in first."
    );
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

// Call when your app is ready
initializeAssistant();
```

## Common pitfalls

- **Loading the Assistant before sign-in** – Always check for the token before loading the script or components.
- **Token not persisting across domains** – If your app and docs are on different domains, the token won't be accessible due to browser security policies. Consider embedding docs on the same domain or using a subdomain.
- **Token expired** – Tokens can expire. If the Assistant returns authentication errors, prompt users to sign in again.
- **Using wrong token key** – The token is stored under `gitbook-visitor-token`, not `gitbook-token` or other variations.
- **Not handling token refresh** – If your auth provider refreshes tokens, update the `gitbook-visitor-token` in `localStorage` accordingly.

## Debugging

To verify the token is present, open your browser console on your app's page and run:

```javascript
console.log(localStorage.getItem("gitbook-visitor-token"));
```

If this returns `null`, the user hasn't signed in to your docs yet.

## Next steps

- [Customizing the Assistant](../configuration/customizing-gitbook-assistant.md) – Add welcome messages and buttons
- [Creating custom tools](../configuration/creating-custom-tools.md) – Integrate with your product APIs
