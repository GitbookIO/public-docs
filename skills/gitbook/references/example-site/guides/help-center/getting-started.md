---
icon: flag
description: First setup, going live, integration help, and the steps every new account walks through.
---

# Getting started

## I just signed up. What do I do first?

Three steps in order:

1. **Verify your business** — answer the prompts in **Settings → Onboarding** to verify your business identity and link a bank account. Until this is done, you're stuck in test mode.
2. **Run a test charge** — follow the [Quickstart](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/quickstart/accept-your-first-payment). Five minutes, no integration required.
3. **Get your live keys** — once business verification passes, **Developers → API keys** has live `sk_live_` and `pk_live_` keys ready.

After that, the [Tutorials](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/) cover the most common integration patterns.

## How long does business verification take?

For US-based businesses with standard structures (LLC, S-corp, sole proprietor), most verifications complete in **1–2 business days**. For more complex structures (multi-layer ownership, international entities, regulated verticals), it can take up to 5 business days.

You can use test mode immediately while verification is pending. Live charges are blocked until verification completes.

## What documents will I need?

Standard business verification needs:

* Legal business name and registration country.
* EIN (US) or local equivalent.
* Business address.
* Beneficial owners (for any entity beyond a sole proprietor).
* A bank account for payouts (Plaid-instant or routing/account number).

For regulated verticals (financial services, gambling, age-restricted goods, money transmission), additional documentation is required. The dashboard prompts for whatever's needed; if you're unsure, talk to your account team before submitting.

## Can I use Evolve in countries that aren't in the dropdown?

The country list in the dashboard reflects where Evolve is currently licensed. If your business is in a country not listed, contact sales — coverage expands regularly and you may be able to onboard via a special-process route.

For sellers in unsupported countries on a Connect platform, the path is usually different — Evolve can onboard them via the platform's account if certain regulatory conditions are met.

## How do I get my first API key?

**Developers → API keys** in the dashboard. You'll see two pairs by default — `sk_test_*` / `pk_test_*` for test mode and (after business verification) `sk_live_*` / `pk_live_*` for live mode.

Copy the secret keys to a password manager or environment-variable store. Don't commit them to source control.

For the full setup walkthrough, see the [Developers Quickstart](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/quickstart).

## What's the fastest way to take my first payment?

The [Accept your first payment](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/quickstart/accept-your-first-payment) walkthrough takes about five minutes via the dashboard, with no code required. Create a payment link, share it, complete the test checkout — done.

For an integration-first start, the [Tutorials → Accept a one-time payment](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/accept-one-time-payment) covers building Checkout into your own site.

## How do I switch from test mode to live mode?

There's no migration step — test and live are fully separate. To go live:

1. Confirm business verification has completed.
2. Generate a live key in **Developers → API keys**.
3. Replace `sk_test_*` with `sk_live_*` in your environment configuration.
4. Update webhook endpoints to point at your production URL with the live signing secret.

Test-mode data doesn't carry over. Most teams run a single $1 live charge as a smoke test before pointing real customers at the live key. See the [Test mode and live mode page](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/quickstart/test-and-live-mode) for the full cutover checklist.

## Which SDK should I use?

Evolve maintains four official SDKs: Node, Python, Go, Ruby. They're feature-equivalent — pick whatever your team uses. For mobile apps, see the iOS / Android / React Native libraries instead, which are built around card collection.

The full list is on the [Developers SDKs page](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/sdks).

## I'm migrating from another provider. Where do I start?

For Stripe specifically, the [Migrate from Stripe tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/migrate-from-stripe) covers the field mapping, the parallel-run pattern, and the cutover checklist. For other providers, the same patterns apply — most concepts (charges, refunds, customers, subscriptions) map cleanly.

For business-side migration of customer data and saved cards, contact your account team. Several import tools are available depending on the source provider.

## Can someone help me design my integration?

Yes — Enterprise customers get a solutions engineer assigned at signup. Growth customers can request integration support via **Settings → Get help → Integration support**; we'll respond within 1 business day.

For most well-trodden integration patterns, the [Tutorials](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/) cover the build end to end, including common pitfalls.

## Where can I find more answers?

* [Community forum](https://gitbookio.github.io/evolve-demo/connections/community/)
* [YouTube: Set up Connect in 10 minutes](https://gitbookio.github.io/evolve-demo/connections/youtube/set-up-connect-in-10-minutes.html)
* [Tutorials](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/) — end-to-end builds for common workflows.
* [Developers Quickstart](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/quickstart) — five-minute API integration.
