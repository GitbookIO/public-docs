---
description: >-
  Learn how to mark an OpenAPI API operation as experimental, deprecated or hide
  it from your documentation
---

# Managing API operations

It’s common to have operations that are not fully stable yet or that need to be phased out. GitBook supports several OpenAPI extensions to help you manage these scenarios.

### Marking operation as experimental, alpha, or beta

Use `x-stability` to communicate that an endpoint is unstable or in progress. It helps users avoid non-production-ready endpoints. Supported values: `experimental`, `alpha`, `beta`.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      x-stability: experimental
</strong></code></pre>

### Deprecating an operation

To mark an operation as deprecated, add the `deprecated: true` attribute.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      deprecated: true
</strong></code></pre>

Optionally specify when support ends by including `x-deprecated-sunset`&#x20;

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      deprecated: true
</strong><strong>      x-deprecated-sunset: 2030-12-05
</strong></code></pre>

### Hiding an operation from the API reference

To hide an operation from your API reference, add `x-internal: true` or `x-gitbook-ignore: true` attribute.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      x-internal: true
</strong></code></pre>

### Hiding a response sample

Add the `x-hideSample: true` attribute to a response object to exclude it from the response samples section.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      responses:
</strong><strong>        200:
</strong><strong>          x-hideSample: true
</strong></code></pre>

### Customizing the authorization prefix and token placeholder

You can customize the authorization prefix (for example, `Bearer`, `Token`, or a custom string) and the token placeholder shown when using security schemes in GitBook.

In your OpenAPI spec, under `components.securitySchemes`, define your scheme like this:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">components:
  securitySchemes:
    apiKey:
      type: apiKey
      in: header
      name: Authorization
<strong>      x-gitbook-prefix: Token
</strong><strong>      x-gitbook-token-placeholder: YOUR_CUSTOM_TOKEN
</strong></code></pre>

These extensions:

* `x-gitbook-prefix` defines the prefix added before the token.
  * example: `Authorization: <x-gitbook-prefix> YOUR_API_TOKEN`
* `x-gitbook-token-placeholder` sets the default token value.
  * example: `Authorization: Bearer <x-gitbook-token-placeholder>`

{% hint style="warning" %}
`x-gitbook-prefix` is not supported for `http` security schemes because these schemes must follow standard IANA authentication definitions. [Learn more](https://www.iana.org/assignments/http-authschemes/http-authschemes.xhtml)
{% endhint %}
