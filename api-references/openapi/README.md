---
description: >-
  Add an OpenAPI spec to a page and let your users test endpoints right on the
  page with interactive blocks
icon: brackets-curly
---

# OpenAPI

Manually writing REST API documentation can be a time-consuming process. Fortunately, GitBook streamlines this task by allowing you to import OpenAPI documents, which detail your API’s structure and functionality.

The OpenAPI Specification (OAS) is a framework that developers use to document REST APIs. Written in JSON or YAML, it outlines all your endpoints, parameters, schemas, and authentication schemes.

Once imported into GitBook, these documents are transformed into interactive and testable API blocks that visually represent your API methods—whether the specification is provided as a file or loaded from a URL.

GitBook supports [Swagger 2.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/2.0.md) or [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md) compliant files.

{% openapi src="https://petstore3.swagger.io/api/v3/openapi.json" path="/pet" method="post" %}
[https://petstore3.swagger.io/api/v3/openapi.json](https://petstore3.swagger.io/api/v3/openapi.json)
{% endopenapi %}

### Test it (powered by Scalar)

GitBook's OpenAPI block also supports a "test it" functionality, which allows your users to test your API methods with data and parameters filled in from the editor.

Powered by [Scalar](https://scalar.com/), you won't need to leave the docs in order to see your API methods in action. See and example of this above.

### API method block (deprecated)

{% hint style="warning" %}
**Editable API method blocks are now deprecated**

In light of our updated OpenAPI method block, **we’ve decided to deprecate the API method block.** [Read our recent announcement](https://changelog.gitbook.com/announcements/depreciating-api-method-block) to find out more about the reasons behind this change.

On **Monday 4 March 2024**, we automatically transitioned all pre-existing API method blocks to regular blocks in the format you can see below. [Read our announcement](https://changelog.gitbook.com/announcements/depreciating-api-method-block) to find out more.
{% endhint %}

You can still create editable API references from the **Quickstart** section of the **Insert menu**. Hit / on your keyboard and select **API Reference**.
