---
icon: arrows-left-right
description: Cut over from Stripe to Evolve with a parallel-run pattern and zero lost transactions.
---

# Migrate from Stripe

By the end of this tutorial you'll have a cutover plan from Stripe to Evolve that runs both processors in parallel during the migration window, validates payments are landing correctly on the Evolve side, and finally flips the switch with no customer-facing disruption. The migration takes 2–6 weeks of calendar time depending on your scale.

This is for teams with an existing production Stripe integration. If you're greenfield, just use the [accept-a-payment tutorial](accept-one-time-payment.md) directly.

{% hint style="info" %}
**Prerequisites.** A live Stripe account, a live Evolve account (work with your account team to set this up — you'll need an acquirer agreement and underwriting). Read access to your Stripe data export. Engineering bandwidth: about 3 weeks for a small team.
{% endhint %}

{% hint style="warning" %}
**Don't try a hard cutover.** Run both processors in parallel for at least a week. Surprises in production payment systems compound — paralleling gives you a rollback path that doesn't break customer experience.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Map your concepts

Most Stripe concepts map directly. Skim this table before doing anything else:

| Stripe | Evolve | Notes |
| --- | --- | --- |
| `Charge` | `Charge` | Same shape on v2. v3 renames to `Payment`. |
| `PaymentIntent` | `Charge` | Evolve doesn't have a separate PaymentIntent; auth-and-capture is unified. |
| `SetupIntent` | `setup_future_usage` flag on Checkout | Equivalent outcome, simpler API. |
| `Customer` | `Customer` | Same. |
| `PaymentMethod` | `PaymentMethod` | Same. |
| `Subscription` | `Subscription` | Same. Plans use a different schema; see step 4. |
| `Connect` | `Connect` | Account types unified — Evolve has one configurable account model instead of Express/Standard/Custom. |
| `Webhook` | `Webhook` | Same shape. Signing algorithm is HMAC-SHA256 (Stripe also uses this). |

{% endstep %}

{% step %}

### Spin up an Evolve account in test mode

Get test API keys, swap your SDK in a feature branch:

{% tabs %}
{% tab title="Node" %}
```diff
-import Stripe from "stripe";
-const stripe = new Stripe(process.env.STRIPE_SECRET_KEY);
+import Evolve from "@evolve/node";
+const evolve = new Evolve(process.env.EVOLVE_SECRET_KEY);
```
{% endtab %}

{% tab title="Python" %}
```diff
-import stripe
-stripe.api_key = os.environ["STRIPE_SECRET_KEY"]
+import evolve
+evolve.api_key = os.environ["EVOLVE_SECRET_KEY"]
```
{% endtab %}
{% endtabs %}

For most teams, this is a sed away. The method names and parameter shapes are largely identical.

{% endstep %}

{% step %}

### Run the test suite

Your existing test suite is gold here. If your tests use `stripe-mock` or VCR-recorded fixtures, you'll need to re-record against Evolve's test mode. Expect 90% of tests to pass with no changes; the 10% that fail are usually webhook-signature differences or specific error code names.

{% endstep %}

{% step %}

### Migrate plans and customers

Two things need to be ported from Stripe to Evolve before the parallel-run window:

* **Subscription plans** — recreate them in Evolve via API or dashboard. Use the same plan IDs (`plan_pro_monthly`, etc.) for clarity.
* **Customer records and saved cards** — Evolve provides a Stripe-import tool that pulls customer records and **network tokens** for saved cards. The actual card numbers don't transfer (PCI), but the tokens do — meaning your customers don't have to re-enter their cards.

The import tool is at **Settings → Migration → Import from Stripe**. It runs against test mode first; double-check the migrated data before going live.

{% endstep %}

{% step %}

### Run both processors in parallel

For your parallel-run window (we recommend 1–2 weeks):

* Route a small percentage of new charges to Evolve (5–10% to start).
* Compare the metrics: approval rate, time-to-auth, dispute rate.
* Existing subscriptions stay on Stripe until you're ready to cut over completely.

Use a feature flag to control the percentage. Easy to roll back if anything looks wrong.

{% endstep %}

{% step %}

### Cut over fully

When metrics on Evolve match or beat Stripe (usually within a week or two), flip the percentage to 100%. Then:

* Migrate the remaining active subscriptions in batch (Settings → Migration → Migrate subscriptions).
* Update your webhook endpoints to point only at the Evolve handler.
* Cancel your Stripe API keys to prevent accidental dual-charging.
* Keep the Stripe account open for 90 days for refunds and dispute responses on charges that were processed there.

{% endstep %}

{% step %}

### Reconcile the cutover month

In the month after cutover, your accounting will see two sets of settlement files — Stripe for the early-month charges and Evolve for the later-month charges. The [Stripe-to-Evolve reconciliation script](https://github.com/GitbookIO/evolve-demo) on GitHub combines them into a unified format your bookkeeper can import.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Webhook signatures aren't matching"</summary>

Stripe and Evolve both use HMAC-SHA256, but the **header format is different** — Stripe uses `Stripe-Signature: t=...,v1=...`, Evolve uses `Evolve-Signature: t=...,v1=...`. Same algorithm, different header name. Update your verifier to read the right header.

</details>

<details>

<summary>"Some saved cards didn't migrate"</summary>

Network tokens migrate; non-tokenized cards don't. About 5–10% of cards on a typical account are non-tokenized — usually older saved methods or smaller issuers. For those, the next charge attempt will fail with `payment_method_required` and your dunning flow should ask the customer to re-enter their card.

</details>

<details>

<summary>"My dispute rate jumped right after cutover"</summary>

Two non-obvious causes: (1) the statement descriptor changed from "ACME-CO" to "EVOLVE*ACME-CO" and customers don't recognize it — fix by setting your descriptor explicitly; (2) Stripe's dispute responses for old charges still flow through Stripe — make sure someone's still watching that queue for 90 days.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-cart-shopping" style="color:$primary;">:cart-shopping:</i></h3></td><td><strong>Accept a one-time payment</strong></td><td>Once you're on Evolve, the canonical checkout build.</td><td><a href="accept-one-time-payment.md">accept-one-time-payment.md</a></td></tr><tr><td><h3><i class="fa-arrows-rotate" style="color:$primary;">:arrows-rotate:</i></h3></td><td><strong>Subscription billing</strong></td><td>Migrating Stripe Subscriptions specifically.</td><td><a href="subscription-billing.md">subscription-billing.md</a></td></tr><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Prevent chargebacks</strong></td><td>The descriptor change is a known landmine.</td><td><a href="chargeback-prevention.md">chargeback-prevention.md</a></td></tr></tbody></table>
