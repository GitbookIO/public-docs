---
icon: user-plus
description: How a seller goes from "signed up to your platform" to "ready to take payments."
---

# Onboarding sellers

Before a seller can take payments, Evolve has to know who they are — legal name, banking details, identity proof. This is the seller-onboarding flow, and it's the first place most platforms spend engineering effort on Connect.

The flow uses [Identity verification](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows) under the hood — Connect adds the connected-account specifics on top. You don't build the verification logic; you decide what data to collect, who collects it (the seller in a hosted flow, your platform in a programmatic flow), and what happens when something fails.

## What gets collected

Every connected account requires:

{% columns %}
{% column width="50%" %}

### <i class="fa-id-card" style="color:$primary;">:id-card:</i> Legal identity

* Legal name (individual or business).
* Date of birth (individuals) or formation date (businesses).
* Government ID number (SSN, EIN, or country equivalent).
* Address.

For businesses, plus [beneficial ownership](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/business/beneficial-ownership) for owners ≥25%.

{% endcolumn %}

{% column width="50%" %}

### <i class="fa-building-columns" style="color:$primary;">:building-columns:</i> Banking

* Bank account for payouts.
* Account holder name (must match the legal entity).
* Verification — Plaid instant or micro-deposits ([details](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/bank-account)).

For non-US banks, plus tax forms (W-9 for US, W-8 for non-US).

{% endcolumn %}
{% endcolumns %}

For some seller types and regions, additional fields are required — you'll see these prompted as part of the hosted onboarding flow when relevant.

## Three onboarding shapes

Pick one based on how much control you want:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-link" style="color:$primary;">:link:</i></h3></td><td><strong>Hosted</strong></td><td>Seller fills in everything on an Evolve-hosted page. Fastest to launch.</td><td></td></tr><tr><td><h3><i class="fa-window-maximize" style="color:$primary;">:window-maximize:</i></h3></td><td><strong>Embedded</strong></td><td>Same fields, rendered inside your site. Your URL.</td><td></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>Programmatic</strong></td><td>Your code submits the data — for sellers who've already given it to you elsewhere.</td><td></td></tr></tbody></table>

Most platforms launch with hosted, then move to embedded once they're confident in their seller-onboarding UX.

## The seller's experience (hosted)

```mermaid
flowchart LR
    Invite[Invite email] --> Form[Hosted form]
    Form --> ID[Identity verification]
    ID --> Bank[Bank verification]
    Bank --> Done[Ready to take payments]
```

Typical timing:

| Step | How long |
| --- | --- |
| Form (legal info, address) | 3–5 min |
| Identity verification (document + selfie) | 1–2 min |
| Bank verification (Plaid) | 1 min |
| Bank verification (micro-deposits) | 1–2 days |
| Manual review (if triggered) | 1 hour to 1 business day |

Most US individuals complete in under 10 minutes end to end if they pass everything on the first try.

## Pre-fill from your platform

Most platforms already have some of the data Evolve needs — the seller's name, email, and address from your sign-up flow. Pre-fill those into the hosted form so the seller doesn't re-enter them.

You pre-fill at session creation time. The seller can still edit the values; pre-filling just saves them typing.

## What happens when something fails

A failed onboarding doesn't mean a permanently rejected seller — most failures are recoverable.

<details>

<summary>Identity verification fails</summary>

Reasons: expired document, document tampering signal, selfie mismatch. The seller sees a clear error and can retry up to 3 times in 24 hours. If they're still stuck, your team can manually review from the dashboard.

</details>

<details>

<summary>Bank verification fails</summary>

Plaid couldn't reach the bank, or the customer entered wrong micro-deposit amounts. The flow falls back to the alternate method ([Plaid → micro-deposits](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/bank-account/micro-deposits), or vice versa) automatically.

</details>

<details>

<summary>Sanctions match</summary>

Rare but serious. The seller can't be onboarded. The dashboard shows the match details to your compliance team; depending on the match confidence, either you reject the seller or escalate to manual review.

</details>

<details>

<summary>Tax form mismatch</summary>

The name on the tax form doesn't match the business legal name. Usually a typo on either side. The seller can re-upload.

</details>

## Re-onboarding when info changes

Sellers' info isn't static. They move, change banks, restructure their business. When this happens:

* **Bank account changes** — the seller updates from their portal; verification re-runs automatically.
* **Address changes** — accepted up to a small threshold of the original; large changes trigger re-verification.
* **Beneficial owner changes** — re-verification required for the new owners (KYB only).

The dashboard surfaces a "Profile changed" badge on the seller until the re-verification completes, and you can hold their payouts during the change if your risk policy requires it.

## Bulk onboarding

For platforms migrating from another payment provider, Evolve supports bulk onboarding — you upload a CSV of seller data, Evolve generates onboarding URLs, and you email them out from your side. The flow is the same hosted experience for the seller; the difference is just how the URLs get generated.

Bulk onboarding is usually a one-shot during platform launch or migration. Day-to-day, you'll create connected accounts as sellers sign up.

## Related

* [Connect quickstart](../quickstart/onboard-your-first-seller.md) — walkthrough with a test seller.
* [Identity verification](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/identity-verification) — the verification engine behind onboarding.
* [Bank account verification](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/bank-account) — the bank-side details.
* [Beneficial ownership](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/business/beneficial-ownership) — for business sellers.
