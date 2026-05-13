---
icon: flask
description: Two separate environments — what changes between them, and how to flip safely.
---

# Test mode and live mode

{% include "../.gitbook/includes/environments.md" %}

## What's different in live mode

* **Real documents are reviewed.** Verifications hit the actual document database, the selfie liveness model, and (where enabled) the watchlist screening engine. Test mode uses fixture results.
* **PII is encrypted and stored.** Test mode discards documents and selfies on session completion. Live mode encrypts and retains them per your [data retention](../compliance/data-retention.md) policy.
* **Per-verification fees apply.** Test mode is free. See [fees](#fees) below.
* **Webhooks fire to your live endpoint.** Make sure your verification handler is using the live signing secret (`whsec_live_*`).

## Flipping from test to live

There is no merge or migration step — test and live are fully separate.

1. Complete the dashboard onboarding (business verification, banking, retention policy review).
2. Generate a live key under **Developers → API keys**.
3. Swap `sk_test_*` for `sk_live_*` in your environment configuration.
4. Update webhook endpoints to point at your production URL and use the live signing secret.

{% hint style="warning" %}
**Live mode triggers regulatory obligations.** Once you're processing real verifications, you're handling PII in scope of GDPR, CCPA, and (where applicable) regional KYC rules. Make sure your privacy notice and retention policy reflect what Evolve does on your behalf — see [Regional requirements](../compliance/regional-requirements.md).
{% endhint %}

## Fees

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="info" icon="layer-group" %}
**You're on Starter** — identity verifications cost **$1.50 each**. Bank verification, KYB, and watchlist screening aren't available on Starter.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "growth" %}

{% hint style="info" icon="layer-group" %}
**You're on Growth** — identity verifications cost **$1.20 each**. Bank verification (Plaid) is **$2.50**, micro-deposits are **$0.80**.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="success" icon="layer-group" %}
**You're on Enterprise** — pricing is per your contract. The standard published rates below show defaults; your effective rates are visible in **Settings → Billing**.
{% endhint %}

{% endif %}

| Verification | Starter | Growth | Enterprise |
| --- | --- | --- | --- |
| Identity (document + selfie) | $1.50 | $1.20 | Custom |
| Bank account (Plaid instant) | — | $2.50 | Custom |
| Bank account (micro-deposits) | — | $0.80 | Custom |
| Business verification (KYB) | — | — | $5.00 / Custom |
| Watchlist screening (initial) | — | — | $0.50 |
| Watchlist screening (re-screen) | — | — | $0.10 |

Verification fees appear on your settlement file as a separate line type `verification_fee`, alongside payment processing fees from [Payments](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reconciliation/settlement-files).

## Cutting over from test

Before flipping the production switch, the team checks we recommend:

<details>

<summary>Run one real verification end to end</summary>

Use a colleague with consent and a real ID. Confirm the result lands in the dashboard, the webhook fires, and the data appears in your downstream system.

</details>

<details>

<summary>Verify your privacy notice covers Identity</summary>

GDPR and CCPA require you to disclose that an automated decisioning service processes ID documents on your behalf. The standard wording is in [Regional requirements → GDPR](../compliance/regional-requirements.md#gdpr).

</details>

<details>

<summary>Set your retention window</summary>

The default is 30 days post-verification. If you need longer (compliance) or shorter (data minimization), change it in **Settings → Identity → Retention** before going live. See [Data retention](../compliance/data-retention.md).

</details>
