---
description: Pass visitor data into your docs through URL query parameters.
---

# URL

{% hint style="info" %}
Head to our guides to find a [full walk-through](https://gitbook.com/docs/guides/product-guides/how-to-personalize-your-gitbook-site-using-url-parameters-and-adaptive-content) on setting up adaptive content with cookies.
{% endhint %}

You can pass visitor data to your docs through URL query parameters. Below is an overview of the method:

<table data-full-width="false"><thead><tr><th width="325.45703125">Method</th><th width="266.6015625">Use-cases</th><th width="206.58984375">Ease of setup</th><th width="202">Security</th><th>Format</th></tr></thead><tbody><tr><td>Query parameters <code>visitor.&#x3C;prop>=</code></td><td>Feature flags, roles</td><td>Easy to use</td><td><span data-gb-custom-inline data-tag="emoji" data-code="274c">❌</span> Visitor can override the properties</td><td>JSON</td></tr></tbody></table>

### Query parameters

To pass data to GitBook through URL parameters, you’ll need to pass the data in the URL in the format `visitor.<prop>`.

For example:

```url
https://docs.acme.org/?visitor.language=fr&visitor.country=fr
```

Visiting this URL would pass in the following claims when the site loads:&#x20;

```json
{
  "language": "fr",
  "country": "fr"
}
```

{% hint style="warning" %}
Data passed through query parameters must be defined in your visitor schema through an [unsigned](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content#setting-unsigned-claims) object. Additionally, query parameters can be easily changed by the visitor and are best suited for non-sensitive information.
{% endhint %}

### Video tutorial

{% embed url="https://www.youtube.com/embed/hCd2_AAHU_I?si=jm2VOThMVh7NdJm_" %}
