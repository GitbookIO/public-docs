---
description: Add descriptions to operations that include enums.
---

# Describing enums

{% include "../../.gitbook/includes/openapi-availability-hint.md" %}

When an API operation includes an enum, you can add `x-enumDescriptions` to provide more context about each option. GitBook will display the enum values and their descriptions in a table next to the operation.

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

