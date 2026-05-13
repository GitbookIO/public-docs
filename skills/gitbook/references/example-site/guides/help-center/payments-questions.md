---
icon: credit-card
description: Charges, refunds, payouts, settlement — the most-asked Payments product questions.
---

# Payments questions

## Why was my customer's card declined?

The decline reason is on the charge timeline as `decline_code`. The most common ones:

| Code | What it means | What to do |
| --- | --- | --- |
| `insufficient_funds` | Not enough money on the card | Ask the customer to use another card |
| `expired_card` | Card past its expiry date | Collect updated details |
| `incorrect_cvc` / `incorrect_zip` | Wrong CVC or billing ZIP | Re-prompt for the failed field |
| `do_not_honor` | Generic decline; bank doesn't say why | Sometimes worth retrying after 24h |
| `lost_card` / `stolen_card` | Card flagged as compromised | Don't retry — fraud signal |

For a deeper dive, see the [community thread on decline-code triage](https://gitbookio.github.io/evolve-demo/connections/community/decline-codes-vs-card-decline-codes.html).

## When do my funds become available for payout?

A captured payment becomes available the moment it's captured. The available balance pays out on your plan's schedule:

| Plan | Schedule |
| --- | --- |
| Starter | T+3 business days |
| Growth | T+2 business days |
| Enterprise | T+1 (same-day available) |

The full mechanic — including reserves, holds, and multi-currency — is on the [Money movement and settlement](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/money-movement) page.

## Why is my payout pending?

Three common reasons:

1. **Risk hold** — Evolve flagged a payment for review. The hold lasts up to 14 days. The payment shows `held_for_review: true` on the timeline.
2. **Account reserve** — your account has a rolling reserve (typically 5% over 90 days for new accounts). The reserved amount stays pending until it ages out.
3. **Bank account issue** — your linked bank account became invalid. The dashboard shows a banner; update the account and the payout retries.

For risk holds specifically, contact support if it's been over 14 days.

## How do I issue a refund?

From the charge page in the dashboard, click **Refund**. You can refund the full amount or a partial amount; multiple partial refunds are fine up to the original total.

Via API, `POST /v2/refunds` with the charge ID. See the [Refunds tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/save-cards) for code samples.

## Why isn't my webhook firing?

Five things to check, in order:

1. **Endpoint subscribed to the right event?** Check **Developers → Webhooks → [endpoint] → Events**.
2. **Endpoint URL correct and reachable?** Use the dashboard's "Test endpoint" button.
3. **Endpoint returning 2xx?** Anything else triggers retries.
4. **Signature verification passing?** Most-cited cause: body parsed before verification.
5. **Live vs test mode mismatch?** Test-mode events only fire to test-mode endpoints, and vice versa.

The [Verifying signatures page](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/verifying-signatures) has the full debugging checklist. Watch the [YouTube webhook-debugging walkthrough](https://gitbookio.github.io/evolve-demo/connections/youtube/webhooks-deep-dive.html) for the live-troubleshooting flow.

## What's the difference between authorize and capture?

Authorize reserves the money on the customer's card without taking it. Capture finalizes the charge and the funds start moving toward your account.

By default, charges authorize and capture in one step. Pass `capture: false` to split them — useful for pre-orders, hospitality, marketplaces. You then have up to 7 days (30 on v3) to capture before the authorization expires.

Full mechanics on the [Payment lifecycle page](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/payment-lifecycle).

## How do I handle disputes?

Disputes show up in **Reconciliation → Disputes**. For each dispute:

1. Read the reason code — it tells you what evidence to gather.
2. Decide to fight or accept. For low-value disputes (under $50), accepting is often cheaper than the staff time to fight.
3. If fighting, submit evidence within 20 calendar days. The form pre-populates the most-relevant fields.

For systematic dispute reduction, the [chargeback-prevention tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/chargeback-prevention) is the highest-ROI thing you can do.

## Why is my approval rate low?

Three common causes:

* **Statement descriptor** — customers don't recognize charges and call their bank. Fix the descriptor in **Settings → Billing**.
* **Single acquirer** — you're missing the lift from Smart routing (Growth+). Check **Settings → Routing**.
* **Card mix** — international cards typically have lower approval rates. The Routing report breaks it down per BIN country.

For Growth and Enterprise, [Smart routing](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/accept-payments/smart-routing) typically lifts approval rates 1–3% with no code changes.

## Can I do partial captures?

Yes. After authorizing, capture an amount less than or equal to the original authorization. The remaining amount is released back to the customer.

```http
POST /v2/charges/{id}/capture
{
  "amount": 8000
}
```

Useful for hospitality (you authorize $200 at check-in, capture $147 at check-out) and marketplaces (you authorize the buyer's full amount, capture once you know what each seller actually delivered).

## What payment methods can I accept?

Cards (Visa, Mastercard, Amex, Discover, JCB, UnionPay, Diners) on every plan. ACH debit on Growth and Enterprise. Wire, SEPA, BACS Direct Debit, and 100+ international rails on Enterprise.

For the per-plan breakdown, see [Payment methods](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/payment-methods).

## How do I configure 3-D Secure?

In **Settings → Risk → 3-D Secure**, three presets:

* **Required only** — Evolve handles required cases (EU SCA), nothing else.
* **By rule** — your custom rules (e.g. amount > $500) on top of required cases.
* **Always** — every charge goes through 3DS.

For most teams, **By rule** with a high-value threshold is the right default. The [3-D Secure tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/3d-secure) walks through the setup.

## Where can I find more answers?

* [Community: Stripe migration gotchas](https://gitbookio.github.io/evolve-demo/connections/community/migrating-stripe-customers.html)
* [YouTube: Smart routing explained](https://gitbookio.github.io/evolve-demo/connections/youtube/smart-routing-explained.html)
* [Payments product space](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/)
* [Tutorials: Build common payment flows](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/#build-common-payment-flows)
