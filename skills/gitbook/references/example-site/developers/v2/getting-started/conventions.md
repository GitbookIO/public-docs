---
icon: list-ul
description: Errors, idempotency, pagination, rate limits — the things that look the same on every endpoint.
---

# Conventions

The Evolve API is plain HTTPS plus JSON. Every endpoint follows the same conventions for errors, retries, pagination, and rate limiting — get them right once and they apply everywhere.

## Request shape

* **Base URL:** <code class="expression">space.vars.api_live</code> (live), <code class="expression">space.vars.api_test</code> (test).
* **Auth:** `Authorization: Bearer sk_*` — see [Authentication](authentication.md).
* **Content type:** JSON for write operations. Form-encoded also accepted for convenience with `curl`.
* **Versioning:** `Evolve-Version: 2026-01-15` header. Defaults to your account version.

## Errors

Every error response has the same shape. Build your error handling around the `code`, never the human-readable message text.

```json
{
  "error": {
    "type": "card_error",
    "code": "card_declined",
    "decline_code": "insufficient_funds",
    "message": "Your card has insufficient funds.",
    "param": "source",
    "request_id": "req_8h2nF6m4Lp"
  }
}
```

### Common codes

| HTTP | `code` | When you'll see it | Retry safe? |
| --- | --- | --- | --- |
| `400` | `invalid_request` | Malformed body, missing required field, unknown parameter | No |
| `401` | `unauthorized` | Missing or invalid API key | No |
| `402` | `card_declined` | Issuer declined the charge | Sometimes — see `decline_code` |
| `409` | `idempotency_conflict` | Same `Idempotency-Key` reused with a different request body | No |
| `422` | `processing_error` | Network-level processing failure | Yes — retry with same key |
| `429` | `rate_limited` | You exceeded your account's request rate | Yes — back off |
| `500` | `api_error` | Evolve-side error | Yes — retry with same key |

Always log `request_id` from the response — it's what we'll need to investigate.

## Idempotency

Every write endpoint accepts an `Idempotency-Key` header. Send a unique key (we recommend UUID v4 or v7) per logical operation. If a request with the same key arrives within **24 hours**, Evolve returns the original response instead of creating a duplicate.

```http
POST /v2/charges
Authorization: Bearer sk_live_...
Idempotency-Key: 7b8f2c4a-91d2-4fe1-9b6a-2c8e5f1a9b0c
Content-Type: application/json

{ "amount": 4200, "currency": "usd", "source": "tok_visa" }
```

Rules:

1. Generate the key on the **server**, not the client. A double-clicked button shouldn't produce two distinct keys.
2. Use a fresh key per logical operation. Never reuse keys across operations.
3. Persist the key alongside the operation in your database **before** sending the request — that way a retry after a process crash uses the same key.

If you send the same key with a *different* body, you get `409 idempotency_conflict`. This is intentional — it catches bugs.

{% hint style="info" %}
The official [SDKs](sdks.md) auto-generate an idempotency key for every write call unless you provide one. You can always pass your own.
{% endhint %}

## Retry strategy

For retryable errors (5xx, 422, 429), use exponential backoff with full jitter, capped at 60 seconds. The official SDKs do this automatically; here's the pattern if you're rolling your own:

{% tabs %}
{% tab title="Node" %}
```js
async function withRetry(fn, max = 6) {
  for (let i = 0; i < max; i++) {
    try { return await fn(); }
    catch (err) {
      if (!isRetryable(err) || i === max - 1) throw err;
      const delay = Math.min(60_000, (2 ** i) * 1000 + Math.random() * 1000);
      await new Promise(r => setTimeout(r, delay));
    }
  }
}
```
{% endtab %}

{% tab title="Python" %}
```python
import random, time

def with_retry(fn, max_attempts=6):
    for attempt in range(max_attempts):
        try:
            return fn()
        except RetryableError:
            if attempt == max_attempts - 1:
                raise
            sleep = min(60, (2 ** attempt) + random.random())
            time.sleep(sleep)
```
{% endtab %}

{% tab title="Go" %}
```go
func withRetry(fn func() error, max int) error {
    for i := 0; i < max; i++ {
        if err := fn(); err == nil || !isRetryable(err) {
            return err
        }
        if i == max-1 {
            return fmt.Errorf("retries exhausted")
        }
        delay := time.Duration(math.Min(60, math.Pow(2, float64(i))+rand.Float64())) * time.Second
        time.Sleep(delay)
    }
    return nil
}
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
def with_retry(max = 6)
  attempts = 0
  begin
    yield
  rescue RetryableError
    attempts += 1
    raise if attempts >= max
    sleep [60, (2 ** attempts) + rand].min
    retry
  end
end
```
{% endtab %}
{% endtabs %}

## Pagination

List endpoints return cursor-paginated responses:

```json
{
  "data": [ { "id": "ch_..." }, { "id": "ch_..." }, ... ],
  "has_more": true,
  "next_cursor": "cur_8M2nF6m4LpQ"
}
```

* Default page size: **100**. Maximum: **1000**. Set with `?limit=`.
* Pass `next_cursor` from the previous response as `?cursor=` to fetch the next page.
* When `has_more` is `false`, you've reached the end.

The SDKs expose iterators that handle pagination automatically:

{% tabs %}
{% tab title="Node" %}
```js
for await (const charge of evolve.charges.list({ limit: 100 })) {
  console.log(charge.id);
}
```
{% endtab %}

{% tab title="Python" %}
```python
for charge in evolve.Charge.list(limit=100).auto_paging_iter():
    print(charge.id)
```
{% endtab %}

{% tab title="Go" %}
```go
iter := charge.List(&evolve.ChargeListParams{Limit: evolve.Int64(100)})
for iter.Next() {
    fmt.Println(iter.Charge().ID)
}
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
Evolve::Charge.list(limit: 100).auto_paging_each do |charge|
  puts charge.id
end
```
{% endtab %}
{% endtabs %}

## Rate limits

| Plan | Default rate |
| --- | --- |
| Starter | 100 req/s |
| Growth | <code class="expression">space.vars.default_rate_limit</code> req/s |
| Enterprise | Custom — typically 2,000+ req/s |

Every response includes:

```http
X-RateLimit-Limit: 500
X-RateLimit-Remaining: 487
X-RateLimit-Reset: 1714477260
```

If you hit the limit, you get `429 rate_limited` and a `Retry-After: <seconds>` header. The SDKs handle backoff automatically.

For sustained loads above your tier's default, contact your account team — we can raise it.

## Object IDs

Every Evolve object has a stable, prefixed ID:

| Prefix | Resource |
| --- | --- |
| `ch_` | Charge |
| `re_` | Refund |
| `dp_` | Dispute |
| `po_` | Payout |
| `cus_` | Customer |
| `vs_` | Verification session (Identity) |
| `acct_` | Connected account (Connect) |
| `tr_` | Transfer (Connect) |
| `cs_` | Checkout session |
| `req_` | Request (in error responses) |

Test-mode and live-mode IDs share the same prefix structure, but objects from one environment are never accessible from the other.

## Timestamps and money

* **Timestamps**: Unix seconds (UTC).
* **Amounts**: integer in the smallest currency unit (cents for USD, EUR; yen for JPY). Always pair with `currency`.

## What's next

* [SDKs](sdks.md) — pick a language and let the conventions handle themselves.
* [Webhooks](../webhooks/README.md) — same conventions apply on inbound events.
* [API references](../payments-api/README.md) — endpoint-by-endpoint detail.
