---
icon: circles-overlap
description: Connected accounts, splits, payouts, marketplace patterns — the most-asked Connect questions.
---

# Connect questions

## Do I need Connect?

Yes if you take payments **on behalf of others** — marketplaces, B2B platforms paying out to vendors, SaaS apps that route money to customers. No if you only take payments **for yourself** (typical e-commerce, SaaS billing, donations).

If you're not sure: ask "does the money belong to me, or to someone using my product?" If the latter, that's Connect.

## What plan do I need for Connect?

Growth or Enterprise. Starter doesn't include Connect.

| | Growth | Enterprise |
| --- | --- | --- |
| Connected accounts | Up to 100 | Unlimited |
| Hosted onboarding | ✅ | ✅ |
| Embedded checkout | — | ✅ |
| Custom (white-label) onboarding | — | ✅ |
| Per-seller dispute routing | ✅ | ✅ |

For the full per-tier breakdown, see [Connect → Plan availability](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/#plan-availability).

## How do I onboard a seller?

Two integration shapes:

* **Hosted** — Evolve generates an onboarding URL, you email it to the seller. Most platforms launch with this. The walkthrough is in the [Onboard your first sellers tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/marketplace/onboard-sellers).
* **Custom** — Enterprise-only. You build your own forms; data is submitted programmatically to Evolve. See [Build a custom Connect onboarding flow](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/marketplace/custom-onboarding).

Most teams should use hosted unless brand standards or specific UX requirements demand custom. Hosted updates automatically as KYC requirements change; custom requires you to keep up.

## Why is my seller's account `restricted`?

Risk team has flagged something. The seller's record in **Connect → Connected accounts → [account] → Status** shows the specific reason. Common ones:

* High dispute rate (above 1%)
* Sudden volume spike that triggers fraud screening
* Sanctions match found during ongoing monitoring
* Manual review pending after a flagged transaction

Restricted accounts can't take new charges; existing balances pay out normally. Contact your account team to discuss next steps for the specific seller.

## How do I take my platform fee on each payment?

Set `application_fee_amount` when creating the Checkout session:

```http
POST /v2/checkout_sessions
{
  "amount": 10000,
  "currency": "usd",
  "connected_account": "acct_3KsM12pL9q",
  "application_fee_amount": 200
}
```

That's $100 to the buyer, $98 transferred to the seller, $2 to your platform. The [split-payments tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/marketplace/split-payments) covers conditional fee logic (per-seller-tier, per-product-category, etc.).

## How are processing fees split between platform and seller?

By default, the card processing fee comes off the platform's application fee. Pass `application_fee_includes_processing: false` to make the seller absorb it instead.

Most marketplaces with thin take-rates pass through to sellers. Most marketplaces competing on seller experience absorb. Pick once at the platform level and keep it consistent.

## Can a seller have a custom payout schedule?

Yes. The platform sets the default in **Connect → Settings → Default payout schedule**. Sellers can override their own (within the schedules you allow) from their seller portal.

For on-demand payouts (seller taps "Pay me now" for instant cash), enable in **Connect → Settings → Instant payouts**. The 1% fee can be paid by seller, platform, or split. Available on Enterprise. See [payout-schedules tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/marketplace/payout-schedules).

## What happens to disputes on a Connect platform?

The **platform is the merchant of record** — disputes are filed against the platform's merchant ID. Three policies for who absorbs the disputed amount + $15 fee:

* **Pass to seller** — most common.
* **Platform absorbs** — for premium-tier sellers as a perk.
* **Split** — platform takes the fee, seller takes the disputed amount.

Set the default in **Connect → Settings → Dispute policy**, override per-seller. For evidence collection, most platforms delegate to the seller — see [disputes-at-scale tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/marketplace/disputes-at-scale).

## Why is a seller's payout `failed`?

Bank account became invalid — closed, frozen, name mismatch, or wrong details. The dashboard shows the bank's reason code. The amount returns to the seller's balance; they update the bank account in their portal and the next scheduled payout includes the failed amount.

Three failed payouts in a row auto-pause the seller until you intervene. See the [community thread on stuck Connect payouts](https://gitbookio.github.io/evolve-demo/connections/community/connect-payout-stuck.html) for the typical playbook.

## Can I have a seller in a country my platform doesn't operate in?

Sometimes — depends on the country pair. Some platform/seller country combinations have regulatory or banking restrictions. Talk to your account team before promising a new seller country to your operators.

For platforms operating in multiple countries themselves, you can configure per-region defaults (different fee structure, different payout schedule) in **Connect → Settings → Per-region**.

## What's the difference between direct charges and destination charges?

* **Direct charge** — the seller is the merchant of record. Set `Evolve-Account: acct_*` header on the charge. The seller's statement descriptor shows on the buyer's bank statement.
* **Destination charge** — the platform is the merchant of record. The platform's descriptor shows. A separate transfer moves the funds to the seller's connected account.

Most Connect platforms use destination charges — buyers see a consistent platform brand, and the platform has clearer dispute responsibility. Pick once at the platform level in **Connect → Settings → Charge type**.

## Where can I find more answers?

* [Community: Stuck Connect payouts](https://gitbookio.github.io/evolve-demo/connections/community/connect-payout-stuck.html)
* [YouTube: Chargebacks at scale](https://gitbookio.github.io/evolve-demo/connections/youtube/chargebacks-at-scale.html)
* [Connect product space](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/)
* [Tutorials: Run a marketplace with Connect](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/#run-a-marketplace-with-connect)
