---
description: Keep your published spec in sync from your CI pipeline.
---

# Automate spec updates with CI/CD

GitBook works with any CI/CD pipeline you already use to manage your OpenAPI spec — the GitBook CLI automates updates to your API reference.

### Upload a spec file

If your spec is generated during CI, upload it directly from your build environment:

```bash
# Set your GitBook API token as an environment variable
export GITBOOK_TOKEN=<api-token>

gitbook openapi publish \
  --spec spec_name \
  --organization organization_id \
  example.openapi.yaml
```

### Set a new source URL or trigger a refresh

If your spec is hosted at a URL, GitBook checks for updates automatically. To force an update — after a release, for example — run:

```bash
# Set your GitBook API token as an environment variable
export GITBOOK_TOKEN=<api-token>

gitbook openapi publish \
  --spec spec_name \
  --organization organization_id \
  https://api.example.com/openapi.yaml
```

### Update your spec with GitHub Actions

{% stepper %}
{% step %}
#### Add your token as a secret

In your repo, go to **Settings → Secrets and variables → Actions** and add a `GITBOOK_TOKEN` secret (your GitBook API token).
{% endstep %}

{% step %}
#### Add variables

Add `GITBOOK_SPEC_NAME` (your spec's name in GitBook) and `GITBOOK_ORGANIZATION_ID` — as repo/org variables, or hardcoded in the workflow.
{% endstep %}

{% step %}
#### Save the workflow

Save the workflow file as `.github/workflows/gitbook-openapi-publish.yml`.
{% endstep %}

{% step %}
#### Push or run manually

Push to `main` (or trigger the workflow manually).
{% endstep %}
{% endstepper %}

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
