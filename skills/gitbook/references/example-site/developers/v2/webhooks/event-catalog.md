---
icon: list
description: Every event type Evolve emits, grouped by product.
---

# Event catalog

This page lists every event type Evolve emits, with a one-line description of when it fires. The full payload schema for each event matches the corresponding object in the API reference.

## Payments events

| Event | Fires when |
| --- | --- |
| `charge.pending` | A charge has been created and is being processed. Most teams skip this. |
| `charge.succeeded` | A charge captured successfully. The most common event. |
| `charge.failed` | A charge was declined or hit a processing error. `decline_code` on the data. |
| `charge.captured` | An authorized charge was captured. Only fires for two-step charges. |
| `charge.voided` | An authorization was released without being captured. |
| `charge.refunded` | A refund was successfully issued against the charge. |
| `charge.disputed` | A cardholder filed a chargeback against the charge. |
| `refund.created` | A refund was issued (mirrors `charge.refunded` from a refund-centric perspective). |
| `refund.succeeded` | A refund was accepted by the network and the funds are returning. |
| `refund.failed` | A refund failed (rare; usually means the cardholder's account is closed). |
| `dispute.created` | A new dispute was opened. |
| `dispute.evidence_required` | Reminder that the dispute response window is closing. |
| `dispute.won` | The network ruled in your favor. Funds are returned. |
| `dispute.lost` | The network ruled against you. Funds and fee remain with the cardholder. |
| `payout.created` | A payout was scheduled. |
| `payout.paid` | The payout completed and funds are in the bank. |
| `payout.failed` | The payout failed (closed account, frozen account). |

## Identity events

| Event | Fires when |
| --- | --- |
| `verification_session.created` | A new verification session was created. |
| `verification_session.processing` | The customer has submitted; Evolve is reviewing. |
| `verification_session.verified` | All required checks passed. |
| `verification_session.failed` | One or more required checks failed. Reason on the data. |
| `verification_session.manual_review` | An automated check was inconclusive; a human is reviewing. |
| `verification_session.expired` | The customer didn't complete within the window. |
| `bank_verification.verified` | A bank account was verified. |
| `bank_verification.failed` | A bank verification failed (Plaid auth, micro-deposits mismatch). |
| `screening.match_added` | Ongoing monitoring detected a new sanctions/PEP/adverse-media match. |

## Connect events

| Event | Fires when |
| --- | --- |
| `account.created` | A new connected account was created. |
| `account.verified` | A connected account completed onboarding and is enabled for charges and payouts. |
| `account.requirements_updated` | Evolve needs more information from this account (additional document, etc.). |
| `account.restricted` | The account has been restricted (typically risk-related). |
| `transfer.created` | A transfer to a connected account was initiated. |
| `transfer.paid` | A transfer settled in the connected account's balance. |
| `transfer.reversed` | A transfer was reversed (typically alongside a refund). |
| `application_fee.created` | An application fee was earned by the platform. |
| `application_fee.refunded` | An application fee was returned to the seller (e.g. as part of a refund). |

## Routing events

| Event | Fires when |
| --- | --- |
| `routing.acquirer_degraded` | An acquirer's success rate has dropped below the failover threshold. |
| `routing.acquirer_recovered` | A previously degraded acquirer is healthy again. |

These fire regardless of whether failover is enabled — useful even as monitoring signals. *Enterprise plans only.*

## Subscribing to events

Configure subscriptions per endpoint under **Developers → Webhooks → [endpoint] → Events**. You can subscribe to:

* **Specific events** (recommended) — list the events you handle.
* **An entire resource** (e.g. `charge.*`) — wildcards supported.
* **Everything** (`*`) — discouraged in production.

The dashboard shows the list of events delivered to each endpoint over the last 30 days, so you can quickly see what you're actually receiving.

## Payload version

Every event includes the `api_version` it was generated against:

```json
{ "id": "evt_...", "type": "charge.succeeded", "api_version": "2026-01-15", ... }
```

Webhook payload shapes change with API versions, just like API responses. The version on the event matches the version configured on the webhook endpoint (overridable per endpoint, in case you want to test a new API version on a specific webhook before rolling it out everywhere).

## Related

* [Verifying signatures](verifying-signatures.md) — verify before parsing.
* [Retries and replay](retries-and-replay.md) — handling delivery failures.
* [Conventions → Object IDs](../getting-started/conventions.md#object-ids) — what each prefix means.
