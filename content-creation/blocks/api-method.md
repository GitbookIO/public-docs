---
description: API method content block
---

# API method

An API Method block is used to manually document an HTTP API endpoint.

### Example of API Method block

{% swagger method="get" path="/user" baseUrl="https://api.example.com/v1" summary="Get a user" %}
{% swagger-description %}
Use this method to get information about a user
{% endswagger-description %}
{% endswagger %}

{% hint style="info" %}
You can now convert the API blocks to full width by clicking on the <img src="../../.gitbook/assets/image (1).png" alt="" data-size="line"> next to the block. [Read more about full-width blocks.](./#new-full-width-blocks)
{% endhint %}

#### Please also check:

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
