---
description: Learn how to automate the update of your OpenAPI specification in GitBook.
---

# Integrating with CI/CD

GitBook can work with any CI/CD pipeline you already have for managing your OpenAPI specification. By using the GitBook CLI, you can automate updates to your API reference.

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

### Set a new source URL or trigger a refresh

If your OpenAPI specification is hosted at a URL, GitBook automatically checks for updates. To force an update (for example, after a release), run:

```bash
# Set your GitBook API token as an environment variable
export GITBOOK_TOKEN=<api-token>

gitbook openapi publish \
  --spec spec_name \
  --organization organization_id \
  https://api.example.com/openapi.yaml
```

### Update your spec with GitHub Actions

If you’re setting up a workflow to publish your OpenAPI spec, complete these steps in your repository:

1. In your repo, go to “Settings → Secrets and variables → Actions”.
2. Add a secret: `GITBOOK_TOKEN` (your GitBook API token).
3. Add variables (or hardcode them in the workflow):
   * `GITBOOK_SPEC_NAME` → your spec’s name in GitBook
   * `GITBOOK_ORGANIZATION_ID` → your GitBook organization ID
4. Save the workflow file as `.github/workflows/gitbook-openapi-publish.yml`.
5. Push changes to “main” (or run the workflow manually).

You can then use this action to update your spec:

{% code title=".github/workflows/gitbook-openapi-publish.yml" %}
```yaml
name: Publish OpenAPI to GitBook

on:
  push:
    branches: [ "main" ]
    paths:
      - "**/*.yaml"
      - "**/*.yml"
      - "**/*.json"
  workflow_dispatch:

jobs:
  publish:
    runs-on: ubuntu-latest
    env:
      # Required secret
      GITBOOK_TOKEN: ${{ secrets.GITBOOK_TOKEN }}
      # Prefer repo/org variables; fallback to inline strings if you like
      GITBOOK_SPEC_NAME: ${{ vars.GITBOOK_SPEC_NAME }}
      GITBOOK_ORGANIZATION_ID: ${{ vars.GITBOOK_ORGANIZATION_ID }}

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Publish spec file to GitBook
        run: |
          npx -y @gitbook/cli@latest openapi publish \
            --spec "$GITBOOK_SPEC_NAME" \
            --organization "$GITBOOK_ORGANIZATION_ID" \
            <path_to_spec>
```
{% endcode %}
