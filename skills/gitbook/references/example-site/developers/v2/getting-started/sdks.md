---
description: >-
  Official SDKs for Node, Python, Go, and Ruby — plus community-maintained
  libraries.
icon: cubes
---

# SDKs

Evolve maintains four official SDKs. They cover every endpoint, ship in idiomatic style for the language, and follow the same release cadence as the API itself.

## Official SDKs

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-node-js" style="color:$primary;">:node-js:</i></h4></td><td><strong>Node</strong></td><td><code>@evolve/node</code></td><td></td></tr><tr><td><h4><i class="fa-python" style="color:$primary;">:python:</i></h4></td><td><strong>Python</strong></td><td><code>evolve</code> on PyPI</td><td></td></tr><tr><td><h4><i class="fa-golang" style="color:$primary;">:golang:</i></h4></td><td><strong>Go</strong></td><td><code>github.com/evolve-pay/evolve-go</code></td><td></td></tr><tr><td><h4><i class="fa-gem" style="color:$primary;">:gem:</i></h4></td><td><strong>Ruby</strong></td><td><code>evolve</code> on RubyGems</td><td></td></tr></tbody></table>

## Install

{% tabs %}
{% tab title="Node" %}
```bash
npm install @evolve/node
# or
yarn add @evolve/node
# or
pnpm add @evolve/node
```

Requires Node 18+. TypeScript types ship in the package.
{% endtab %}

{% tab title="Python" %}
```bash
pip install evolve
# or
poetry add evolve
```

Requires Python 3.9+. Synchronous and async clients both available — use `evolve.AsyncClient` for the async path.
{% endtab %}

{% tab title="Go" %}
```bash
go get github.com/evolve-pay/evolve-go
```

Requires Go 1.21+. Strict module boundaries — every resource is a separate package (`charge`, `refund`, `payout`, etc.).
{% endtab %}

{% tab title="Ruby" %}
```ruby
# Gemfile
gem "evolve", "~> 2.0"
```

Requires Ruby 3.0+. Thread-safe; uses Net::HTTP with persistent connections.
{% endtab %}
{% endtabs %}

## What each SDK gives you

* **Full API coverage.** Every endpoint in [Payments](../payments-api/), [Identity](../identity-api/), and [Connect](../connect-api/) has a typed method.
* **Automatic retries** with exponential backoff for transient errors (5xx, 429, network errors).
* **Idempotency** — the SDK auto-generates an idempotency key for write operations unless you provide one.
* **Webhook signature verification** — `Evolve.Webhook.constructEvent` (or equivalent) handles HMAC verification.
* **Telemetry** — anonymized SDK version and request shape, used to find regressions. Disable with `EVOLVE_TELEMETRY=off`.

## Versioning

The SDK tracks the API closely. Every API version has at least one matching SDK release.

| API version            | Node SDK | Python SDK | Go SDK   | Ruby SDK |
| ---------------------- | -------- | ---------- | -------- | -------- |
| `2026-01-15` (default) | `2.x`    | `2.x`      | `v2.x.x` | `2.x`    |
| `2025-07-01`           | `1.x`    | `1.x`      | `v1.x.x` | `1.x`    |

You can pin the API version in the SDK explicitly:

{% tabs %}
{% tab title="Node" %}
```js
const evolve = new Evolve(process.env.EVOLVE_SECRET_KEY, {
  apiVersion: "2026-01-15",
});
```
{% endtab %}

{% tab title="Python" %}
```python
evolve.api_key = os.environ["EVOLVE_SECRET_KEY"]
evolve.api_version = "2026-01-15"
```
{% endtab %}

{% tab title="Go" %}
```go
evolve.Key = os.Getenv("EVOLVE_SECRET_KEY")
evolve.APIVersion = "2026-01-15"
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
Evolve.api_key = ENV["EVOLVE_SECRET_KEY"]
Evolve.api_version = "2026-01-15"
```
{% endtab %}
{% endtabs %}

## Source and contributions

All four SDKs are open source under the MIT license:

* [evolve-pay/evolve-node](https://github.com/GitbookIO/evolve-demo)
* [evolve-pay/evolve-python](https://github.com/GitbookIO/evolve-demo)
* [evolve-pay/evolve-go](https://github.com/GitbookIO/evolve-demo)
* [evolve-pay/evolve-ruby](https://github.com/GitbookIO/evolve-demo)

PRs welcome. For bigger changes, open an issue first to align on direction.

## Community libraries

Maintained by external contributors, not officially supported by Evolve:

* **PHP** — [`evolve-community/evolve-php`](https://github.com/evolve-community/evolve-php)
* **Java** — [`evolve-community/evolve-java`](https://github.com/evolve-community/evolve-java)
* **.NET** — [`evolve-community/Evolve.NET`](https://github.com/evolve-community/Evolve.NET)
* **Rust** — [`evolve-community/evolve-rs`](https://github.com/evolve-community/evolve-rs)

For anything not in this list, the API is plain HTTPS + JSON — `curl` and your language's HTTP client will work fine. See [Conventions](conventions.md).

## Mobile SDKs

Mobile-specific SDKs (iOS, Android, React Native) are part of the [Payments → Embedded Elements](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/accept-payments/take-a-payment) story rather than the server SDK story. They're shipped from a separate repo:

* [`evolve-pay/evolve-ios`](https://github.com/GitbookIO/evolve-demo) — Swift, supports iOS 15+.
* [`evolve-pay/evolve-android`](https://github.com/GitbookIO/evolve-demo) — Kotlin, supports Android 8+.
* [`evolve-pay/evolve-react-native`](https://github.com/GitbookIO/evolve-demo) — TypeScript wrapper around both.

These handle PCI-scope-reducing card collection on the client. Don't use a server SDK from a mobile app — it'd require shipping a secret key.
