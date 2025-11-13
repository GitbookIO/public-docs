---
description: Host your documentation with a /docs subdirectory using Vercel
icon: triangle
---

# Configuring a subdirectory with Vercel

{% include "../../.gitbook/includes/ultimate-hint.md" %}

{% stepper %}
{% step %}
### Configuring your GitBook site

In your GitBook organization, click on your docs site name in the sidebar, then **Manage site**, then **Domain and redirects**. Under ‘Subdirectory’, click **Set up a subdirectory**.

Enter the URL where you would like to host your docs. Then specify the subdirectory for docs access, e.g. `tomatopy.pizza/docs`, and click **Configure**.

Under **Additional configuration**, you will now see a proxy URL. You’ll use this in the next step when configuring your Vercel settings. Copy it to your clipboard.
{% endstep %}

{% step %}
### Update your vercel.json

In your Vercel app, open your `vercel.json`file (or create one in the root directory if you don't already have one). Then, add the following:

```json
{
    "rewrites": [
        {
            "source": "/docs",
            "destination": "<INSERT YOUR PROXY URL FROM GITBOOK>"
        },
        {
            "source": "/docs/:match*",
            "destination": "<INSERT YOUR PROXY URL FROM GITBOOK>/:match*"
        }
    ]
}
```

_Be sure to update the URL_ on line 5 with the proxy URL you got from GitBook in the first step.
{% endstep %}

{% step %}
### Re-deploy your app and try it out!

Re-deploy your Vercel app with the update configuration. This may take a few moments. Now, when visiting the URL, you should see your docs site!
{% endstep %}
{% endstepper %}
