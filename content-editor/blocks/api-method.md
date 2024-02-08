---
description: Add an API method to a page.
---

# API method

{% hint style="danger" %}
#### We are depreciating the API method block

We’re working on some major improvements to how teams can document APIs in GitBook.  **As a result, we’ve decided to deprecate the API method block.** [Read our recent announcement](https://changelog.gitbook.com/announcements/depreciating-api-method-block) to find out more about the reasons behind this change.

From **Monday 13 February**, you will no longer be able to add API method blocks to your content in GitBook.&#x20;

On **Monday 4 March**, we’ll automatically transition all pre-existing API method blocks to regular text blocks. [Read our announcement](https://changelog.gitbook.com/announcements/depreciating-api-method-block) to find out more.
{% endhint %}

An API method block is used to manually document an HTTP API endpoint.

### Example of API method block

{% swagger method="get" path="/user" baseUrl="https://api.example.com/v1" summary="Get a user" expanded="false" %}
{% swagger-description %}
Use this method to get information about a user.
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" %}
ID of the user to lookup
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="User details" %}
```json
{
  "id": "eoziwgldfkj18239J30kd1Dj",
  "email": "user@example.com",
  "firstName": "Happy",
  "lastName": "User"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid ID provided" %}

{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
You can make API method blocks [span the full width of your window](./#full-width-blocks) by clicking on the **Options menu** <img src="../../.gitbook/assets/Options menu.png" alt="" data-size="line">  next to the block and choosing **Full width**.
{% endhint %}

#### Related: <a href="#please-also-check" id="please-also-check"></a>

{% content-ref url="openapi.md" %}
[openapi.md](openapi.md)
{% endcontent-ref %}

## Representation in Markdown

```
# API

{% raw %}
{% swagger method="get" path="" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}
{% endraw %}
```
