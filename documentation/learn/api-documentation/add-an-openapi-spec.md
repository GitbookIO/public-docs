---
description: Add a spec and insert API reference blocks into your pages.
---

# Add an OpenAPI spec and insert references

## Add a specification

Add your OpenAPI spec to your organization by uploading a file, linking a hosted URL, or using the [GitBook CLI](https://gitbook.com/docs/developers/integrations/reference). GitBook accepts Swagger 2.0, OpenAPI 3.0, and OpenAPI 3.1 for all three methods — see [OpenAPI compatibility](how-gitbook-renders-openapi.md#openapi-compatibility).

{% stepper %}
{% step %}
#### Open the OpenAPI section

Open **OpenAPI** in the sidebar and click **Add specification**.
{% endstep %}

{% step %}
#### Name it

Give your spec a name — this helps identify it if you manage several.
{% endstep %}

{% step %}
#### Choose a source

Upload a file (e.g. `openapi.yaml`), enter a URL to a hosted spec, or use the CLI to publish it.
{% endstep %}
{% endstepper %}

### Update your specification

Update your spec at any time, regardless of how it was added:

* **URL-linked specs** — GitBook checks for updates automatically every 6 hours, or click **Check for updates** to fetch immediately.
* **File-uploaded specs** — click **Update** to upload a new version.
* Switch from a file to a URL source using **Edit** in the breadcrumb actions menu.

Using the CLI, run the same command to update:

```bash
gitbook openapi publish --spec api-spec-name --organization organization_id <path-or-url>
```

You can also use the CLI's publish command against the same URL to check for updates. See [Automate spec updates with CI/CD](automate-spec-updates.md) to script this.

<details>

<summary>Why isn't my spec loading?</summary>

{% hint style="info" %}
This only applies to specs added by URL.
{% endhint %}

Your API must [allow cross-origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Access-Control-Allow-Origin) GET requests from your docs site. In your API's CORS settings, allow the exact origin where your docs are hosted (e.g. `https://your-site.gitbook.io` or `https://docs.example.com`). If your endpoint is public and doesn't use credentials, you can also return `Access-Control-Allow-Origin: *`.

</details>

## Insert API reference in your docs

GitBook can automatically generate pages for the endpoints in your spec — each containing OpenAPI operation blocks that let you and your visitors test and explore endpoints based on the spec.

{% hint style="success" %}
Endpoints generated from your spec keep updating whenever the spec updates.
{% endhint %}

### Automatically create pages from your spec

After [adding your spec](#add-a-specification), generate endpoint pages by inserting an **OpenAPI Reference** into a section's table of contents.

{% stepper %}
{% step %}
#### Generate pages from OpenAPI

Click **Add new...** at the bottom of the section's table of contents, then **OpenAPI Reference**.
{% endstep %}

{% step %}
#### Choose your spec and page structure

Pick your uploaded spec, then choose **One page per tag** or **One page per operation** — see [Structure your API reference](structure-your-api-reference.md#openapi-layouts) for the difference. You can also add a models page and a download link. Click **Insert**.
{% endstep %}

{% step %}
#### Manage your operations

GitBook generates pages based on your spec and its tags, grouping operation pages by tag if you chose **One page per operation**. See [Structure your API reference](structure-your-api-reference.md) to organize further.
{% endstep %}
{% endstepper %}

### Add an individual OpenAPI block

You can also add individual operations or schemas from your spec to any page.

{% stepper %}
{% step %}
#### Add a new OpenAPI block

Press **/** to open the block selector and search for OpenAPI.
{% endstep %}

{% step %}
#### Choose your spec

Pick your uploaded spec and click **Continue**.
{% endstep %}

{% step %}
#### Choose operations or schemas

Select what you want to insert, and click **Insert**.
{% endstep %}
{% endstepper %}
