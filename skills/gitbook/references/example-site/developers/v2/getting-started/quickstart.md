---
description: >-
  Make your first API call to Evolve in five minutes — in your language of
  choice.
icon: rocket
---

# Quickstart

This walkthrough takes a single test charge end to end. By the time you're done, you'll have proven your environment is set up, your auth works, and a payment landed in your dashboard.

You don't need a production account or any prior payments experience to follow along.

## Prerequisites

* A test API key from [https://dashboard.test.evolve.com](https://gitbook.com) → **Developers → API keys**. It starts with `sk_test_`.
* Your language's package manager set up (`npm`, `pip`, `go get`, or `gem`).

{% hint style="warning" %}
**Treat secret keys like passwords.** Never commit them to source control or paste them into client-side code. Use environment variables.
{% endhint %}

## 1. Install the SDK

{% tabs %}
{% tab title="Node" %}
```bash
npm install @evolve/node
```
{% endtab %}

{% tab title="Python" %}
```bash
pip install evolve
```
{% endtab %}

{% tab title="Go" %}
```bash
go get github.com/evolve-pay/evolve-go
```
{% endtab %}

{% tab title="Ruby" %}
```bash
gem install evolve
```
{% endtab %}

{% tab title="cURL" %}
```bash
# No install needed.
```
{% endtab %}
{% endtabs %}

## 2. Make your first charge

{% tabs %}
{% tab title="Node" %}
```js
import Evolve from "@evolve/node";

const evolve = new Evolve(process.env.EVOLVE_SECRET_KEY);

const charge = await evolve.charges.create({
  amount: 4200,
  currency: "usd",
  source: "tok_visa",
  description: "First test payment",
}, {
  idempotencyKey: crypto.randomUUID(),
});

console.log(charge.id, charge.status);
```
{% endtab %}

{% tab title="Python" %}
```python
import os, uuid
import evolve

evolve.api_key = os.environ["EVOLVE_SECRET_KEY"]

charge = evolve.Charge.create(
    amount=4200,
    currency="usd",
    source="tok_visa",
    description="First test payment",
    idempotency_key=str(uuid.uuid4()),
)

print(charge.id, charge.status)
```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
    "fmt"
    "os"

    "github.com/evolve-pay/evolve-go"
    "github.com/evolve-pay/evolve-go/charge"
    "github.com/google/uuid"
)

func main() {
    evolve.Key = os.Getenv("EVOLVE_SECRET_KEY")

    params := &evolve.ChargeParams{
        Amount:      evolve.Int64(4200),
        Currency:    evolve.String("usd"),
        Source:      evolve.String("tok_visa"),
        Description: evolve.String("First test payment"),
    }
    params.SetIdempotencyKey(uuid.NewString())

    ch, err := charge.New(params)
    if err != nil {
        panic(err)
    }
    fmt.Println(ch.ID, ch.Status)
}
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "evolve"
require "securerandom"

Evolve.api_key = ENV["EVOLVE_SECRET_KEY"]

charge = Evolve::Charge.create(
  {
    amount: 4200,
    currency: "usd",
    source: "tok_visa",
    description: "First test payment",
  },
  idempotency_key: SecureRandom.uuid
)

puts "#{charge.id} #{charge.status}"
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://api.test.evolve.com/v2/charges \
  -H "Authorization: Bearer $EVOLVE_SECRET_KEY" \
  -H "Idempotency-Key: $(uuidgen)" \
  -d amount=4200 \
  -d currency=usd \
  -d source=tok_visa \
  -d description="First test payment"
```
{% endtab %}
{% endtabs %}

A successful response looks like:

```json
{
  "id": "ch_3KsM12pL9qXa7",
  "object": "charge",
  "amount": 4200,
  "currency": "usd",
  "status": "succeeded",
  "created": 1714477200,
  "payment_method": { "type": "card", "brand": "visa", "last4": "4242" }
}
```

## 3. Verify it landed

Open [https://dashboard.test.evolve.com/payments](https://gitbook.com). Your charge should be at the top of the list. Click it to see the request that created it, the timeline, and the webhook deliveries.

## 4. Receive a webhook

Most production integrations react to webhook events rather than polling.

{% stepper %}
{% step %}
#### Add an endpoint

In the dashboard, **Developers → Webhooks → Add endpoint**. For local testing, use a tool like [ngrok](https://ngrok.com) to expose `localhost`. Subscribe to `charge.succeeded` and `charge.failed` to start.
{% endstep %}

{% step %}
#### Verify the signature

Every event Evolve sends is HMAC-signed. Verify the signature before acting on it — see [Verifying signatures](../webhooks/verifying-signatures.md).
{% endstep %}

{% step %}
#### Replay events

Webhooks fail; that's normal. The dashboard's webhook log shows every delivery and lets you replay any event with one click. See [Retries and replay](../webhooks/retries-and-replay.md).
{% endstep %}
{% endstepper %}

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-key" style="color:$primary;">:key:</i></h4></td><td><strong>Auth deep dive</strong></td><td>Restricted keys, signature verification, rotation.</td><td><a href="authentication.md">authentication.md</a></td></tr><tr><td><h4><i class="fa-list-ul" style="color:$primary;">:list-ul:</i></h4></td><td><strong>Conventions</strong></td><td>Errors, idempotency, pagination, rate limits.</td><td><a href="conventions.md">conventions.md</a></td></tr><tr><td><h4><i class="fa-credit-card" style="color:$primary;">:credit-card:</i></h4></td><td><strong>Payments API</strong></td><td>Full reference for charges, refunds, payouts.</td><td><a href="../payments-api/">payments-api</a></td></tr></tbody></table>
