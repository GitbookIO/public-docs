# Add an OpenAPI specification

{% include "../../.gitbook/includes/openapi-availability-hint.md" %}

If you have an OpenAPI specification, you can add it directly to your organization. You can link your specification via the URL of a hosted OpenAPI document, or by uploading the OpenAPI file directly.

<figure><img src="../../.gitbook/assets/02_04_25_add_api_spec.svg" alt=""><figcaption></figcaption></figure>

### Add a specification

To add a specification, head to the OpenAPI panel in the sidebar. Here you’ll be able to upload a file, link via URL to your existing OpenAPI specification, or use our [CLI](https://docs.gitbook.com/developers/cli/quickstart) to publish your OpenAPI spec to GitBook.

You’ll need to give your specification a name, which will be its identifier if you add more than 1 specification to your organization.

<figure><img src="../../.gitbook/assets/03_04_25_api_spec_modal (1).svg" alt=""><figcaption><p>Add an OpenAPI specification modal.</p></figcaption></figure>

### Update your specification

From time to time you might need to update or modify your API specification.&#x20;

#### Updating your specification via URL

If you added your specification via URL, GitBook will automatically check for updates every 6 hours. If you need to update your specification faster than that, click the “Check for updates” button in the upper right corner of the OpenAPI section.

#### Updating your specification via file

To update your OpenAPI spec if you’ve added it as a file, click the “Update” button in the upper right corner of the OpenAPI section to update or replace the file.

#### Updating your specification via CLI

If you’ve used the [CLI](https://docs.gitbook.com/developers/cli/quickstart) to add an OpenAPI specification, you can update it by running the same command:

```bash
gitbook openapi publish --spec api-spec-name --organization organization_id <path-to-openapi-file>
```

