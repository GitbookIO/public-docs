---
description: How to use GitBook’s OpenAPI method blocks to support a CI/CD workflow
---

# Support for CI/CD with API blocks

Our OpenAPI block supports CI/CD, which means your API documentation can auto-update when a new version is released. The method of updating depends on whether you upload your API spec via URL or as a file.

### URL upload

If you upload your API spec via a URL, your docs will auto-update existing API references when they change in the spec. However, when the OpenAPI file is changed, the cache will not be updated immediately. It may take a few hours for the published docs to reflect the latest version, but it can take up to a day.

For example, [this](https://github.com/GitbookIO/integrations/blob/main/docs/gitbook-api/reference/collections.md) is the method we use in our developer docs.

### API file upload

If you upload your API spec as a file, you will have to re-upload the new version of the file in order to update your documentation. However, GitBook will detect existing blocks on the same page and auto-update them when you upload the file.

An alternative solution is to use [Git Sync](../../getting-started/git-sync/) with an OpenAPI spec file in the synced repository. Store the OpenAPI spec in a repository as a JSON/YAML file and reference it in Markdown:

{% code overflow="wrap" %}
```markdown
{% raw %}
{% swagger src="./openapi.json" path="/collections/{collectionId}" method="get" expanded="true" %} 
[openapi.json](./openapi.json) 
{% endswagger %}
{% endraw %}
```
{% endcode %}

Every time this file changes and a commit is pushed to GitHub, your docs will also update. This ensures that your documentation is always up to date with your latest API changes.

### Configure third-party tools & frameworks

In instances where you want to display custom information (such as `x-codeSamples`), you can configure your tool of choice to export the needed OpenAPI spec to the formats above.&#x20;

In cases where your OpenAPI spec is being referenced via URL, the data will be pulled from the hosted spec every time the page loads, meaning updates will be automatic.&#x20;

If you are referencing the OpenAPI spec via file upload, you must first [configure Git Sync](../../getting-started/git-sync/) in order to allow GitBook to reference local files in your repository. Once [configured](support-for-ci-cd-with-api-blocks.md#api-file-upload), any updates to the file referenced in your OpenAPI blocks or pages will update when changes are made to this file.

