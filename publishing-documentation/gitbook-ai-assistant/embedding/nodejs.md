---
description: >-
  Integrate GitBook Assistant using the NPM package for full application-level
  control
---

# Node.js/NPM

If you need more control and want to work at the application level, you can install the GitBook embed package from npm. This approach is ideal for server-side rendering, build-time integration, or custom iframe management.

## Steps

1.  **Install the package**

    Add `@gitbook/embed` to your project:

    ```bash
    npm install @gitbook/embed
    ```
2.  **Import the package**

    In your application code, import the `createGitBook` function:

    ```javascript
    import { createGitBook } from "@gitbook/embed";
    ```

    Or using CommonJS:

    ```javascript
    const { createGitBook } = require("@gitbook/embed");
    ```
3.  **Initialize GitBook**

    Create a GitBook instance with your docs site URL:

    ```javascript
    const gitbook = createGitBook({
      siteURL: "https://docs.company.com",
    });
    ```
4.  **Create an iframe**

    Generate an iframe element and set its source to the Assistant URL:

    ```javascript
    const iframe = document.createElement("iframe");
    iframe.src = gitbook.getFrameURL();
    iframe.style.border = "none";
    iframe.style.width = "100%";
    iframe.style.height = "600px";
    ```
5.  **Attach the frame**

    Create a GitBook frame instance and mount it to your page:

    ```javascript
    const frame = gitbook.createFrame(iframe);
    document.getElementById("assistant-container").appendChild(iframe);
    ```
6.  **Control the Assistant programmatically**

    Use the frame instance to interact with the Assistant:

    ```javascript
    // Open the Assistant
    frame.open();

    // Close the Assistant
    frame.close();

    // Toggle the Assistant
    frame.toggle();

    // Navigate to a specific page
    frame.navigateToPage("/getting-started");

    // Send a message
    frame.postUserMessage("How do I get started?");
    ```
7.  **Add configuration options**

    Pass customization options when initializing:

    ```javascript
    const gitbook = createGitBook({
      siteURL: "https://docs.company.com",
      welcomeMessage: "Welcome to our help center!",
      suggestions: ["How do I get started?", "What are the pricing plans?"],
      buttons: [
        {
          label: "Contact Support",
          icon: "envelope",
          onClick: () => {
            window.open("mailto:support@example.com", "_blank");
          },
        },
      ],
    });
    ```
8.  **Cleanup when unmounting**

    Remove the Assistant when your component or page unmounts:

    ```javascript
    frame.destroy();
    ```

## Props & Configuration

| Option           | Type       | Required | Default | Description                                                                                             |
| ---------------- | ---------- | -------- | ------- | ------------------------------------------------------------------------------------------------------- |
| `siteURL`        | `string`   | Yes      | N/A     | Your GitBook docs site URL (e.g., `https://docs.company.com`).                                          |
| `welcomeMessage` | `string`   | No       | `null`  | Custom welcome message shown when the Assistant opens.                                                  |
| `suggestions`    | `string[]` | No       | `[]`    | Array of suggested questions displayed to users.                                                        |
| `buttons`        | `object[]` | No       | `[]`    | Custom buttons in the Assistant header. Each button has `label`, `icon`, and `onClick` properties.      |
| `tools`          | `object[]` | No       | `[]`    | Custom tools for the Assistant. See [Creating custom tools](../configuration/creating-custom-tools.md). |

**Frame Methods:**

| Method                     | Parameters        | Description                                   |
| -------------------------- | ----------------- | --------------------------------------------- |
| `open()`                   | None              | Open the Assistant panel.                     |
| `close()`                  | None              | Close the Assistant panel.                    |
| `toggle()`                 | None              | Toggle the panel open/closed.                 |
| `navigateToPage(path)`     | `path: string`    | Navigate to a specific docs page.             |
| `navigateToAssistant()`    | None              | Navigate directly to the Assistant interface. |
| `postUserMessage(message)` | `message: string` | Send a message as the user.                   |
| `clearChat()`              | None              | Clear all chat messages.                      |
| `destroy()`                | None              | Remove the Assistant and clean up resources.  |

## Common pitfalls

* **Forgetting to install the package** – Run `npm install @gitbook/embed` before importing.
* **Missing siteURL** – The `siteURL` option is required and must match your published docs site.
* **iFrame not rendering** – Ensure the parent container has sufficient width/height for the iframe to display.
* **Frame methods called before initialization** – Wait until `createFrame()` completes before calling frame methods.
* **Not cleaning up on unmount** – Always call `frame.destroy()` to prevent memory leaks in single-page apps.
