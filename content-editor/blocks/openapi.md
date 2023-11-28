---
description: Add an OpenAPI spec to a page.
---

# OpenAPI methods

You can also sync with an OpenAPI or Swagger file or URL to include auto-generated methods in your documentation.

### Example of an OpenAPI block

{% swagger src="https://petstore.swagger.io/v2/swagger.json" path="/pet/{petId}" method="get" %}
[https://petstore.swagger.io/v2/swagger.json](https://petstore.swagger.io/v2/swagger.json)
{% endswagger %}

Manually writing documentation for your REST API can be time-consuming. To help, GitBook supports importing OpenAPI documents, which describe your API, and provides API Blocks to automatically represent your API methods based on the specification you provide, either as a file or as a URL for GitBook to load.

GitBook supports [Swagger 2.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/2.0.md) or [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md) compliant files.

### Create OpenAPI Block using your OpenAPI file

Once you have an OpenAPI compliant representation of your API, you can use it in your documentation.

1. **Create a new OpenAPI block using the insert palette.**
2. **Add your OpenAPI specification**:
   1. Upload your OpenAPI formatted file
   2. Provide a URL to your publicly available OpenAPI file.

If you're providing a **URL**, make sure that the file is available on the open internet, and that it's not behind any kind of password protection.

If you're just experimenting, you can use one of the [default Swagger files](https://petstore.swagger.io/#/):

`https://petstore.swagger.io/v2/swagger.json`

3. Choose your API operation

To change the operation that your swagger block is showing, use the "Choose API Operation" option in the block menu

4. Show more than one operation

Chances are good that your API has more than one operation that you'll want to document. Each OpenAPI block shows one API operation. In order to show multiple API operations, you can create an extra OpenAPI block per operation, backed by the same OpenAPI specification file.

### Update your specification

From time to time you might need to update or modify your API specification. In GitBook, you can replace the specification underlying your OpenAPI blocks, and have the update be reflected across all your documentation.

#### Replacing a specification in a file

1. Using the Block context menu on one of your OpenAPI Blocks, select "Choose OpenAPI Source"
2. On your OpenAPI file in the file list, click "Replace"

Once the OpenAPI Source has been replaced, each OpenAPI block that references your file will be updated based on your new specification.

#### Replacing a specification from a link

1. Using the Block context menu on one of your OpenAPI Blocks, select "Choose OpenAPI Source"
2. Provide a new URL in the input box, and save

Once the OpenAPI Source has been replaced, each OpenAPI block that references your file will be updated based on your new specification.
