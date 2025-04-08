---
description: How to use GitBook’s OpenAPI method blocks to support a CI/CD workflow
---

# Integrating with CI/CD

{% include "../../.gitbook/includes/openapi-availability-hint.md" %}

GitBook can work with [Git Sync](../../getting-started/git-sync/) or any CI/CD pipeline you already have for managing your OpenAPI specification. By using the GitBook CLI, you can automate updates to your API reference.

### Upload a specification file

If your OpenAPI spec is generated during your CI process, you can upload it directly from your build environment:

```bash
# Set your GitBook API token as an environment variable
export GITBOOK_TOKEN=<api-token>

gitbook openapi publish \
  --spec spec_name \
  --organization organization_id \
  example.openapi.yaml
```

### Set a new souce URL or trigger a refresh

If your OpenAPI specification is hosted at a URL, GitBook automatically checks for updates. To force an update (for example, after a release), run:

```bash
# Set your GitBook API token as an environment variable
export GITBOOK_TOKEN=<api-token>

gitbook openapi publish \
  --spec spec_name \
  --organization organization_id \
  https://api.example.com/openapi.yaml
```
