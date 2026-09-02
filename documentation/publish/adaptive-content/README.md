---
description: Deliver a tailored documentation experience based on who's reading
---

# Adaptive content

When a user visits your site, you may already know things about them — such as who they are, which plan they’re subscribed to, and which features they have access to.

Adaptive content helps to build a tailored documentation experience based on who is reading.

<figure><img src="../../.gitbook/assets/25_08_20_adaptive_content.webp" alt="A GitBook screenshot showing adaptive content controls"><figcaption><p>Personalize your user’s documentation experience through adaptive content</p></figcaption></figure>

{% hint style="info" %}
Adaptive content is slightly different from [authenticated access](../site-audience/authenticated-access/), although they can work together.

While authenticated access allows you to protect your docs through a login, adaptive content customizes published material based on various authentication methods — including authenticated access or those from your own app.
{% endhint %}

### How it works

Adaptive content works in one of two ways:

1. Passing data from your app to GitBook
2. Passing data from authenticated access

When a user visits your sites, we call the data they bring with them their “claims” — basically data that helps to identify a user. These claims are controllable by you — the site author — and can be used through the GitBook editor to show or hide different pages, variants, and sections in your docs.

You can also use conditions to target human visitors or AI agents. See [targeting human visitors and AI agents](adapting-your-content.md#target-human-visitors-and-ai-agents).

Head to our page about [enabling adaptive content](enabling-adaptive-content/) to start setting up adaptive content for your site.
