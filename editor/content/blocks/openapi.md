---
description: >-
  OpenAPI content block. It allows using swagger files or external public URLs
  to reuse your existing API representation.
---

# OpenAPI

You can also sync with an OpenAPI or Swagger file or URL to include auto-generated methods in your documentation.

### Example

{% swagger src="https://petstore.swagger.io/v2/swagger.json" path="/pet/{petId}" method="get" %}
[https://petstore.swagger.io/v2/swagger.json](https://petstore.swagger.io/v2/swagger.json)
{% endswagger %}

