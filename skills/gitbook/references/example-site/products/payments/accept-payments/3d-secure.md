---
icon: shield-halved
description: When 3-D Secure is required, when it's optional but worth it, and how Evolve handles it.
---

# 3-D Secure and SCA

3-D Secure (3DS) is an extra step at checkout where the cardholder authenticates with their bank — usually a one-time code, a push notification, or a biometric prompt. When 3DS succeeds, the card-issuing bank takes on the liability for fraud chargebacks. When it's not used, you do.

3DS is **required** for cards issued in the EU and UK (under SCA rules) and **optional but often worth it** elsewhere.

## When Evolve applies 3DS automatically

You don't have to configure anything for required cases. Evolve detects them based on the card BIN and the transaction context:

| Trigger | Result |
| --- | --- |
| Card issued in the EEA, UK, or India | 3DS challenge required |
| Transaction over €30 with a European card | 3DS challenge required (with limited exemptions) |
| Card flagged as high-risk by the issuer | 3DS challenge required |
| Recurring payment using a saved card with a recorded mandate | Often exempt |
| Low-value transaction (<€30) | Often exempt under low-value-payment rules |

## When you might want to require 3DS

Even where it's not required, some teams turn 3DS on for high-value payments or known-risk patterns. The trade-off is real:

{% columns %}
{% column width="50%" %}

#### Pros

* Liability shifts to the issuer for fraud chargebacks.
* Approval rates often go up on cards the issuer was about to decline.
* Strong signal to the network that you take fraud seriously.

{% endcolumn %}

{% column width="50%" %}

#### Cons

* Adds 5–15 seconds to the checkout flow.
* 1–3% of customers abandon during the challenge.
* Costs $0.05 per attempt outside required cases.

{% endcolumn %}
{% endcolumns %}

## Configuring 3DS rules

In **Settings → Risk → 3-D Secure**, you can set rules for when 3DS should be requested:

* **Always** — every payment goes through 3DS.
* **Required only** (default) — Evolve handles required cases; everything else skips 3DS.
* **By rule** — your own rules layered on top of the required cases.

A rule is a condition (`amount`, `currency`, `country`, `payment_method`, `customer_history`) and an action (`require_3ds`, `skip_3ds`). Most teams start with one rule:

> Require 3DS when amount is over $500 and the customer has no prior successful payments.

## What customers see

Three flows, depending on the card and the issuer:

<details>

<summary>Frictionless</summary>

The issuer authenticates the customer in the background based on signals Evolve sends — device, browser, transaction history. The customer sees nothing extra. About 60% of European 3DS challenges resolve frictionlessly today.

</details>

<details>

<summary>Challenge</summary>

The customer is asked to authenticate — usually a one-time code, push notification, or biometric in their banking app. Takes 5–15 seconds. After they confirm, the payment continues automatically.

</details>

<details>

<summary>Failure</summary>

The customer fails to authenticate (wrong code, timeout, declined the push). The payment fails with `authentication_required` or `authentication_failed`. They can try again with a different card.

</details>

## SCA exemptions

Strong Customer Authentication (SCA) is the EU regulation behind 3DS. It allows a few exemptions where authentication can be skipped without losing the liability shift entirely:

| Exemption | Used when |
| --- | --- |
| **Low-value** | Transaction under €30 (max 5 in a row, then forced auth) |
| **Trusted beneficiary** | Customer has added you to their bank's trusted-merchants list |
| **Merchant-initiated transaction** | Recurring charge against a previously authenticated card with a recorded mandate |
| **Transaction risk analysis (TRA)** | Evolve's risk score is low enough that the issuer accepts a frictionless flow |

Evolve applies exemptions automatically when they fit. You can see which exemption was used (if any) on the payment timeline.

## Related

* [Saved payment methods](saved-payment-methods.md) — mandates and merchant-initiated transactions.
* [Smart routing](smart-routing.md) — pairing 3DS with the most likely-to-approve route.
* [Disputes and chargebacks](../reconciliation/disputes.md) — what the liability shift means in practice.
