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

Please also check:

{% content-ref url="openapi.md" %}
[openapi.md](openapi.md)
{% endcontent-ref %}
