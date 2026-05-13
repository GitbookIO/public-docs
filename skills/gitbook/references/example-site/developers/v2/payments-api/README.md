---
description: Charges, refunds, payouts, and balance — the stable v2 surface.
icon: credit-card
---

# Overview

The Payments API is the workhorse of Evolve — taking money, refunding money, and moving it to your bank. The operation reference is auto-generated and listed below this page in the sidebar.

{% hint style="success" icon="circle-check" %}
**You're viewing v2 — the stable default.** Use the variant dropdown in the top bar to switch to **v1** (deprecated) or **v3** (preview).
{% endhint %}

## Base URL

```
https://api.evolve.com/v2
```

The default version date for v2 is <code class="expression">space.vars.api_version</code>. Pin it in your code with the `Evolve-Version` header — see [Authentication → API versioning](../getting-started/authentication.md#api-versioning).

## Resources

* **Charges** — create, capture, void, retrieve, list.
* **Refunds** — full and partial refunds against a charge.
* **Payouts** — list and retrieve. Schedule is configured in the dashboard.
* **Balance** — available, pending, and reserved balances per currency.

## What changed since v1

If you're migrating from v1, the most consequential changes:

* `POST /sources/charge` is gone. Use `POST /charges` directly — the source-type is inferred from the token.
* Error `code` values are stable across languages and won't change within v2.
* Webhook signatures use HMAC-SHA256 (v1 used HMAC-SHA1). See [Verifying signatures](../webhooks/verifying-signatures.md).
* Idempotency keys are required on every write endpoint, not optional.

The full migration walkthrough lives at [Guides → v1 → v2 migration](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/migrate-payments-v1-to-v2). v1 sunset is **2026-12-31**.

## What's coming in v3

v3 is in preview today. Use the variant dropdown to flip over and explore. Highlights:

* `Charge` is renamed to `Payment`.
* `capture: true|false` becomes `capture_method: automatic|manual`.
* Authorization window extended from 7 to 30 days.
* Multi-currency capture — authorize in USD, capture in EUR at wholesale FX.

When v3 graduates to stable, we'll publish a migration tool. For now, treat v3 as exploratory.

## Conceptual background

For the product-side concepts behind these endpoints — what a charge actually does, how settlement timing works, when 3-D Secure applies — see the [Payments product space](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/). It's the right complement to the API reference.
