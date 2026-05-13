---
description: >-
  How Evolve retries failed deliveries, and how to replay events your handler
  missed.
icon: rotate
---

# Retries and replay

Webhook delivery isn't perfect. Your server will go down, your handler will throw, networks will glitch. Evolve treats this as the default case rather than the exception — every delivery is retried until it succeeds or we give up after **3 days**.

## The retry schedule

If your endpoint returns anything other than `2xx`, or doesn't respond within 30 seconds, Evolve retries:

| Attempt    | After       |
| ---------- | ----------- |
| 1          | Immediately |
| 2          | 1 minute    |
| 3          | 5 minutes   |
| 4          | 15 minutes  |
| 5          | 1 hour      |
| 6          | 4 hours     |
| 7          | 16 hours    |
| 8          | 1 day       |
| 9          | 2 days      |
| 10 (final) | 3 days      |

After the final attempt, the event is marked **failed** and stays in the dashboard's webhook log for 90 days. You can replay it manually any time within that window.

## What counts as a successful delivery

Anything in the `2xx` range. Redirects (`3xx`) are followed up to 5 hops. Anything else (including timeouts) triggers retry.

We strongly recommend returning `2xx` quickly (under a few seconds) and processing the event asynchronously. If your handler does the actual work synchronously and takes 25 seconds, you're one slow database query away from a `504` and a duplicate-delivery storm during retries.

## Replaying events from the dashboard

The webhook log shows every delivery attempt for every endpoint:

{% stepper %}
{% step %}
#### Find the event

**Developers → Webhooks → \[endpoint] → Events**. Filter by event type, status, or time range. Each row shows the delivery attempts and the response code Evolve got.
{% endstep %}

{% step %}
#### Replay it

Click an event and hit **Replay**. Evolve sends a fresh delivery to the same endpoint, with a current timestamp on the signature so it passes a strict freshness check.
{% endstep %}

{% step %}
#### Watch the new attempt

The dashboard shows the new delivery attempt and your response within seconds.
{% endstep %}
{% endstepper %}

You can also replay in bulk — select multiple events and click **Replay all** to re-deliver in chronological order. This is the right tool after fixing a handler bug that caused a backlog of failed deliveries.

## Replaying programmatically

For automated recovery (e.g. a deploy script that replays events from the deployment window), use the API:

```http
POST /v2/webhook_endpoints/{endpoint_id}/events/{event_id}/replay
Authorization: Bearer sk_live_...
```

Returns the new delivery attempt's `id`. Replays are rate-limited per endpoint to 100/minute.

## Why deliveries fail (and what to do)

<details>

<summary>Connection refused / timeout</summary>

Your endpoint is down. Investigate why. Evolve will keep retrying for 3 days, so a brief outage doesn't lose events — but if you discover a long outage, replay manually to be sure.

</details>

<details>

<summary>500 Internal Server Error</summary>

Your handler threw. Check your logs for the underlying error. Common causes: parsing the body as JSON before verifying the signature (which fails on the raw bytes), missing environment variables, downstream service errors.

</details>

<details>

<summary>400 Bad Request (with "Invalid signature" message)</summary>

Signature verification failed. See [Verifying signatures → Common pitfalls](verifying-signatures.md#common-pitfalls).

</details>

<details>

<summary>Slow responses (mostly 504 from gateway)</summary>

Your handler is too slow. Acknowledge fast and queue the actual work. Even if your processing typically completes in 5 seconds, the p99 will eventually exceed 30 and trigger retries.

</details>

## Idempotency on your side

Webhook delivery is **at-least-once**, not exactly-once. The same event can be delivered multiple times if:

* Evolve retried after your endpoint timed out, but the original request actually completed on your side.
* You replayed an event manually.
* A network glitch caused us to think delivery failed when it didn't.

Use the event `id` (`evt_...`) as a dedup key in your database. If you've seen the id before, ack and skip the work. The id is stable across retries and replays.

```sql
CREATE TABLE processed_webhook_events (
  event_id TEXT PRIMARY KEY,
  processed_at TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

## Pause an endpoint

Sometimes you need to stop receiving events temporarily — during a long outage, a deploy with breaking changes, an investigation. **Pause** an endpoint in the dashboard and Evolve stops trying to deliver to it. Events queue up; when you **Resume**, Evolve delivers them in order, with the original timestamps preserved on the signature payload.

There's a 7-day cap on paused-endpoint queues. After 7 days, queued events are dropped (but still visible for manual replay in the webhook log).

## Related

* [Verifying signatures](verifying-signatures.md) — verify before processing.
* [Event catalog](event-catalog.md) — every event type.
* [Conventions → Idempotency](../getting-started/conventions.md#idempotency) — for outbound requests, the same idea.
