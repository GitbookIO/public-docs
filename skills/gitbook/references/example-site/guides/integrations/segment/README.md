---
icon: circle-nodes
description: Stream Evolve events into Segment as a source, or apply Segment events to customer records.
---

# Segment

The Evolve Segment integration runs in two directions:

* **Source** — Evolve events flow into your Segment workspace, where they fan out to your downstream destinations (data warehouse, analytics, marketing tools).
* **Destination** — Segment events land on Evolve customer records as metadata, useful for personalizing receipts and surfacing context to support.

Most teams enable the source direction first (it's the higher-leverage one) and add the destination later if needed.

## Connect Evolve as a Segment source

{% stepper %}
{% step %}

### Get a Segment write key

In your Segment workspace, **Connections → Sources → Add Source → Evolve**. Segment generates a write key — copy it.

{% endstep %}

{% step %}

### Configure Evolve

In your Evolve dashboard, **Settings → Integrations → Segment → Source**. Paste the Segment write key and pick which events to stream:

* **Charges** (created, succeeded, failed, refunded, disputed)
* **Customers** (created, updated)
* **Subscriptions** (created, renewed, canceled)
* **Verifications** (created, verified, failed)
* **Connect** (account-related events)

The default selection covers the most common analytics use cases. Tighten it if you only need a subset.

{% endstep %}

{% step %}

### Verify in the Segment debugger

In Segment's source debugger, trigger a test charge in Evolve and watch the event arrive in Segment. From there, the data flows to whatever destinations you've configured (Snowflake, Mixpanel, Customer.io, etc.).

{% endstep %}
{% endstepper %}

## Source-direction event mapping

Each Evolve event becomes a Segment **track** event with a stable name and a curated payload. See [Event mapping](event-mapping.md) for the full table.

The general rule:

* The Evolve event ID is the Segment `messageId` — useful for deduplication.
* The Evolve customer email becomes the Segment `userId` (or `anonymousId` for guest checkouts).
* Amounts are in dollars (not cents), to match Segment conventions.

## Connect Segment as a destination

The destination direction lets Segment write to Evolve. Useful for:

* **Tagging** an Evolve customer with marketing-attribution data from Segment.
* **Triggering** an Evolve verification or refund from a Segment workflow.

In **Settings → Integrations → Segment → Destination**, configure which Segment events should affect Evolve records and how. Most teams use a small set of explicit mappings rather than firehosing everything.

{% hint style="warning" %}
**Be conservative with the destination direction.** Writes to Evolve from Segment are the most-likely place for data-quality issues — a misconfigured Segment source can pollute your Evolve customer records. Start with one event mapping, monitor the audit log, expand from there.
{% endhint %}

## Pricing

Segment integration is included on all plans. Per-event volume is metered against Segment's own pricing on their side; Evolve doesn't charge extra.

For the highest-volume mappings (every charge), Segment's per-MTU pricing can add up — watch your Segment usage as you scale.

## Last reviewed

Last reviewed in early 2026. Segment's event spec is occasionally updated; submit changes via the [docs repo](https://github.com/GitbookIO/evolve-demo).

## Related

* [Event mapping](event-mapping.md) — full Evolve→Segment event reference.
* [Webhooks](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/) — the underlying Evolve event source.
