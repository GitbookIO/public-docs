---
description: Add an API method to a page.
---

# API methods

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
