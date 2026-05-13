---
icon: flask
description: Two separate environments — what changes between them, and how to flip safely.
---

# Test mode and live mode

{% include "../.gitbook/includes/environments.md" %}

## What's different in live mode

* **Real money moves.** Successful charges debit the cardholder and are scheduled for payout to your bank account. See [Money movement](../concepts/money-movement.md) for payout timing.
* **Real cards only.** Test card numbers (`4242 4242 4242 4242` and friends) are rejected with `card_declined` in live mode.
* **Webhooks fire to your live endpoint.** Make sure your verification logic is using the live signing secret (it's a separate value, prefixed `whsec_live_`).
* **Settlement files are generated.** A new CSV lands in your reconciliation feed every day at 06:00 UTC. See [Settlement files](../reconciliation/settlement-files.md).

## Flipping from test to live

There is no merge or migration step — test and live are fully separate. To go live:

1. Complete the dashboard onboarding (business verification, bank account, statement descriptor).
2. Generate a live key under **Developers → API keys**.
3. Swap `sk_test_*` for `sk_live_*` in your environment configuration.
4. Update webhook endpoints to point at your production URL and use the live signing secret.

{% hint style="warning" %}
**Don't rely on switching keys at runtime.** Hard-code the environment in your config, not by inspecting the key prefix. Code that branches on key shape tends to leak test behavior into production.
{% endhint %}

## Cutting over from a test integration

If you've been integrating against test mode, the fastest path to confidence in live is:

<details>

<summary>Run a single small live charge end to end</summary>

Use a real card you control, charge $1.00, confirm it appears in your dashboard, and refund it. This proves your live key, webhook signature, and settlement view are wired up correctly — without putting any customer-facing flow at risk.

</details>

<details>

<summary>Verify your webhook handler against live signatures</summary>

Test-mode webhooks are signed with a different secret than live-mode webhooks. A common pre-launch bug is leaving the test signing secret in your handler. Replay a live webhook from the dashboard's **Webhook log** and confirm your handler accepts it.

</details>

<details>

<summary>Reconcile your first settlement</summary>

After your first live payout, download the settlement CSV from the dashboard and walk through it row by row. See [Settlement files](../reconciliation/settlement-files.md) for the schema and a sample reconciliation script.

</details>
