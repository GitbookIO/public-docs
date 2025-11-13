# Configuring the “Test it” button

You can configure the "Test It" button and accompanying window in GitBook using several OpenAPI extensions. These extensions can help improve and configure the testing suite for users.

### Hiding the “Test it” button

You can hide the “Test it” button from your endpoints by adding the `x-hideTryItPanel` to an endpoint, or at the root of your OpenAPI spec.

{% code title="openapi.yaml" %}
```yaml
openapi: '3.0'
info: ...
tags: [...]
paths:
  /example:
    get:
      summary: Example summary
      description: Example description
      operationId: examplePath
      responses: [...]
      parameters: [...]
      x-hideTryItPanel: true
```
{% endcode %}

### Enable authentication in the testing window

The request runner can only present and apply auth if your spec declares it. Define schemes under `components.securitySchemes`, then attach them either globally via `security` (applies to all operations) or per-operation (overrides global).

#### Declare your auth scheme

Below are common patterns. Use straight quotes in YAML.

{% tabs %}
{% tab title="HTTP Bearer (e.g., JWT)" %}
```yaml
openapi: '3.0.3'
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
{% endtab %}

{% tab title="API Key in header" %}
```yaml
openapi: '3.0.3'
components:
  securitySchemes:
    apiKeyAuth:
      type: apiKey
      in: header
      name: X-API-Key
```
{% endtab %}

{% tab title="OAuth2 (authorizationCode)" %}
```yaml
openapi: '3.0.3'
components:
  securitySchemes:
    oauth2:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: 'https://auth.example.com/oauth/authorize'
          tokenUrl: 'https://auth.example.com/oauth/token'
          scopes:
            read:items: 'Read items'
            write:items: 'Write items'
```
{% endtab %}
{% endtabs %}

#### Apply schemes globally or per operation

{% tabs %}
{% tab title="Gloabl" %}
```yaml
openapi: '3.0.3'
security:
  - bearerAuth: []
paths: ...
```
{% endtab %}

{% tab title="Per-operation" %}
```yaml
paths:
  /reports:
    get:
      summary: Get reports
      security:
        - apiKeyAuth: []
      responses:
        '200':
          description: OK
```
{% endtab %}
{% endtabs %}

### Control the endpoint URL with `servers`

The request runner targets the URL(s) you define in the `servers` array. Declare one or more servers; you can also parameterize them with variables.

{% tabs %}
{% tab title="Single server" %}
```yaml
openapi: '3.0.3'
servers:
  - url: https://instance.api.region.example.cloud
```
{% endtab %}

{% tab title="Multiple servers" %}
```yaml
servers:
  - url: https://api.example.com
    description: Production
  - url: https://staging-api.example.com
    description: Staging
```
{% endtab %}

{% tab title="Server variables" %}
```yaml
servers:
  - url: https://{instance}.api.{region}.example.cloud
    variables:
      instance:
        default: acme
        description: Your tenant or instance slug
      region:
        default: eu
        enum:
          - eu
          - us
          - ap
        description: Regional deployment
```
{% endtab %}

{% tab title="Per-operation servers" %}
<pre class="language-yaml"><code class="lang-yaml"><strong>paths:
</strong>  /reports:
    get:
      summary: Get reports
      servers:
        - url: https://reports.api.example.com
      responses:
        '200':
          description: OK
</code></pre>
{% endtab %}
{% endtabs %}
