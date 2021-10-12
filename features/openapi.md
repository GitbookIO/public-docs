# OpenAPI

{% swagger method="get" path="/user" baseUrl="https://app.com/api" summary="Get a user" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}

Manually writing documentation for your REST API can be time consuming. To help, GitBook supports importing OpenAPI documents, which describe your API, and provides API Blocks to automatically represent your API methods based on the specification you provide, either as a file, or as a URL for GitBook to load.

GitBook supports [Swagger 2.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/2.0.md) or [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md) compliant files.

### Creating an OpenAPI Block using your OpenAPI file

Once you have an OpenAPI compliant representation of your API, you can use it in your documentation.

#### **1. Create a new OpenAPI block** using the command palette, and select 'OpenAPI'.

![](<../.gitbook/assets/Open API.gif>)

#### 2. Either:

* **Upload** your OpenAPI formatted file, _or_
* Provide a **URL** to your publicly available OpenAPI file.

![](<../.gitbook/assets/OpenAPI Source.png>)

If you're providing a **URL**, make sure that the file is available on the open internet, and that it's not behind any kind of password protection.

If you're just experimenting, you can use one of the [default Swagger files](https://petstore.swagger.io/#/):

`https://petstore.swagger.io/v2/swagger.json`

#### **3. Check out your OpenAPI block!**

OpenAPI blocks can be expanded and collapsed to show and hide more detail about the API endpoint.

![](<../.gitbook/assets/OpenAPI Expanded.png>)

#### **4. Choose your API operation**

To change the operation that your swagger block is showing, use the "Choose API Operation" option in the block menu

![](<../.gitbook/assets/OpenAPI Operation.gif>)

#### **5. Show more than one operation**

Chances are good that your API has more than one operation that you'll want to document. Each OpenAPI block shows one API operation. In order to show multiple API operations, you can create an extra OpenAPI block per operation, backed by the same OpenAPI specification file.

### Updating your Specification

From time to time you might need to update or modify your API specification. In GitBook, you can replace the specification underlying your OpenAPI blocks, and have the update be reflected across all your documentation.

#### Replacing a specification in a file

1. Using the Block context menu on one of your OpenAPI Blocks, select "Choose OpenAPI Source"
2. On your OpenAPI file in the file list, click "Replace"

Once the OpenAPI Source has been replaced, each OpenAPI block that references your file will be updated based on your new specification.

#### Replacing a specification from a link

![](<../.gitbook/assets/OpenAPI Source.png>)

1. Using the Block context menu on one of your OpenAPI Blocks, select "Choose OpenAPI Source"
2. Provide a new URL in the input box, and save

Once the OpenAPI Source has been replaced, each OpenAPI block that references your file will be updated based on your new specification.

### Creating an API Operation from scratch

GitBook supports creating API methods from scratch, using the editable "API Method" Block. To use the "API Method" block, create a new block using the command palette, and select "API Method". Each field in the block is editable, and displays just like an OpenAPI block.

![](<../.gitbook/assets/API Block From Scratch.png>)

With the API block, you can:

* Set the URL and the path of your operation
* Name your operation and give it a longer description or summary
* Add, remove, and reorder **parameters**, grouped into **Path**, **Query**, **Header**, **Cookie** and **Body**
* Add, remove, and reorder **responses**
  * Document your responses with code examples
