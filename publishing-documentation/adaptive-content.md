---
icon: cloud-bolt
description: Control page visibility and more based on your user’s data.
if: visitor.claims.flags?.ADAPTIVE_CONTENT === true
noIndex: true
---

# Adaptive content

{% hint style="info" %}
This feature is available on [Premium and Ultimate site plans](https://www.gitbook.com/pricing).
{% endhint %}

Adaptive content lets you modify the content and presentation of your site based on who is reading.

<figure><img src="../.gitbook/assets/10_01_25_adaptive_content.svg" alt=""><figcaption><p>Define user access to a page through it's visibility.</p></figcaption></figure>

In a page’s visibility options, you’re able to define conditional access — a way to set a condition in code on who can or can’t see the page.

For example, this page is only available to logged in GitBook users that have the `ADAPTIVE_CONTENT` flag set in our backend, and sent through the GitBook cookie’s session.

{% hint style="warning" %}
This feature is still currently under development, and is subject to change. More information on using this feature in production will be updated soon.
{% endhint %}
