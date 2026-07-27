---
description: Organize generated API reference pages.
---

# Structure your API reference

GitBook does more than render your OpenAPI spec — you can customize your API reference's layout, navigation, and branding.

## OpenAPI layouts

When you insert an **OpenAPI Reference**, GitBook organizes operations one of two ways. To choose, click **Add new...** → **OpenAPI Reference** (or edit an existing one), pick your spec, then choose a **Page structure** — see [Add an OpenAPI spec](add-an-openapi-spec.md#insert-api-reference-in-your-docs) for the full flow.

Both layouts start from the same data:

{% code title="openapi.yaml" %}
```yaml
paths:
  /users:
    get:
      tags:
        - users
      summary: List users
    post:
      tags:
        - users
      summary: Create user
```
{% endcode %}

**One page per tag** creates one page per tag, listing every operation with that tag — both operations above appear on the same `users` page. Use this when each tag is a clear section of your API, and you want overview pages with fewer navigation entries.

**One page per operation** creates one page per operation, grouped by tag in the table of contents — `GET /users` and `POST /users` each get their own page, both under the `users` group. Use this for larger APIs, or when each endpoint needs its own direct link.

**Quick recommendation:** one page per tag for smaller APIs; one page per operation for larger ones, or when you want a dedicated page per endpoint.

## Use tags to organize generated pages

In both layouts, GitBook uses tags to organize pages. Assign the same tag to related operations to group them:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
<strong>      tags:
</strong><strong>        - pet
</strong>      summary: Update an existing pet.
      description: Update an existing pet by Id.
      operationId: updatePet
</code></pre>

### Reorder pages

Generated tag pages or groups follow the order of your `tags` array:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">tags:
<strong>  - name: pet
</strong><strong>  - name: store
</strong><strong>  - name: user
</strong></code></pre>

### Nest pages into groups

Use `x-parent` (or `parent`, on OpenAPI 3.2+) on a tag to build multi-level navigation, in either layout:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">tags:
  - name: everything
  - name: pet
<strong>    x-parent: everything
</strong>  - name: store
<strong>    x-parent: everything
</strong></code></pre>

This creates:

```
Everything
├── Pet
└── Store
```

If a generated parent page has no description, GitBook shows a card-based layout for its sub-pages.

### Customize page titles, icons, and descriptions

Enhance generated tag pages with extensions on the `tags` entry. All [Font Awesome icons](https://fontawesome.com/search) are supported via `x-page-icon`:

{% code title="openapi.yaml" %}
```yaml
tags:
  - name: pet
    # Page title displayed in table of contents and page
    x-page-title: Pet
    # Icon shown in table of contents and next to page title
    x-page-icon: dog
    # Description shown just above the title
    x-page-description: Pets are amazing!
    # Content of the page
    description: Everything about your Pets
```
{% endcode %}

### Build rich descriptions with GitBook blocks

Tag `description` fields support GitBook markdown, including [advanced blocks](../creating-content/blocks/README.md) like tabs:

{% code title="openapi.yaml" %}
```yaml
tags:
  - name: pet
    description: |
      Here is the detail of pets.

      {% tabs %}
      {% tab title="Dog" %}
      Here are the dogs
      {% endtab %}

      {% tab title="Cat" %}
      Here are the cats
      {% endtab %}

      {% tab title="Rabbit" %}
      Here are the rabbits
      {% endtab %}
      {% endtabs %}
```
{% endcode %}

### Highlight schemas

Highlight a schema in a description using GitBook markdown — this example highlights the "Pet" schema from the "petstore" spec:

{% code title="openapi.yaml" %}
```yaml
tags:
  - name: pet
    description: |
      {% openapi-schemas spec="petstore" schemas="Pet" grouped="false" %}
      The Pet object
      {% endopenapi-schemas %}
```
{% endcode %}

### Document a webhook endpoint

GitBook supports OpenAPI 3.1 webhooks. Your spec must declare `openapi: 3.1.0` or later — define webhooks directly in your file, and GitBook renders them alongside your other operations:

{% code title="openapi.yaml" %}
```yaml
openapi: 3.1.0 # Webhooks are available starting from OpenAPI 3.1

webhooks:
  newPet:
    post:
      summary: New pet event
      description: Information about a new pet in the system
      requestBody:
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Pet"
      responses:
        "200":
          description: Return a 200 status to indicate that the data was received successfully
```
{% endcode %}

## Managing operation visibility and status

Operations aren't always fully stable, or need to be phased out. A few extensions help manage this — see [OpenAPI extensions](openapi-extensions.md) for the full reference.

**Mark an operation experimental, alpha, or beta** with `x-stability`, so readers avoid non-production-ready endpoints:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      x-stability: experimental
</strong></code></pre>

**Deprecate an operation** with `deprecated: true`, optionally with a sunset date via `x-deprecated-sunset`:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      deprecated: true
</strong><strong>      x-deprecated-sunset: 2030-12-05
</strong></code></pre>

**Hide an operation** from the reference entirely with `x-internal: true` or `x-gitbook-ignore: true`:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      x-internal: true
</strong></code></pre>

**Hide a response sample** with `x-hideSample: true` on a response object:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
      operationId: updatePet
<strong>      responses:
</strong><strong>        200:
</strong><strong>          x-hideSample: true
</strong></code></pre>

**Customize the authorization prefix and token placeholder** shown for a security scheme, under `components.securitySchemes`:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">components:
  securitySchemes:
    apiKey:
      type: apiKey
      in: header
      name: Authorization
<strong>      x-gitbook-prefix: Token
</strong><strong>      x-gitbook-token-placeholder: YOUR_CUSTOM_TOKEN
</strong></code></pre>

* `x-gitbook-prefix` sets the prefix before the token, e.g. `Authorization: <x-gitbook-prefix> YOUR_API_TOKEN`.
* `x-gitbook-token-placeholder` sets the default token value, e.g. `Authorization: Bearer <x-gitbook-token-placeholder>`.

{% hint style="warning" %}
`x-gitbook-prefix` isn't supported for `http` security schemes, since those must follow standard IANA authentication definitions. [Learn more](https://www.iana.org/assignments/http-authschemes/http-authschemes.xhtml).
{% endhint %}
