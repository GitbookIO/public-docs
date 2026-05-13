---
description: API keys, scopes, and how Evolve authenticates every request.
icon: key
---

# Authentication

Evolve uses bearer-token authentication. Every request includes an `Authorization` header with a secret key:

```http
Authorization: Bearer sk_live_4gT8m...
```

Keys are issued and rotated from the \[dashboard]\(<code class="expression">space.vars.dashboard_live</code>) under **Developers → API keys**. We recommend rotating production keys every 90 days.

## Key types

| Key              | Prefix                  | Use it for                                        | Safe to expose? |
| ---------------- | ----------------------- | ------------------------------------------------- | --------------- |
| Live secret      | `sk_live_`              | Server-side production calls                      | No              |
| Live publishable | `pk_live_`              | Client-side payment session creation              | Yes             |
| Test secret      | `sk_test_`              | Server-side test calls                            | No              |
| Test publishable | `pk_test_`              | Client-side test integrations                     | Yes             |
| Restricted       | `rk_live_` / `rk_test_` | Scoped server keys (read-only, refund-only, etc.) | No              |

## Setting the key in each SDK

{% tabs %}
{% tab title="Node" %}
```js
import Evolve from "@evolve/node";

// Reads from EVOLVE_SECRET_KEY by default.
const evolve = new Evolve();

// Or pass explicitly:
const evolve = new Evolve(process.env.EVOLVE_SECRET_KEY);
```
{% endtab %}

{% tab title="Python" %}
```python
import os
import evolve

evolve.api_key = os.environ["EVOLVE_SECRET_KEY"]
```
{% endtab %}

{% tab title="Go" %}
```go
import (
    "os"
    "github.com/evolve-pay/evolve-go"
)

evolve.Key = os.Getenv("EVOLVE_SECRET_KEY")
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "evolve"

Evolve.api_key = ENV["EVOLVE_SECRET_KEY"]
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://api.evolve.com/v2/charges \
  -H "Authorization: Bearer $EVOLVE_SECRET_KEY"
```
{% endtab %}
{% endtabs %}

## Restricted keys

If you need to grant a third party (BI tool, internal microservice, on-call dashboard) access to a subset of your account, create a **restricted key** under **Developers → API keys → New restricted key**. You pick the resources and permissions; the key can never be widened after creation.

Common restricted-key shapes:

| Shape             | Use case                                   |
| ----------------- | ------------------------------------------ |
| Read-only         | BI exports, monitoring dashboards          |
| Refunds only      | Customer-support tooling                   |
| Connect read-only | Per-platform reporting on Connect activity |
| Webhooks only     | Dedicated event-handler service            |

## API versioning

Evolve uses **dated versioning** via the `Evolve-Version` header. The default version for your account is set when you create your first API key, and you can override it per request:

```http
Evolve-Version: 2026-01-15
```

Major shape changes (resources renamed, fields removed) ship as **variants** rather than new dates — see [Payments API → Overview](../payments-api/) for `v1`, `v2`, and `v3`.

If you don't send the header, your account-default version is used. We recommend pinning explicitly in production code.

## Verifying webhook signatures

Webhooks and partner callbacks are signed with HMAC-SHA256 using a separate **signing secret** (prefix `whsec_`). Always verify the signature before acting on the payload — a missing or invalid signature means the request did not come from Evolve.

See [Verifying signatures](../webhooks/verifying-signatures.md) for the per-language code.

{% hint style="danger" %}
**Never disable signature verification "temporarily" in production.** This is the single most common source of payment-platform incidents we see. If you can't verify, fail closed.
{% endhint %}

## Rotating keys

You can rotate any secret key without downtime:

{% stepper %}
{% step %}
#### Generate a new key

In the dashboard, click **Roll** next to the key. The new key becomes active immediately. The old key keeps working for 24 hours so you can deploy at your own pace.
{% endstep %}

{% step %}
#### Deploy the new key

Update your environment configuration and redeploy. Verify by making a test call against the live API.
{% endstep %}

{% step %}
#### Revoke the old key

Once you've confirmed the new key is in place everywhere, click **Revoke**. Any further requests with the old key will fail with `401 unauthorized`.
{% endstep %}
{% endstepper %}

## Detection and incident response

If a key is exposed (committed to a public repo, leaked in a log), revoke it immediately from the dashboard. Evolve also runs leaked-key detection across public GitHub and a few other surfaces — if we find your key in a public commit, we'll auto-revoke it and email you within minutes.

## Related

* [Quickstart](quickstart.md) — minimal setup walkthrough.
* [Conventions](conventions.md) — what each request and response look like.
* [Webhooks → Verifying signatures](../webhooks/verifying-signatures.md) — for inbound auth.
