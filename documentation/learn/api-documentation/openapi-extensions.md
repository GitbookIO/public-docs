---
description: Reference for GitBook's x- extensions to OpenAPI.
---

# OpenAPI extensions

You can enhance your OpenAPI spec using extensions — custom fields prefixed with `x-` — to add extra information and tailor your API documentation. See [Structure your API reference](structure-your-api-reference.md), [Code samples and enum descriptions](code-samples-and-enums.md), and [Configure the "Test it" button](configure-the-test-it-button.md) for guides on using many of these; this page is the complete lookup reference.

<details>

<summary><code>x-page-title</code> | <code>x-displayName</code></summary>

Change the display name of a tag used in the navigation and page title.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags:
  - name: users
    x-page-title: Users
```
{% endcode %}

</details>

<details>

<summary><code>x-page-description</code></summary>

Add a description to the page.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags:
  - name: "users"
    x-page-title: "Users"
    x-page-description: "Manage user accounts and profiles."
```
{% endcode %}

</details>

<details>

<summary><code>x-page-icon</code></summary>

Add a [Font Awesome icon](https://fontawesome.com/search) to the page.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags:
  - name: "users"
    x-page-title: "Users"
    x-page-description: "Manage user accounts and profiles."
    x-page-icon: "user"
```
{% endcode %}

</details>

<details>

<summary><code>parent</code> | <code>x-parent</code></summary>

Add hierarchy to tags to organize your pages.

{% hint style="warning" %}
`parent` is the official property name in OpenAPI 3.2+. For earlier versions (3.0.x, 3.1.x), use `x-parent`.
{% endhint %}

{% code title="openapi.yaml" %}
```yaml
openapi: '3.2'
info: ...
tags:
  - name: organization
  - name: admin
    parent: organization
  - name: user
    parent: organization
```
{% endcode %}

</details>

<details>

<summary><code>x-hideTryItPanel</code></summary>

Show or hide the "Test it" button for an OpenAPI block.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags: [...]
paths:
  /example:
    get:
      summary: Example summary
      description: Example description
      operationId: examplePath
      responses: [...]
      parameters: [...]
      x-hideTryItPanel: true
```
{% endcode %}

</details>

<details>

<summary><code>x-expandAllResponses</code></summary>

Expand all response sections by default, instead of showing only one at a time. Add it at the root to apply to every operation, or on an operation to apply to just that endpoint.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">openapi: '3.0'
info: ...

# Expand all responses for every operation
<strong>x-expandAllResponses: true
</strong>
paths:
  /pets:
    get:
      summary: List pets
      responses: [...]
      # Opt out for a single operation
<strong>      x-expandAllResponses: false
</strong></code></pre>

</details>

<details>

<summary><code>x-expandAllModelSections</code></summary>

Expand all model/schema sections by default, showing nested object properties without requiring interaction. Add it at the root to apply to every operation, or on an operation to apply to just that endpoint.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">openapi: '3.0'
info: ...

# Expand all model sections for every operation
<strong>x-expandAllModelSections: true
</strong>
paths:
  /pets:
    post:
      summary: Create a pet
      requestBody: [...]
      responses: [...]
      # Opt out for a single operation
<strong>      x-expandAllModelSections: false
</strong></code></pre>

</details>

<details>

<summary><code>x-enable-proxy</code></summary>

Route "Test it" requests through GitBook's OpenAPI proxy. Add it at the root to apply to every operation, or on an operation to override the root value.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0.3'
info: ...

# Enable proxy for all operations
x-enable-proxy: true

paths:
  /health:
    get:
      summary: Health check
      # Opt out for a single operation
      x-enable-proxy: false
      responses:
        '200':
          description: OK
```
{% endcode %}

See [Use the OpenAPI proxy](use-the-openapi-proxy.md) for more.

</details>

<details>

<summary><code>x-codeSamples</code></summary>

Show, hide, or include custom code samples for an OpenAPI block.

| Field | Type | Description |
|---|---|---|
| `lang` | string | Code sample language — one of this [list](https://github.com/github/linguist/blob/master/lib/linguist/popular.yml) |
| `label` | string | Code sample label, e.g. `Node` or `Python2.7` — optional, defaults to `lang` |
| `source` | string | Code sample source code |

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags: [...]
paths:
  /example:
    get:
      summary: Example summary
      description: Example description
      operationId: examplePath
      responses: [...]
      parameters: [...]
      x-codeSamples:
        - lang: 'cURL'
          label: 'CLI'
          source: |
            curl -L \
            -H 'Authorization: Bearer <token>' \
            'https://api.gitbook.com/v1/user'
```
{% endcode %}

</details>

<details>

<summary><code>x-enumDescriptions</code></summary>

Add an individual description for each `enum` value in a schema.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
components:
  schemas:
    project_status:
      type: string
      enum:
        - LIVE
        - PENDING
        - REJECTED
      x-enumDescriptions:
        LIVE: The project is live.
        PENDING: The project is pending approval.
        REJECTED: The project was rejected.
```
{% endcode %}

</details>

<details>

<summary><code>x-internal</code> | <code>x-gitbook-ignore</code></summary>

Hide an endpoint from your API reference.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags: [...]
paths:
  /example:
    get:
      summary: Example summary
      description: Example description
      operationId: examplePath
      responses: [...]
      parameters: [...]
      x-internal: true
```
{% endcode %}

</details>

<details>

<summary><code>x-hideSample</code></summary>

Exclude a response object from the response samples section.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      responses:
</strong><strong>        200:
</strong><strong>          x-hideSample: true
</strong></code></pre>

</details>

<details>

<summary><code>x-stability</code></summary>

Mark endpoints that are unstable or in progress. Supported values: `experimental`, `alpha`, `beta`.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags: [...]
paths:
  /example:
    get:
      summary: Example summary
      description: Example description
      operationId: examplePath
      x-stability: experimental
```
{% endcode %}

</details>

<details>

<summary><code>deprecated</code></summary>

Mark whether an endpoint is deprecated. Deprecated endpoints show deprecation warnings on your published site.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags: [...]
paths:
  /example:
    get:
      summary: Example summary
      description: Example description
      operationId: examplePath
      responses: [...]
      parameters: [...]
      deprecated: true
```
{% endcode %}

</details>

<details>

<summary><code>x-deprecated-sunset</code></summary>

Add a sunset date to a deprecated operation. Supported format: ISO 8601 (`YYYY-MM-DD`).

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags: [...]
paths:
  /example:
    get:
      summary: Example summary
      description: Example description
      operationId: examplePath
      responses: [...]
      parameters: [...]
      deprecated: true
      x-deprecated-sunset: 2030-12-05
```
{% endcode %}

</details>

<details>

<summary><code>x-gitbook-prefix</code> | <code>x-gitbook-token-placeholder</code></summary>

Customize the authorization prefix (e.g. `Bearer`, `Token`, or a custom string) and the token placeholder shown for a security scheme.

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">components:
  securitySchemes:
    apiKey:
      type: apiKey
      in: header
      name: Authorization
<strong>      x-gitbook-prefix: Token
</strong><strong>      x-gitbook-token-placeholder: YOUR_CUSTOM_TOKEN
</strong></code></pre>

* `x-gitbook-prefix` — the prefix before the token, e.g. `Authorization: <x-gitbook-prefix> YOUR_API_TOKEN`.
* `x-gitbook-token-placeholder` — the default token value, e.g. `Authorization: Bearer <x-gitbook-token-placeholder>`.

{% hint style="warning" %}
`x-gitbook-prefix` isn't supported for `http` security schemes, which must follow standard IANA authentication definitions.
{% endhint %}

</details>
