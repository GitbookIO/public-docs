---
description: How GitBook turns an OpenAPI spec into API reference pages.
---

# How GitBook renders OpenAPI

Manually writing REST API documentation is time-consuming. GitBook streamlines this by importing OpenAPI documents — the structure and functionality of your API — and rendering them as interactive, testable pages.

The OpenAPI Specification (OAS) is the framework developers use to document REST APIs, written in JSON or YAML, describing your endpoints, parameters, schemas, and authentication schemes. Once imported, GitBook turns these into interactive API blocks that visually represent your API's methods, whether the spec comes from a file or a URL.

### OpenAPI compatibility

GitBook supports importing and rendering:

* [Swagger 2.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/2.0.md)
* [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md)
* [OpenAPI 3.1](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.1.md), including 3.1-only features like `webhooks`

{% openapi src="https://petstore3.swagger.io/api/v3/openapi.json" path="/pet" method="post" %}
[https://petstore3.swagger.io/api/v3/openapi.json](https://petstore3.swagger.io/api/v3/openapi.json)
{% endopenapi %}

### "Test it," powered by Scalar

GitBook's OpenAPI block supports "Test it" — readers can test your API methods with data and parameters filled in from the editor, powered by [Scalar](https://scalar.com/), without leaving your docs. See [Configure the "Test it" button](configure-the-test-it-button.md) to hide it, add authentication, or route requests through GitBook's proxy.
