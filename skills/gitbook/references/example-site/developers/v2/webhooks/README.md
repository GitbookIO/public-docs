---
description: >-
  How Evolve sends events to your endpoints, how to verify them, and how to
  handle failures.
icon: bolt
---

# Overview

Webhooks let Evolve push events to your servers as they happen — a charge succeeded, a verification finished, a dispute opened. Most production integrations rely on webhooks rather than polling, because polling at the granularity needed for payments hits the rate limits fast.

## What an event looks like

```json
{
  "id": "evt_3KsM12pL9qXa7",
  "object": "event",
  "type": "charge.succeeded",
  "created": 1714477200,
  "api_version": "2026-01-15",
  "data": {
    "object": {
      "id": "ch_3KsM12pL9qXa7",
      "object": "charge",
      "amount": 4200,
      "currency": "usd",
      "status": "succeeded"
    }
  },
  "request": {
    "id": "req_8h2nF6m4Lp",
    "idempotency_key": "7b8f2c4a-91d2-4fe1-9b6a-2c8e5f1a9b0c"
  }
}
```

Every event has the same outer shape — `id`, `type`, `data.object` — regardless of which resource it's about.

## Setting up an endpoint

{% stepper %}
{% step %}
#### Add the endpoint

In the dashboard, **Developers → Webhooks → Add endpoint**. Enter your URL and pick the events to subscribe to. For local testing, expose `localhost` with [ngrok](https://ngrok.com) or similar.
{% endstep %}

{% step %}
#### Save the signing secret

Each endpoint has its own signing secret (prefix `whsec_`). Copy it and add it to your environment as `EVOLVE_WEBHOOK_SECRET`.
{% endstep %}

{% step %}
#### Verify the signature

In your handler, verify the `Evolve-Signature` header before parsing the body. See [Verifying signatures](verifying-signatures.md) for code in every supported language.
{% endstep %}

{% step %}
#### Respond with 2xx

Evolve treats any `2xx` as a successful delivery. Anything else is retried — see [Retries and replay](retries-and-replay.md).
{% endstep %}
{% endstepper %}

## What's in the rest of the section

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h4></td><td><strong>Verifying signatures</strong></td><td>Per-language signature verification.</td><td><a href="verifying-signatures.md">verifying-signatures.md</a></td></tr><tr><td><h4><i class="fa-list" style="color:$primary;">:list:</i></h4></td><td><strong>Event catalog</strong></td><td>Every event type Evolve emits, with payload examples.</td><td><a href="event-catalog.md">event-catalog.md</a></td></tr><tr><td><h4><i class="fa-rotate" style="color:$primary;">:rotate:</i></h4></td><td><strong>Retries and replay</strong></td><td>Retry behavior and how to replay missed events.</td><td><a href="retries-and-replay.md">retries-and-replay.md</a></td></tr></tbody></table>

## Best practices

A few patterns that consistently save trouble:

<details>

<summary>Be idempotent on your side too</summary>

Webhooks can be delivered more than once — at-least-once delivery, not exactly-once. Use the event `id` as a dedup key in your database; if you've seen the id before, ack and skip the work.

</details>

<details>

<summary>Respond fast, defer the work</summary>

Acknowledge the webhook (return 2xx) within a few seconds. If the actual processing is slow, push the event onto a queue and process it asynchronously. Slow handlers cause Evolve to retry, which causes duplicate processing.

</details>

<details>

<summary>Don't trust the event payload more than necessary</summary>

For destructive operations, refetch the canonical object from the API after receiving the event. Webhook payloads are point-in-time — by the time you process the event, the object may have changed.

</details>

<details>

<summary>Subscribe narrowly</summary>

Subscribe only to event types you actually handle. Subscribing to `*` is convenient but means more retries and more noise during incidents.

</details>
