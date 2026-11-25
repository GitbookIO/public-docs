---
description: Choose an authentication method to pass user data to GitBook.
---

# Enabling adaptive content

To start customizing your documentation experience for your readers, you'll need to enable adaptive content and decide how your visitor data is passed to GitBook. This lets your site's content dynamically adapt based on who's viewing it.

### Enable adaptive content

Before you’re able to pass user data to GitBook, you’ll need to configure your site to use adaptive content.

Head to your [site’s settings](../../../manage-your-site/site-settings.md), and enable **Adaptive content** from your site’s audience settings. Once enabled, you’ll get a generated ‘Visitor token signing key’, which you’ll need in order to continue the adaptive content setup.

<figure><img src="../../../.gitbook/assets/26_01_06_enable_adaptive_content@2x.png" alt="A GitBook screenshot showing the enable adaptive content toggle"><figcaption><p>Enable adaptive content in your site’s Settings</p></figcaption></figure>

### Set your visitor schema

After enabling adaptive content, you’ll need to define a schema for the types of claims you expect GitBook to receive when a user visits your site.

The visitor schema should reflect how these claims are structured when sent to GitBook.

For example, if you expect a visitor to potentially be a beta user in your product, you would set a visitor schema similar to:

```json
{
  "type": "object",
  "properties": {
    "isBetaUser": {
      "type": "boolean",
      "description": "Whether the visitor is a Beta user."
    }
  },
  "additionalProperties": false
}
```

This will also help you use autocomplete when configuring your claims in the [condition editor](../adapting-your-content.md#working-with-the-condition-editor). Visitor schemas only support the following types:

{% tabs %}
{% tab title="Strings" %}
Read claims being passed in as strings.

GitBook accepts dynamic strings, meaning you can dynamically pass string data — such as a user’s name, developer tokens, and more.

Strings can also contain an **optional enum** key, which allows you to restrict the data that is received by GitBook to one of its set values.

```json
{
  "type": "object",
  "properties": {
    "language": {
          "type": "string",
          "description": "The language of the visitor",
          // Optional enum property
          "enum": [
            "en",
            "fr",
            "it"
          ]
  },
  "additionalProperties": false
}
```

{% hint style="warning" %}
Dynamic strings (strings defined without an enum key) are only accepted for [inline expressions](../../../create-content/variables-and-expressions.md#use-variables-in-your-content). Conditional expressions for visibility of elements (pages, sections, blocks) only work with strings defined with enum keys.
{% endhint %}
{% endtab %}

{% tab title="Booleans" %}
Read claims being passed in as booleans.

```json
{
  "type": "object",
  "properties": {
    "isBetaUser": {
      "type": "boolean",
      "description": "Whether the visitor is a Beta user."
    },
  },
  "additionalProperties": false
}
```
{% endtab %}

{% tab title="Objects" %}
Nest claims in an object to group similar values.

```json
{
  // Top level claims
  "type": "object",
  "properties": {
    // Nested claims
    "access": {
      "type": "object",
      "description": "User’s access to product feature",
      "properties": {
        "isAlphaUser": {
          "type": "boolean",
          "description": "Whether the visitor is a Alpha user."
        },
        "isBetaUser": {
          "type": "boolean",
          "description": "Whether the visitor is a Beta user."
        },
      },
      "additionalProperties": false
    }
  },
  "additionalProperties": false
}
```
{% endtab %}
{% endtabs %}

### Set an unsigned claim

Unsigned claims are a specific type of claim that identifies claims coming through that might not be signed by a client application. It is required to set claims in your visitor schema as `unsigned` if you are passing claims through URL parameters, unsigned cookies, and feature flags.

If you intend to work with unsigned claims, you will need to declare the claims you are expecting in the schema under an “unsigned” prop alongside your signed claims.

```json
{
  "type": "object",
  "properties": {
    "isBetaUser": {
      "type": "boolean",
      "description": "Whether the visitor is a Beta user."
    },
    // Add unsigned claims
    "unsigned": {
      "type": "object",
      "description": "Unsigned claims of the site visitor.",
      "properties": {
        "language": {
          "type": "string",
          "description": "The language of the visitor",
          // Optional enum property
          "enum": [
            "en",
            "fr",
            "it"
          ]
        }
      },
      "additionalProperties": false
    }
  },
  "additionalProperties": false
}
```

### Use visitor claims with the Content API

Use the Content API when your server needs published content evaluated for a specific visitor.

Define visitor claims in your schema, then sign the visitor JSON Web Token (JWT) with the **Visitor token signing key** in audience settings. Only claims declared in the schema can drive your adaptive content conditions.

Your trusted server exchanges the signed visitor JWT and target published URL for a short-lived content API token. Use the returned `Bearer` token to search content, list pages, and retrieve pages in that visitor's context.

Before implementing the flow, understand how retrieval behaves:

* A single-page request with `evaluated=true` resolves conditional blocks and inline expressions for the visitor. Without it, the API returns raw authored content.
* Search results and page lists omit content the visitor cannot view. A direct request for an ineligible page returns `404`.
* If the visitor JWT signature is invalid, GitBook evaluates content as an anonymous visitor. GitBook doesn't trust the supplied claims.

{% hint style="warning" %}
Create and exchange signed visitor JWTs only on a trusted server. Never expose the Visitor token signing key or content API token in browser code or logs.
{% endhint %}

### Pass visitor data to GitBook

GitBook provides different ways to pass visitor data to adapt your site's content. After defining your schema, you’ll need to decide how you want to pass your visitor data to GitBook.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><i class="fa-cookie">:cookie:</i></td><td><strong>Cookies</strong></td><td>Pass visitor data into your docs through a public or signed cookie.</td><td><a href="cookies.md">cookies.md</a></td></tr><tr><td><i class="fa-link">:link:</i></td><td><strong>URL</strong></td><td>Pass visitor data into your docs through URL query parameters.</td><td><a href="url.md">url.md</a></td></tr><tr><td><i class="fa-flag">:flag:</i></td><td><strong>Feature flags</strong></td><td>Pass visitor data into your docs through a feature flag provider.</td><td><a href="feature-flags.md">feature-flags.md</a></td></tr><tr><td><i class="fa-lock">:lock:</i></td><td><strong>Authenticated access</strong></td><td>Pass visitor data into your docs through an authentication provider.</td><td><a href="authenticated-access.md">authenticated-access.md</a></td></tr></tbody></table>
