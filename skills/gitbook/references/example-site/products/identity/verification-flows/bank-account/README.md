---
icon: building-columns
description: Confirm a bank account belongs to the customer before debiting or paying out.
---

# Bank account verification

Bank account verification proves the customer owns the account they've handed you — important before you debit them with ACH, before you push a payout to them, or before you accept them as a payment recipient on a marketplace.

Evolve supports two methods. **Plaid instant** is faster (one tap) but only works for banks Plaid covers. **Micro-deposits** work for any US bank account but take 1–2 business days.

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="warning" icon="lock" %}
**Bank account verification is a Growth and Enterprise feature.** Starter accounts can verify identities but not bank accounts.
{% endhint %}

{% endif %}

## Pick a method

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-bolt" style="color:$primary;">:bolt:</i></h3></td><td><strong>Plaid instant</strong></td><td>One-tap, real-time. Best customer experience.</td><td><a href="plaid-instant.md">plaid-instant.md</a></td></tr><tr><td><h3><i class="fa-coins" style="color:$primary;">:coins:</i></h3></td><td><strong>Micro-deposits</strong></td><td>Two small test deposits, customer confirms amounts. 1–2 business days.</td><td><a href="micro-deposits.md">micro-deposits.md</a></td></tr></tbody></table>

## When to use which

| Situation | Method |
| --- | --- |
| Customer's bank is on Plaid (most major US banks) | Plaid instant |
| Customer's bank isn't on Plaid (small credit unions, foreign banks) | Micro-deposits |
| You want every customer to have the same UX | Plaid first, fall back to micro-deposits |
| Speed is critical (real-time onboarding) | Plaid instant only |
| Cost is critical | Micro-deposits ($0.80 vs $2.50) |

The default flow Evolve generates tries Plaid first and falls back to micro-deposits automatically when Plaid can't help. You can override this in **Settings → Identity → Bank verification**.

## What gets verified

Both methods confirm:

* The **routing and account numbers** match a real, open account.
* The **account holder name** matches what the customer told you.

Plaid instant adds:

* The **balance** (helpful if you want to gate large debits on available funds).
* Recent **transaction history** (used by some teams for risk scoring).

Both methods generate a `bank_account.verified` webhook event when complete, with the masked account number and the verification method used.

## Storing the result

Once verified, the bank account is attached to a Customer record (see [Saved payment methods](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/accept-payments/saved-payment-methods) in Payments) and can be used for ACH debits or payouts without re-verification — until the customer's bank reissues credentials or you trigger a re-verification.

## What's logged

Every bank account verification creates an entry in the [audit log](../../compliance/audit-logs.md) with the method used, the verification status, and which member of your team initiated it (if it was triggered from the dashboard rather than the API).

## Related

* [Plaid instant](plaid-instant.md) — setup and customer experience.
* [Micro-deposits](micro-deposits.md) — what the customer sees, retry handling.
* [Payments / Money movement](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/money-movement) — how verified bank accounts are used in ACH flows.
