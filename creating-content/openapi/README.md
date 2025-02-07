---
icon: brackets-curly
description: >-
  Add an OpenAPI spec to a page and let your users test endpoints right on the
  page with interactive blocks
---

# OpenAPI

You can sync with an OpenAPI or Swagger file or URL to include auto-generated methods in your documentation.

### Test it (powered by Scalar)

GitBook's OpenAPI block also supports a "try it" functionality, which allows your users to test your API methods with data and parameters filled in from the editor.

Powered by [Scalar](https://scalar.com/), you won't need to leave the docs in order to see your API methods in action. See and example of this below.

{% swagger src="https://petstore3.swagger.io/api/v3/openapi.json" path="/pet" method="post" %}
[https://petstore3.swagger.io/api/v3/openapi.json](https://petstore3.swagger.io/api/v3/openapi.json)
{% endswagger %}

Manually writing documentation for your REST API can be time-consuming. To help, GitBook supports OpenAPI document imports, which describe your API, and provides API blocks. These will automatically represent your API methods based on the specification you provide — either as a file or as a URL for GitBook to load.

GitBook supports [Swagger 2.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/2.0.md) or [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md) compliant files.

### Options

GitBook supports extra options you can define in your OpenAPI specification to alter they way your API methods display in your published documentation.

<details>

<summary><strong><code>x-hideTryItPanel</code></strong></summary>

Show or hide the “Test it” button for an OpenAPI block.

#### **Values**

`true` | `false`

#### **Root level**

{% code title="openapi.yaml" %}
```yaml
...
x-hideTryItPanel: false
...
```
{% endcode %}

#### **Operation level**

{% code title="openapi.yaml" %}
```yaml
...
paths:
  /user
    get:
      summary: Get the current user
      x-hideTryItPanel: true
...
```
{% endcode %}

</details>

<details>

<summary><strong><code>x-codeSamples</code></strong></summary>

Show or hide code samples for an OpenAPI block Custom code samples are supported, from tools such as [Stainless](https://www.stainless.com/) and more by [configuring the output](support-for-ci-cd-with-api-blocks.md#configure-third-party-tools-and-frameworks) from your tool.

#### Values

&#x20;`true` | `false` | `custom`

#### Root level

{% code title="openapi.yaml" %}
```yaml
...
x-codeSamples: false
...
```
{% endcode %}

#### Operation level

<pre class="language-yaml" data-title="openapi.yaml"><code class="lang-yaml">...
<strong>paths:
</strong>  /user
    get:
      x-codeSamples:
        - lang: 'cURL'
          label: CLI
          source: | 
            curl -L \
            -H 'Authorization: Bearer &#x3C;token>' \
            'https://api.gitbook.com/v1/user'
...
</code></pre>

</details>

### Create an OpenAPI block using your OpenAPI file

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
