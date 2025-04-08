# Organize your endpoints

{% include "../../.gitbook/includes/openapi-availability-hint.md" %}

GitBook allows you to automatically generate pages related to the endpoints you have in your OpenAPI spec. These pages will contain OpenAPI blocks, allowing you and your visitors to test your endpoints and explore them further based on the information found in the spec.

{% hint style="success" %}
Endpoints added from your spec will continue to be updated anytime your spec is updated. See the [Update your specification](add-an-openapi-specification.md#update-your-specification) section for more info.
{% endhint %}

### Automatically create OpenAPI pages from your spec

After you’ve [added your OpenAPI spec](add-an-openapi-specification.md), you can generate endpoint pages for your spec using our OpenAPI integration.

<figure><img src="../../.gitbook/assets/03_04_25_create_api_pages.svg" alt=""><figcaption><p>Add API References to a Space.</p></figcaption></figure>

{% stepper %}
{% step %}
### Generate pages from OpenAPI

In the space you’d like to generate endpoint pages, click the “Add new...” button from the bottom of your space’s [table of contents](../../resources/gitbook-ui.md#table-of-contents).

From here, click “OpenAPI Reference”.
{% endstep %}

{% step %}
### Choose your OpenAPI spec

Choose your previously uploaded OpenAPI spec, and click “Insert” to automatically add your endpoints to your space.
{% endstep %}
{% endstepper %}

### Add an OpenAPI block using your OpenAPI file

Alternatively, you can add OpenAPI blocks from your spec individually to pages throughout your docs.&#x20;

{% stepper %}
{% step %}
### Add a new OpenAPI block

Open the block selector by pressing “/“, and search for OpenAPI.
{% endstep %}

{% step %}
### Choose your OpenAPI spec

Choose your previously uploaded OpenAPI spec, and click “Continue” to choose your the endpoints you’d like to use.
{% endstep %}

{% step %}
### Choose the endpoints you’d like to display

Use the endpoint modal to choose the endpoints you’d like to add to your page
{% endstep %}
{% endstepper %}
