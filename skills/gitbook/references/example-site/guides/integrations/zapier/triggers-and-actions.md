---
icon: list-check
description: Every Evolve trigger and action available in Zapier, with sample payloads.
---

# Triggers and actions

The Zapier integration exposes a curated subset of Evolve's API — the events most useful for cross-tool automation, plus the actions most useful from external apps.

## Triggers

Triggers fire when something happens in Evolve. Each maps to a real-time webhook event under the hood, with Zapier polling on top.

### Payments triggers

| Trigger | Fires when | Common downstream action |
| --- | --- | --- |
| Charge succeeded | A charge captures successfully | Append to spreadsheet, update CRM |
| Charge failed | A charge fails (declined or processing error) | Alert in Slack, log in Linear |
| Refund created | A refund is issued | Email customer, update internal records |
| Dispute opened | A new dispute lands | Create Linear/Jira ticket, alert ops |
| Payout paid | A payout completes to your bank | Update accounting spreadsheet |

### Identity triggers

| Trigger | Fires when |
| --- | --- |
| Verification verified | An identity verification succeeds |
| Verification failed | An identity verification fails |
| Verification needs review | An automated check is inconclusive |
| Bank account verified | A Plaid or micro-deposit verification succeeds |

### Connect triggers

| Trigger | Fires when |
| --- | --- |
| Connected account verified | A new seller completes onboarding |
| Account requirements updated | A seller needs to provide more info |
| Application fee earned | Your platform earns a fee on a charge |
| Connect dispute opened | A dispute opens against a seller's charge |

### Customer triggers

| Trigger | Fires when |
| --- | --- |
| Customer created | A new customer record is created |
| Customer updated | An existing customer's details change |

## Actions

Actions let other apps create things in Evolve. Use a [restricted key](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/authentication#restricted-keys) scoped to just the actions your Zap performs.

### Customer actions

* **Create customer** — useful when a new lead in your CRM should also exist as an Evolve customer.
* **Update customer** — sync metadata changes from your CRM.
* **Tag customer** — add a metadata key/value pair.

### Charge actions

* **Create charge** — for very narrow use cases. Most teams shouldn't trigger charges from Zaps; the failure modes are hard to debug.
* **Refund charge** — useful for one-off refund flows where a support tool triggers the refund.

### Verification actions

* **Create verification session** — kick off an identity check from another app.

### Connect actions

* **Create connected account** — useful for integrating a non-Zapier-sourced seller list (e.g. a custom CRM with sellers you want to onboard).

## Sample trigger payload

When a charge-succeeded trigger fires, Zapier receives:

```json
{
  "id": "ch_3KsM12pL9qXa7",
  "amount_dollars": 42.00,
  "currency": "USD",
  "status": "succeeded",
  "customer_id": "cus_4n2P3qR5sT6uV",
  "customer_email": "jordan@acme.com",
  "description": "Order #1042",
  "created_at": "2026-04-30T14:22:01Z",
  "metadata": { "order_id": "1042" }
}
```

The fields are flattened (Zapier handles them better than nested JSON) and amounts are in dollars rather than cents. Use these directly in downstream actions.

## Custom fields

Each Evolve resource carries a `metadata` object — arbitrary key/value pairs your code attaches to the resource. These are surfaced in Zapier as individual fields you can map. If you tag every charge with `order_id`, that field appears as `metadata_order_id` in your Zap step.

## Limits and best practices

* **Test mode first.** Build with a `sk_test_*` key, swap to live when ready.
* **Use restricted keys.** Don't paste a full secret key into Zapier — scope it.
* **Watch task usage.** Trigger frequency × Zap count adds up fast on Zapier's per-task pricing. Budget accordingly.
* **For real-time, use webhooks.** Zapier polls every 1–15 minutes depending on plan. Sub-minute reactivity needs a direct webhook integration.

## Last reviewed

Last reviewed in early 2026. The trigger and action catalog is updated as new Evolve features ship; suggest additions via [change request on the docs repo](https://github.com/GitbookIO/evolve-demo).
