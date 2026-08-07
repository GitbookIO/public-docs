# Using OpenAPI proxy

GitBook can proxy **Test It** requests so they work even when your API server doesn't support CORS.

### Why this exists

Browsers block cross-origin requests unless the API server opts in with CORS headers. Without CORS configured, **Test It** requests fail in the browser. The proxy routes those requests server-side through GitBook, bypassing that restriction.

### Enable the proxy for your whole spec

Add `x-enable-proxy: true` at the root of your OpenAPI spec.

<pre class="language-yaml"><code class="lang-yaml">openapi: '3.0.3'
<strong>x-enable-proxy: true
</strong>info:
  title: Example API
  version: '1.0.0'
servers:
  - url: https://api.example.com
</code></pre>

### Enable or disable for a specific operation

Add `x-enable-proxy` on an operation.

<pre class="language-yaml"><code class="lang-yaml">openapi: '3.0.3'
info:
  title: Example API
  version: '1.0.0'
servers:
  - url: https://api.example.com
paths:
  /reports:
    get:
      summary: List reports
<strong>      x-enable-proxy: true
</strong>      responses:
        '200':
          description: OK
    post:
      summary: Create report
<strong>      x-enable-proxy: false
</strong>      responses:
        '201':
          description: Created
</code></pre>

{% hint style="info" %}
Operation-level `x-enable-proxy` takes precedence over the root-level value.
{% endhint %}

### What the proxy supports

GitBook forwards all `HTTP` methods (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`), headers, cookies, and request bodies.

### Security

The proxy only forwards requests to the URLs listed in your spec’s `servers` array. It can’t be used to reach arbitrary URLs.&#x20;

{% hint style="info" %}
Make sure your `servers` array includes every base URL you want to test against. If a URL isn't listed, **Test It** requests to that host will bypass the proxy.
{% endhint %}
