---
description: Add GitBook Assistant to any website with a simple script tag
---

# Script tag

The quickest way to add GitBook Assistant to your website or app is by adding it through a script tag. Every docs site in GitBook includes a ready-to-use script for embedding the Assistant as a widget.

## Steps

1.  **Get your embed script URL**

    Navigate to your docs site's **Settings** → **AI & MCP** tab and copy the script URL. It will look like: `https://docs.company.com/~gitbook/embed/script.js`
2.  **Add the script tag to your HTML**

    Place this code in your HTML `<head>` or before the closing `</body>` tag:

    ```html
    <script src="https://docs.company.com/~gitbook/embed/script.js"></script>
    <script>
      window.GitBook("show");
    </script>
    ```
3.  **Replace the docs URL**

    Update `docs.company.com` with your actual docs site URL.
4.  **Test the widget**

    Load your page. The Assistant widget should appear in the bottom-right corner.
5.  **Optionally configure the Assistant**

    Add customization options before calling `show()`:

    ```html
    <script src="https://docs.company.com/~gitbook/embed/script.js"></script>
    <script>
      window.GitBook("configure", {
        welcomeMessage: "Welcome! How can I help you today?",
        suggestions: [
          "How do I get started?",
          "What are the pricing plans?",
          "How do I reset my password?",
        ],
      });
      window.GitBook("show");
    </script>
    ```
6.  **Control widget visibility**

    Use the API to show, hide, open, or close the Assistant:

    ```html
    <script>
      // Show the widget
      window.GitBook("show");

      // Hide the widget
      window.GitBook("hide");

      // Open the Assistant panel
      window.GitBook("open");

      // Close the Assistant panel
      window.GitBook("close");
    </script>
    ```
7.  **Load dynamically (optional)**

    For authenticated docs or conditional loading, inject the script at runtime:

    ```html
    <script>
      function loadGitBookAssistant() {
        var script = document.createElement("script");
        script.src = "https://docs.company.com/~gitbook/embed/script.js";
        script.async = true;
        script.onload = function () {
          window.GitBook("show");
        };
        document.head.appendChild(script);
      }

      // Load when ready
      loadGitBookAssistant();
    </script>
    ```
8.  **Verify the setup**

    Open your browser console and type `window.GitBook` to confirm the API is available.

## Props & Configuration

| Option           | Type       | Required | Default                 | Description                                                                                        |
| ---------------- | ---------- | -------- | ----------------------- | -------------------------------------------------------------------------------------------------- |
| `siteURL`        | `string`   | Yes\*    | Derived from script URL | Your GitBook docs site URL. Only required when using `configure()` explicitly.                     |
| `welcomeMessage` | `string`   | No       | `null`                  | Custom welcome message shown when the Assistant opens.                                             |
| `suggestions`    | `string[]` | No       | `[]`                    | Array of suggested questions displayed to users.                                                   |
| `buttons`        | `object[]` | No       | `[]`                    | Custom buttons in the Assistant header. Each button has `label`, `icon`, and `onClick` properties. |

**API Methods** (via `window.GitBook()`):

| Method        | Parameters | Description                                                              |
| ------------- | ---------- | ------------------------------------------------------------------------ |
| `'show'`      | `config?`  | Show the Assistant widget. Optionally pass a config object.              |
| `'hide'`      | None       | Hide the widget without unloading it.                                    |
| `'open'`      | None       | Open the Assistant panel.                                                |
| `'close'`     | None       | Close the Assistant panel.                                               |
| `'toggle'`    | None       | Toggle the panel open/closed.                                            |
| `'configure'` | `config`   | Set configuration options (welcomeMessage, suggestions, buttons, tools). |
| `'unload'`    | None       | Completely remove the widget from the page.                              |

## Common pitfalls

* **Script URL is incorrect** – Ensure you're using your actual docs URL, not the example `docs.company.com`.
* **Calling GitBook before script loads** – Wrap API calls in `script.onload` or place them after the script tag.
* **Authenticated docs not accessible** – If your docs require sign-in, the Assistant cannot access content unless you provide the `gitbook-visitor-token`. See [Using with authenticated docs](../authentication/using-with-authenticated-docs.md).
* **CORS or CSP errors** – Ensure your site's Content Security Policy allows loading scripts and iframes from your GitBook domain.
* **Widget not visible** – Check z-index conflicts with other elements on your page. The widget uses a high z-index by default.
