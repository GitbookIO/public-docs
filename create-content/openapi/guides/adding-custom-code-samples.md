---
description: >-
  Learn how to configure custom code samples to display alongside your API
  endpoints
---

# Adding custom code samples

GitBook can automatically generate generic code examples for each API operation. If you’d prefer to showcase custom or more detailed snippets, add `x-codeSamples` to your OpenAPI definition. This way, you control how your endpoints are demonstrated and can offer language or SDK-specific examples.

{% code title="openapi.yaml" %}
```yaml
paths:
  /users:
    get:
      summary: Retrieve users
      x-codeSamples:
        - lang: JavaScript
          label: Node SDK
          source: |
            import { createAPIClient } from 'my-api-sdk';

            const client = createAPIClient({ apiKey: 'my-api-key' });
            client.users.list().then(users => {
              console.log(users);
            });
        - lang: Java
          label: Java SDK
          source: |
            MyApiClient client = new MyApiClient("my-api-key");
            List<User> users = client.getUsers();
            System.out.println(users);
```
{% endcode %}

**Key Points**

* `x-codeSamples` is an array of code sample objects.
* Each object defines:
  * `lang`: The language of the code (e.g., JavaScript, Java).
  * `label`: A short label for the code block.
  * `source`: The actual code snippet.

### Quick guide

<details>

<summary>How do I add custom code samples from Fern?</summary>

Use Fern-generated SDK examples as custom code samples in your OpenAPI definition.

This guide covers finding the generated examples, formatting `x-codeSamples`, and adding them to an API operation.

<button type="button" class="button secondary" data-action="ask" data-query="How do I add custom code samples from Fern to my GitBook API documentation? Show me how to find Fern-generated SDK examples, format x-codeSamples, and add them to an OpenAPI operation. Include links to the relevant docs pages." data-icon="gitbook-assistant">Open guide</button>

</details>

<details>

<summary>How do I add custom code samples from Stainless?</summary>

Use Stainless-generated SDK examples as custom code samples in your OpenAPI definition.

This guide covers finding the generated examples, formatting `x-codeSamples`, and adding them to an API operation.

<button type="button" class="button secondary" data-action="ask" data-query="How do I add custom code samples from Stainless to my GitBook API documentation? Show me how to find Stainless-generated SDK examples, format x-codeSamples, and add them to an OpenAPI operation. Include links to the relevant docs pages." data-icon="gitbook-assistant">Open guide</button>

</details>

<details>

<summary>How do I add custom code samples from HeyAPI?</summary>

Use HeyAPI-generated SDK examples as custom code samples in your OpenAPI definition.

This guide covers finding the generated examples, formatting `x-codeSamples`, and adding them to an API operation.

<button type="button" class="button secondary" data-action="ask" data-query="How do I add custom code samples from HeyAPI to my GitBook API documentation? Show me how to find HeyAPI-generated SDK examples, format x-codeSamples, and add them to an OpenAPI operation. Include links to the relevant docs pages." data-icon="gitbook-assistant">Open guide</button>

</details>
