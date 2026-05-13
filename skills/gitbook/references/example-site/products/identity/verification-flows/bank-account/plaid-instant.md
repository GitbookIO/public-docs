---
icon: bolt
description: One-tap, real-time bank account verification through Plaid.
---

# Plaid instant

Plaid instant is the fastest way to verify a customer's bank account. The customer signs into their bank from your verification flow; Evolve receives the verified account and routing numbers in real time. The whole experience takes 30–60 seconds.

It's the right default for any product where customer experience matters — checkout abandonment is real and 1–2 days of waiting for micro-deposits is enough to lose a sign-up.

## What the customer experiences

{% stepper %}
{% step %}

### "Connect your bank"

A button or link in your flow opens the Evolve hosted verification page. The customer picks their bank from a list of Plaid-supported institutions (or searches by name).

{% endstep %}

{% step %}

### Sign in to the bank

The customer signs in with their online banking credentials, on a Plaid-hosted page. Their credentials never touch Evolve or your servers — Plaid handles the bank session.

{% endstep %}

{% step %}

### Pick an account

Most customers have multiple accounts at the same bank. They pick the one they want to use — checking vs savings, primary vs secondary.

{% endstep %}

{% step %}

### Done

The flow returns to your site. The verified account appears on the customer's record in **Identity → Customers** with a verified badge. From there it can be used immediately for ACH debits, payouts, or whatever your product needs.

{% endstep %}
{% endstepper %}

## Coverage

Plaid covers ~12,000 US financial institutions, including all major retail banks and most credit unions. For a customer's specific bank, the [Plaid coverage checker](https://plaid.com/institutions) shows whether instant verification is supported.

For non-US accounts, Plaid's coverage is much narrower — currently only major banks in Canada, the UK, France, Spain, the Netherlands, and Ireland. Customers outside these countries fall back to micro-deposits or open banking flows specific to their region.

## What you get back

Once verified, you have on the customer record:

| Field | Example |
| --- | --- |
| Account number (masked) | `••••6789` |
| Routing number | `021000021` |
| Account type | `checking` / `savings` |
| Bank name | `Chase` |
| Account holder name (verified) | `Jordan Patel` |
| Available balance (optional) | `$4,182.50` |
| Currency | `USD` |

The masked account number is what you should display to the customer in your UI. The full account and routing numbers are accessible via the API for ACH debit operations, but never displayed in the dashboard or on receipts.

## Risk and fraud signals

In addition to the account data, Plaid returns a set of risk signals you can opt into:

* **Account age** — when the account was opened. Very new accounts (< 30 days) are higher fraud risk.
* **Recent NSF events** — non-sufficient-funds bounces in the last 90 days. Indicates the customer might not have funds for your debit.
* **Large recent deposits** — unusual incoming activity, sometimes a fraud signal.
* **Multiple Plaid links recently** — the same account being linked to many products in a short window is a classic synthetic-identity pattern.

These come back as a `risk_score` on the verification record, plus the individual signals. You decide how to act on them — block, manual review, or ignore.

## Costs and limits

| | |
| --- | --- |
| **Cost per verification** | $2.50 |
| **Speed** | 30–60 seconds |
| **Re-verification** | Free for 30 days after initial |
| **Coverage** | ~12,000 US banks + select international |

There's no monthly minimum or platform fee — you only pay per verification.

## When Plaid fails

Sometimes the customer can't get through Plaid — their bank is undergoing maintenance, their credentials don't work, they'd rather not share online banking access. The default Evolve flow handles this gracefully:

* The Plaid sheet shows a "Use another method" link at the bottom of the bank list.
* Clicking it switches the customer into the [micro-deposits](micro-deposits.md) flow seamlessly.
* The verification record links the two attempts so you can see both in the timeline.

If you'd rather not offer the fallback (e.g. you can't wait 1–2 days), turn it off in **Settings → Identity → Bank verification → Fallback**.

## Related

* [Micro-deposits](micro-deposits.md) — fallback when Plaid isn't available.
* [Bank account verification](README.md) — parent flow.
* [Payments / Money movement](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/money-movement) — using a verified account for ACH.
