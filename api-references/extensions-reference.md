---
description: The complete reference of OpenAPI extensions supported by GitBook
icon: code
---

# Extensions reference

You can enhance your OpenAPI specification using extensions—custom fields that start with the `x-` prefix. These extensions let you add extra information and tailor your API documentation to suit different needs.

GitBook allows you to adjust how your API looks and works on your published site through a range of different extensions you can add to your OpenAPI spec.&#x20;

Head to our [guides section](guides/) to learn more about using OpenAPI extensions to configure your documentation.

<details>

<summary><code>x-page-title | x-displayName</code></summary>

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

Add a Font Awesome icon to the page. See available icons [here](https://fontawesome.com/search).

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

<summary><code>parent | x-parent</code>  </summary>

Add hierarchy to tags to organize your pages in GitBook.&#x20;

{% hint style="warning" %}
`parent` is the official property name in OpenAPI 3.2+. If using OpenAPI versions prior to 3.2 (3.0.x, 3.1.x),  use `x-parent` instead.
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

Show or hide the “Test it” button for an OpenAPI block.

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

<summary><code>x-codeSamples</code></summary>

Show, hide, or include custom code samples for an OpenAPI block.

#### Fields

<table><thead><tr><th width="103.625">Field Name</th><th width="88.07421875" align="center">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>lang</code></td><td align="center">string</td><td>Code sample language. Value should be one of the following <a href="https://github.com/github/linguist/blob/master/lib/linguist/popular.yml">list</a></td></tr><tr><td><code>label</code></td><td align="center">string</td><td>Code sample label, for example <code>Node</code> or <code>Python2.7</code>, <em>optional</em>, <code>lang</code> is used by default</td></tr><tr><td><code>source</code></td><td align="center">string</td><td>Code sample source code</td></tr></tbody></table>

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

Add an individual description for each of the `enum` values in your schema.

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

<summary><code>x-internal | x-gitbook-ignore</code></summary>

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

<summary><code>x-stability</code></summary>

Mark endpoints that are unstable or in progress.&#x20;

Supported values: `experimental`, `alpha`, `beta`.

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

Mark whether an endpoint is deprecated or not. Deprecated endpoints will give deprecation warnings in your published site.

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

Add a sunset date to a deprecated operation.&#x20;

Supported values: **ISO 8601** format (YYYY-MM-DD)

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
