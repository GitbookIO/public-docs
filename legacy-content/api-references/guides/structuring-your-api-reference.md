---
description: >-
  Learn how to structure your API reference across multiple pages with icons and
  descriptions
---

# Structuring your API reference

GitBook does more than just render your OpenAPI spec. It lets you customize your API reference for better clarity, navigation, and branding.

To choose between **One page per tag** and **One page per operation**, see [OpenAPI layouts](openapi-layouts.md).

This page explains how to control the generated navigation with tags.

### Use tags to organize generated pages

GitBook uses tags to organize generated API reference pages in both layouts.

With **One page per tag**, GitBook creates one page for each tag. With **One page per operation**, GitBook creates one page for each operation and uses tags to group those pages in the table of contents.

To group related operations, assign the same tag to each operation:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">paths:
  /pet:
    put:
<strong>      tags:
</strong><strong>        - pet
</strong>      summary: Update an existing pet.
      description: Update an existing pet by Id.
      operationId: updatePet
</code></pre>

### Reorder pages in your table of contents

The order of generated tag pages or tag groups matches the order of tags in your OpenAPI `tags` array:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">tags:
<strong>  - name: pet
</strong><strong>  - name: store
</strong><strong>  - name: user
</strong></code></pre>

### Nest pages into groups

To build multi-level navigation, use `x-parent` (or `parent`) in tags to define hierarchy. This works with both page structures:

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">tags:
  - name: everything
  - name: pet
<strong>    x-parent: everything
</strong>  - name: store
<strong>    x-parent: everything
</strong></code></pre>

The above example creates a table of contents like this:

```
Everything
├── Pet
└── Store
```

If GitBook generates a parent page and that page has no description, it shows a card-based layout for its sub-pages.

### Customize page titles, icons, and descriptions

You can enhance generated tag pages and navigation labels with custom extensions in the `tags` section. All [Font Awesome icons](https://fontawesome.com/search) are supported via `x-page-icon`.

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

### Build rich descriptions with GitBook Blocks

Tag description fields support GitBook markdown, including [advanced blocks](../../creating-content/blocks/) like tabs:

{% code title="openapi.yaml" %}
```yaml
---
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

You can highlight a schema in a GitBook description by using GitBook markdown. Here is an example that highlights the “Pet” schema from the “petstore” specification:

{% code title="openapi.yaml" %}
```yaml
---
tags:
  - name: pet
      description: |
          {% openapi-schemas spec="petstore" schemas="Pet" grouped="false" %}
              The Pet object
          {% endopenapi-schemas %}
```
{% endcode %}

### Document a webhook endpoint

GitBook supports OpenAPI 3.1, including webhook endpoints.

The `webhooks` field is part of OpenAPI 3.1, so your specification must declare an OpenAPI 3.1 version. You can define webhooks directly in your OpenAPI file, and GitBook renders them alongside your other API operations. For version support across OpenAPI docs, see [OpenAPI compatibility](../openapi/#openapi-compatibility).

{% code title="openapi.yaml" %}
```yaml
---
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
