---
icon: circles-overlap
description: Connected accounts, transfers, and checkout sessions for marketplace platforms.
---

# Connect API

The Connect API extends Payments with the platform-specific resources — connected accounts (sellers), transfers (moving funds to sellers), and checkout sessions (taking payments on a seller's behalf). The operation reference is auto-generated and listed below this page in the sidebar.

## Resources

* **Connected accounts** — the sellers on your platform. One per seller.
* **Transfers** — move funds from your platform balance to a connected account.
* **Checkout sessions** — hosted or embedded checkout for a Connect payment.

## A minimal flow

```mermaid
flowchart LR
    A[POST /connected_accounts] --> B[Seller onboards via hosted URL]
    B --> C[POST /checkout_sessions]
    C --> D[Buyer pays]
    D --> E[Funds split: platform fee + seller balance]
    E --> F[Seller payout on schedule]
```

## Application fees

Every checkout session can carry an `application_fee_amount` — your platform's cut, in the smallest currency unit:

```http
POST /v2/checkout_sessions
{
  "amount": 10000,
  "currency": "usd",
  "connected_account": "acct_3KsM12pL9q",
  "application_fee_amount": 200
}
```

That charges the buyer $100, transfers $98 to the seller's connected account, and credits $2 to your platform balance. By default the card processing fee is netted from your application fee — see [Connect → Splitting payments](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/platform-setup/splitting-payments) for the full mechanics including pass-through fees.

## Direct charges vs destination charges

Two patterns for routing a payment to a seller:

| Pattern | When to use |
| --- | --- |
| **Direct charge** | The seller is the merchant of record. Set `Evolve-Account: acct_*` header on the charge. The seller's statement descriptor appears on the buyer's card statement. |
| **Destination charge** | The platform is the merchant of record. Charge happens on the platform; a transfer moves the funds to the connected account. The platform's descriptor appears on the buyer's statement. Most Connect platforms use this. |

Choose at the platform level by setting your default in **Connect → Settings → Charge type** in the dashboard. Override per checkout session if needed.

## Conceptual background

For the product-side concepts — onboarding flow, payout scheduling, dispute routing, refund splits — see the [Connect product space](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/).
