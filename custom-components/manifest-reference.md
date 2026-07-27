---
description: Every field in gitbook-manifest.yaml, the file that configures an integration.
---

# Manifest reference

Integrations are defined through a file called `gitbook-manifest.yaml`, automatically created by the CLI when you run `gitbook new`.

Fields marked <mark style="color:red;">\*</mark> are required.

### Name<mark style="color:red;">\*</mark>

The name of your integration. Must be unique across all GitBook integrations.

```yaml
name: unique-integration-name
```

### Title<mark style="color:red;">\*</mark>

The title of your integration.

```yaml
title: My Integration
```

### Description<mark style="color:red;">\*</mark>

A short description for your integration.

```yaml
description: A short, descriptive overview of my integration.
```

### Summary

A summary for your integration, displayed on the installation page. Supports Markdown, limited to 2048 characters.

```yaml
summary: |
    # Overview
    The GitBook Slack integration brings the power of GitBook to your Slack workspace. Your teams have instant access to your GitBook knowledge base, without leaving Slack.
    # Configure
    You can install the integration on a single space by clicking the integrations button in the sub-navigation panel. If you prefer to install the Slack integration on all spaces, you can enable this through organization settings. To configure the integration you will have to authorize the connection between Slack and GitBook. You can also select the default channel to post messages to.
```

### Organization<mark style="color:red;">\*</mark>

The id or subdomain of the organization that owns this integration. See [Integration concepts](integration-concepts.md).

```yaml
organization: <org_id>
```

### Visibility<mark style="color:red;">\*</mark>

| Visibility | Description |
|---|---|
| `private` | Default for new integrations. Only members of the organization defined in the manifest can install it. |
| `unlisted` | Members of any organization can install it, but only via its shared install link. |
| `public` | Members of any organization can install it. Required to [submit your integration to the marketplace](publishing-and-submitting-integrations.md). |

```yaml
visibility: private
```

### Scopes<mark style="color:red;">\*</mark>

The permissions your integration requests.

```yaml
scopes:
    # Spaces
    - space:content:read       # Read space content
    - space:content:write      # Write space content
    - space:metadata:read      # Read metadata related to a space
    - space:metadata:write     # Write metadata related to a space
    - space:git:sync           # Manage Git Sync within a space
    # Sites
    - site:metadata:read       # Read metadata related to a site
    - site:views:read          # Read analytics related to a site
    - site:script:inject       # Internal scope - see note below
    - site:script:cookies      # Internal scope - see note below
    - site:visitor:auth        # Enable workflows related to authenticated access
    - site:visitor:claims      # Expose visitor claims to webframes
    - site:adaptive:read       # Read claims available from Adaptive Content
    - site:adaptive:write      # Write claims available to Adaptive Content
    # OpenAPI
    - openapi:read             # Read information from a site's OpenAPI spec
    - openapi:write            # Write information to a site's OpenAPI spec
    # Conversations
    - conversations:ingest
```

{% hint style="danger" %}
You may see the scope `site:script:inject` used throughout GitBook-owned integrations — this scope is for internal GitBook use only. Building integrations that inject JavaScript into a site or space isn't possible at this time.
{% endhint %}

### Script

The main script to execute for your integration, containing the `createIntegration()` call. See the [Integration runtime reference](integration-runtime-reference.md).

```yaml
script: ./src/index.ts
```

### Blocks

Component block(s), referenced by id, to render in the quick insert menu (⌘ + /). See `createComponent()` in the [Integration runtime reference](integration-runtime-reference.md).

```yaml
blocks:
  - id: example-block
    title: Example Block
    description: An example block for a GitBook integration
```

### Categories

A list of categories your integration falls into.

```yaml
categories:
    - analytics
    - collaboration
    - content
    - marketing
    - authenticated-access
    - other
```

### Icon

A locally referenced icon for your integration. The asset must be located alongside the code for your integration.

```yaml
icon: ./assets/icon.png
```

### Preview images

A list of locally referenced assets to display on the installation page for your integration (recommended: 1600×800px, 2:1 aspect ratio).

```yaml
previewImages:
    - ./assets/integration-preview-image.png
```

### External links

A list of URLs to display on the installation page. Each link requires a `label` and a `url`.

```yaml
externalLinks:
    - label: Documentation
      url: https://example.com/docs
    - label: Homepage
      url: https://example.com/
```

### Configurations

The `configurations` key lets you specify the steps a user goes through when configuring your integration, exposed at runtime through `environment`.

Set defaults under `configurations.account`, and site-specific configuration under `configurations.site`. Both accept `properties` — named keys describing each configuration step — and an optional `required` list to enforce specific properties.

Properties can be one of the following types:

**`string`** — collects user input. Add `enum` to offer a fixed dropdown list, or `completion_url` to populate the dropdown from an endpoint you control.

```yaml
string_property:
    type: string
    title: String Property
    description: A short description
    default: A default value

    # Optional: a fixed list of options
    enum:
      - item 1
      - item 2

    # Optional: fetch a list of entries from an endpoint
    completion_url: /completion-endpoint
```

**`number`**

```yaml
number_property:
    type: number
    title: Number Property
    description: A short description
    default: 1
```

**`boolean`**

```yaml
boolean_property:
    type: boolean
    title: Boolean Property
    description: A short description
    default: true
```

**`button`** — used to kick off an OAuth connection with a provider. See `createOAuthHandler()` in the [Integration runtime reference](integration-runtime-reference.md).

```yaml
button_property:
    type: button
    title: Button Property
    description: A short description
    button_text: Authorize
    callback_url: /callback-url
```

**Full example:**

```yaml
configurations:
    account:
        properties:
            oauth_credentials:
                type: button
                title: Connection
                description: Authorization between my app and GitBook.
                button_text: Authorize
                callback_url: /oauth
            default_channel:
                type: string
                title: Default Channel
                description: Select a channel to post messages to, when none is configured for a specific space.
                completion_url: /channels
        required:
            - oauth_credentials
            - default_channel
    site:
        properties:
            channel:
                type: string
                title: Channel
                description: Select a channel to post messages related to this space.
                completion_url: /channels
            notify_content_update:
                type: boolean
                title: Notify Content Update
                description: Post a notification message every time the content of the space is updated.
                default: true
            notify_visibility_update:
                type: boolean
                title: Notify Visibility Update
                description: Post a notification message every time the visibility of the space is updated.
                default: true
```

### Secrets

A list of secrets or environment variables your integration needs at runtime. Environment variables aren't loaded into the manifest by default — use a package like [`dotenv-cli`](https://www.npmjs.com/package/dotenv-cli) to load them from an `.env` file when using the CLI.

```yaml
secrets:
    CLIENT_ID: ${{ env.CLIENT_ID }}
```

### Installation & configuration flow

When an integration is installed for the first time, an `installation_setup` event fires. You can tell the configuration is incomplete by checking `environment.installation.status != 'active'`.

This event fires again every time the user edits a configuration property, and the status becomes `active` once the configuration passes schema validation.
