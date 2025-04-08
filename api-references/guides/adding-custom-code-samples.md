---
description: Configure custom code samples to display alongside your API endpoints.
---

# Adding custom code samples

{% include "../../.gitbook/includes/openapi-availability-hint.md" %}

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
