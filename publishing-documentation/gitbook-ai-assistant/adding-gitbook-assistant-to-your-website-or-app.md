---
description: >-
  Embed GitBook Assistant in your website or app and let users get instant
  answers based on your docs knowledge in the context of their current task
if: >-
  visitor.claims.unsigned.bucket.EMBED_ASSISTANT_PANEL == true ||
  visitor.claims.unsigned.reflag.EMBED_ASSISTANT_PANEL == true
---

# Adding GitBook Assistant to your website or app

{% include "../../.gitbook/includes/ultimate-hint.md" %}

GitBook Assistant can be embedded directly into your website or app, so your users always have access to the product knowledge within your documentation, right where they need it.&#x20;

You can add it as a script, integrate it as a package, or drop in ready-made React components.

### Embedding with a script

The quickest way to add GitBook Assistant to your website or app is by adding it through a script. Every docs site in GitBook includes a ready-to-use script for embedding the Assistant as a widget.

You’ll find the embed script in your docs site’s **Settings**, under the **AI & MCP tab**, or you can copy it from the example below (replacing `docs.company.com` with your docs site url):

```html
<script src="https://docs.company.com/~gitbook/embed/script.js"></script>
<script>
  window.GitBook('show');
</script>
```

Once added, the Assistant will appear as a widget on your site, giving visitors direct access to your documentation and more.

### Embedding with NPM

If you’d prefer more control and want to work at the application level, you can install the GitBook embed package from npm.

```bash
npm install @gitbook/embed
```

After importing it into your application, you’ll be able to create an iFrame, and set it’s URL to an initialized GitBook Assistant window.

```javascript
import { createGitBook } from '@gitbook/embed';

const gitbook = createGitBook({
  siteURL: 'https://docs.company.com'
});

const iframe = document.createElement('iframe');
iframe.src = gitbook.getFrameURL();

const frame = gitbook.createFrame(iframe);
```

This gives you full control over where and how the Assistant is displayed in your app.

### Using React components

For React projects, we provide prebuilt components that make embedding even simpler. Start by installing the GitBook embed package from npm.

```bash
npm install @gitbook/embed
```

After installing the NPM package, you can add the Assistant with just a few lines to your reach app:

```jsx
import { GitBookProvider, GitBookAssistantFrame } from '@gitbook/embed/react';

<GitBookProvider siteURL="https://docs.company.com">
  <GitBookAssistantFrame />
</GitBookProvider>
```

This setup automatically manages the Assistant’s context, so your users can explore documentation seamlessly without leaving your product.
