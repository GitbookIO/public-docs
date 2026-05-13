---
icon: arrow-right-arrow-left
description: How Evolve events map to Segment track events and properties.
---

# Event mapping

Each Evolve event maps to a Segment track event with a curated subset of the event's data — flattened, dollar-denominated, and named to match Segment's spec.

## Identification

When an event has a customer attached, Evolve sends:

* `userId` — the customer's email if available, else the Evolve customer ID.
* `traits` — name, email, country, customer cohort, custom metadata fields.

For guest checkouts (no customer record), Evolve sends an `anonymousId` derived from the session ID instead.

## Payments events

| Evolve event | Segment event name | Key properties |
| --- | --- | --- |
| `charge.succeeded` | `Order Completed` | `revenue`, `currency`, `order_id`, `payment_method` |
| `charge.failed` | `Payment Failed` | `currency`, `decline_code`, `payment_method` |
| `charge.refunded` | `Order Refunded` | `revenue`, `currency`, `refund_amount` |
| `charge.disputed` | `Payment Disputed` | `revenue`, `currency`, `dispute_reason` |
| `payout.paid` | `Payout Sent` | `amount`, `currency`, `bank_last4` |

The `Order Completed` event matches the [Segment e-commerce spec](https://segment.com/docs/connections/spec/ecommerce/v2/), so it slots cleanly into Segment's pre-built downstream destinations (Mixpanel funnels, Customer.io campaigns, etc.).

## Customer events

| Evolve event | Segment event name | Key properties |
| --- | --- | --- |
| `customer.created` | `Customer Created` | `customer_id`, `email`, `signup_source` |
| `customer.updated` | `Customer Updated` | `customer_id`, `changed_fields` |

Customer events are also accompanied by an `identify` call to update the Segment user's traits.

## Subscription events

| Evolve event | Segment event name | Key properties |
| --- | --- | --- |
| `subscription.created` | `Subscription Started` | `plan`, `mrr`, `trial_end` |
| `subscription.invoice_paid` | `Subscription Renewed` | `plan`, `mrr` |
| `subscription.canceled` | `Subscription Canceled` | `plan`, `mrr_lost`, `cancel_reason` |
| `subscription.invoice_failed` | `Payment Failed` | `plan`, `mrr_at_risk`, `attempt_count` |

For SaaS-focused teams, the subscription mapping plus Mixpanel's pre-built MRR dashboards is the highest-leverage Segment integration.

## Identity events

| Evolve event | Segment event name | Key properties |
| --- | --- | --- |
| `verification_session.verified` | `Verification Completed` | `verification_type`, `customer_id` |
| `verification_session.failed` | `Verification Failed` | `verification_type`, `failure_reason` |

Useful for marketing tools that want to gate or personalize based on verification status.

## Connect events

| Evolve event | Segment event name | Key properties |
| --- | --- | --- |
| `account.verified` | `Seller Onboarded` | `account_id`, `country`, `business_type` |
| `account.restricted` | `Seller Restricted` | `account_id`, `restriction_reason` |
| `application_fee.created` | `Platform Revenue` | `amount`, `currency`, `seller_id`, `charge_id` |

The `Platform Revenue` event is the canonical "platform revenue per transaction" event — most marketplaces wire this directly to a daily revenue chart in their data warehouse.

## Custom metadata

Evolve resources carry a `metadata` object — arbitrary key/value pairs you attach. These flow into Segment as `metadata_*` properties on the relevant event. If your code adds `metadata: { campaign_id: "summer2026" }` to charges, the Segment event has `metadata_campaign_id: "summer2026"` for downstream attribution.

## Filtering events

If you only want a subset of events (e.g. only `charge.succeeded`), filter at the Evolve side under **Settings → Integrations → Segment → Source → Events**. This is more efficient than sending everything and filtering in Segment.

## Last reviewed

Last reviewed in early 2026. The mapping is stable; new events are added as new Evolve features ship — those go through change requests on the [docs repo](https://github.com/GitbookIO/evolve-demo).

## Related

* [Segment overview](README.md) — install and concepts.
* [Webhooks event catalog](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/event-catalog) — the Evolve-side events.
