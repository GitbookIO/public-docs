---
description: Host your documentation with a /docs subdirectory using Cloudflare
icon: cloudflare
---

# Configuring a subdirectory with Cloudflare

{% include "../../.gitbook/includes/ultimate-hint.md" %}

{% stepper %}
{% step %}
### Configuring your GitBook site

In your GitBook organization, click on your docs site name in the sidebar, then click **Manage site** or open the **Settings** tab. Open the **Domain and redirects** section and under ‘Subdirectory’, click **Set up a subdirectory**.

Enter the URL where you would like to host your docs. Then specify the subdirectory for docs access, e.g. `tomatopy.pizza/docs`, and click **Configure**.

Under **Additional configuration**, you will now see a proxy URL. You'll use this in the next step when configuring your Cloudflare worker. Copy it to your clipboard.
{% endstep %}

{% step %}
### Create your Cloudflare worker

Sign into your Cloudflare account and navigate to **Workers & Pages**

Click the **Create** button.&#x20;

On the ‘Create an application’ screen, click the **Hello world** button in the ‘Start from a template’ card.

Give the worker a more descriptive name, like `mydocs-subpath-proxy`. Once you finish renaming the worker, click **Deploy**.&#x20;
{% endstep %}

{% step %}
## Configure your custom domain

Your worker will get a default URL that you can use. To configure your custom domain instead (such as `tomatopy.pizza`), click **Settings.** Then, in the ‘Domains & Routes’ section, click **+ Add**.

In the ‘Domains & Routes’ tray that opens, click **Custom domain**, then enter your custom domain in the textbox that follows. When you specify the custom domain, _do not_ include the subdirectory. For example, `tomatopy.pizza` is correct, while `tomatopy.pizza/docs` is not.&#x20;
{% endstep %}

{% step %}
### Update the worker code

When the worker is finished deploying, click **Edit code**, or click **Continue to project**, and then the **Edit code** button in the upper right.&#x20;

In the code editor that opens, replace the sample code with the following snippet:

{% code lineNumbers="true" %}
```javascript
export default {
  fetch(request) { 
    const SUBDIRECTORY = '/docs';
    const url = new URL(request.url);
    const target = "<INSERT YOUR PROXY URL FROM GITBOOK>" + url.pathname.slice(SUBDIRECTORY.length);
    const proxy = new URL(
      target.endsWith('/') ? target.slice(0, -1) : target 
    )
    proxy.search = url.search;
    return fetch(new Request(proxy, request));
  }
};
```
{% endcode %}

{% hint style="info" %}
Be sure to update the URL on line 5 with the proxy URL you got from GitBook in the first step.
{% endhint %}

Once that’s done, click **Deploy**. This process may take a few moments. Once it’s complete, when visiting the URL, you should see your docs site!
{% endstep %}
{% endstepper %}
