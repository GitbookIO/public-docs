---
icon: flask
description: Two separate environments — what changes between them, and how to flip safely.
---

# Test mode and live mode

{% include "../.gitbook/includes/environments.md" %}

## What's different in live mode for Connect

Connect has all the live-mode considerations of [Payments live mode](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/quickstart/test-and-live-mode), plus several specific to platforms:

* **Real seller onboarding.** Live connected accounts go through real [identity](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/identity-verification) and [bank](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/bank-account) verification. Onboarding can take from minutes (US individuals) to days (international businesses).
* **Real KYC obligations.** Live mode triggers your platform's KYC obligations under the regimes you operate in. See [Identity / Regional requirements](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/compliance/regional-requirements).
* **Real payouts.** Live payouts move real money to seller bank accounts on the schedule you've configured.
* **Real disputes.** Disputes opened against your sellers' charges hit the platform's dispute queue and can affect both your platform's risk profile and the seller's account standing.

## Flipping from test to live

There is no merge or migration step — test connected accounts don't carry over. Sellers go through onboarding once in test (for your integration testing) and again in live (for real).

{% stepper %}
{% step %}

### Complete platform onboarding

Your own platform account needs to be live-mode-eligible — business verification, banking, and a signed platform agreement. Most platforms do this once and then forget.

{% endstep %}

{% step %}

### Generate live keys

Under **Developers → API keys**, generate live secret and publishable keys. Restricted keys for downstream services (BI tools, internal services) work the same as in [Payments](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/quickstart/test-and-live-mode).

{% endstep %}

{% step %}

### Update onboarding URLs

Hosted onboarding URLs are environment-specific. The links your platform sends to sellers must point at the live environment, not test. If you build a custom onboarding flow, this is the URL prefix to swap.

{% endstep %}

{% step %}

### Update webhook endpoints

Live-mode webhooks are signed with a separate signing secret. Update your webhook handler to use the live secret before flipping the key.

{% endstep %}
{% endstepper %}

{% hint style="warning" %}
**Don't run test and live onboarding in parallel during cutover.** Sellers who go through test onboarding and assume they're live will be confused when they don't get paid. Make the cutover sharp — turn off test-mode self-serve onboarding before announcing live mode is open.
{% endhint %}

## Volume limits

{% if visitor.claims.unsigned.plan === "growth" %}

{% hint style="info" icon="layer-group" %}
**You're on Growth** — up to **100 connected accounts** in live mode. Test mode is unlimited. To go beyond 100, [upgrade to Enterprise](mailto:support@evolve.com).
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="success" icon="layer-group" %}
**You're on Enterprise** — unlimited connected accounts in both environments.
{% endhint %}

{% endif %}

## Cutting over checklist

Before flipping production:

<details>

<summary>Run a single live payment through one real seller</summary>

Use a colleague or your own business as the live seller. Onboard them, take a $1 payment with your real card, watch the transfer land, refund it. This proves your live keys, webhook signatures, application fees, and payout configuration are wired up correctly.

</details>

<details>

<summary>Verify the seller-facing emails point to live URLs</summary>

The onboarding email, payout notification email, and dispute alerts all contain URLs. Test-mode emails point at `dashboard.test.evolve.com`, live-mode emails point at `dashboard.evolve.com`. Make sure your email templates use the live values.

</details>

<details>

<summary>Confirm your dispute-handling plan</summary>

In live mode, disputes are real. Decide who on your team handles them, who has access to the dispute queue, and what your policy is for whether the platform absorbs disputes or passes them through to the seller. See [Refunds and disputes](../platform-setup/refunds-and-disputes.md).

</details>
