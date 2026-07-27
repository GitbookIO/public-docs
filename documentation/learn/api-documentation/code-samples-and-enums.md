---
description: Customize code samples and document enum values.
---

# Code samples and enum descriptions

## Custom code samples

GitBook automatically generates generic code examples for each operation. For custom or more detailed snippets — language- or SDK-specific — add `x-codeSamples` to your OpenAPI definition:

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

`x-codeSamples` is an array of objects, each with:

* `lang` — the code's language (e.g. JavaScript, Java)
* `label` — a short label for the code block
* `source` — the code snippet itself

## Enum descriptions

To add context to an enum's options, add `x-enumDescriptions` — GitBook displays the values and descriptions in a table next to the operation:

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
