---
description: Add an OpenAPI spec to a page.
---

# OpenAPI methods

You can sync with an OpenAPI or Swagger file or URL to include auto-generated methods in your documentation.

{% hint style="info" %}
After adding your OpenAPI specification to GitBook, you’ll see a condensed version of the API block in the in-app editor. We’re working on consolidating both the in-app editor view and the published content view.
{% endhint %}

### Example of an OpenAPI block

{% swagger src="https://petstore3.swagger.io/api/v3/openapi.json" path="/pet" method="post" %}
[https://petstore3.swagger.io/api/v3/openapi.json](https://petstore3.swagger.io/api/v3/openapi.json)
{% endswagger %}

Manually writing documentation for your REST API can be time-consuming. To help, GitBook supports OpenAPI document imports, which describe your API, and provides API blocks. These will automatically represent your API methods based on the specification you provide — either as a file or as a URL for GitBook to load.

GitBook supports [Swagger 2.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/2.0.md) or [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md) compliant files.

### Create OpenAPI block using your OpenAPI file

Once you have an OpenAPI compliant representation of your API, you can use it in your documentation.

1. **Create a new OpenAPI block using the insert palette.**
2. **Add your OpenAPI specification, choosing between one of the following options**:
   1. Upload your OpenAPI formatted file
   2. Provide a URL to your publicly available OpenAPI file.

If you’re providing a **URL**, make sure that the file is available on the open internet, and that it’s not behind any kind of password protection.

If you’re just experimenting, you can use one of the [default Swagger files](https://petstore.swagger.io/#/):

`https://petstore.swagger.io/v2/swagger.json`

3. Choose your API operation

To change the operation that your swagger block is showing, use the "Choose API Operation" option in the block menu

4. Show more than one operation

Your API is likely to have more than one operation that you'll want to document. Each OpenAPI block shows one API operation. In order to show multiple API operations, you can create an extra OpenAPI block per operation, backed by the same OpenAPI specification file.

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

### API method block (deprecated)

{% hint style="danger" %}
**Editable API method blocks are now deprecated**

In light of our updated OpenAPI method block, **we’ve decided to deprecate the API method block.** [Read our recent announcement](https://changelog.gitbook.com/announcements/depreciating-api-method-block) to find out more about the reasons behind this change.

On **Monday 4 March 2024**, we automatically transitioned all pre-existing API method blocks to regular blocks in the format you can see below. [Read our announcement](https://changelog.gitbook.com/announcements/depreciating-api-method-block) to find out more.
{% endhint %}

You can still create editable API references from the **Quickstart** section of the **Insert menu**. Hit / on your keyboard and select **API Reference**. GitBook will create an editable section that looks like this:

## Create a new user

<mark style="color:green;">`POST`</mark> `/users`

\<Description of the endpoint>

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body**

| Name   | Type   | Description      |
| ------ | ------ | ---------------- |
| `name` | string | Name of the user |
| `age`  | number | Age of the user  |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "id": 1,
  "name": "John",
  "age": 30
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}
