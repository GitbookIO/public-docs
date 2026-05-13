---
icon: id-card
description: Verification flows, decisions, retention, and the most-asked Identity product questions.
---

# Identity questions

## Which verification flow do I need?

Three flows, picked by what you're verifying:

| Verifying... | Use this flow |
| --- | --- |
| An individual customer | Identity verification (document + selfie) |
| A bank account belongs to the customer | Bank account verification (Plaid or micro-deposits) |
| A business and its owners | Business verification (KYB) |

Most consumer products need only identity verification. ACH-accepting products add bank verification. Marketplaces and B2B platforms add KYB. The [decision tree](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows#a-decision-tree) shows it visually.

## How long does verification take?

| Flow | Time |
| --- | --- |
| Identity (document + selfie) | 60–90 seconds for the customer; result in seconds |
| Bank verification (Plaid) | 30–60 seconds for the customer; result in seconds |
| Bank verification (micro-deposits) | 1–2 business days |
| Business verification (KYB, simple LLC) | 2 business days end-to-end |
| Business verification (complex ownership) | Up to 10 business days |

Manual review (when an automated check is inconclusive) typically resolves within an hour during business hours.

## Why did a verification fail?

The reason code on the session timeline tells you. The most common ones:

| Code | Cause | What customer can do |
| --- | --- | --- |
| `document_expired` | ID is past expiry | Provide a current document |
| `document_tampered` | Pixel analysis detected manipulation | Retry with different document; flagged as fraud |
| `document_unrecognized` | Couldn't match a template; usually a partial capture | Recapture |
| `selfie_mismatch` | Face doesn't match the ID photo | Retry; if persistent, manual review |
| `liveness_failed` | Spoof attempt detected | No retry — fraud |
| `data_mismatch` | Typed data doesn't match document | Correct typed data |

For the full code reference, see [Document review](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/identity-verification/document-review).

## What countries can I verify in?

Identity verification (document + selfie) works in **195 countries** — every country except those on the OFAC blocklist. Specific document type support varies by country; the dashboard's country picker shows what's supported.

Bank verification (Plaid) is broadest in the US, with Canada, UK, France, Spain, Netherlands, and Ireland in coverage. For other countries, micro-deposits or country-specific open-banking flows are alternatives — talk to your account team for non-listed countries.

Business verification (KYB) covers ~50 countries through national-register integrations. Outside that list, KYB falls back to manual document review which takes longer.

## How do I trigger re-verification?

Three patterns most teams use:

1. **On a chargeback** — fraud signal warrants a fresh check.
2. **On a transaction over a threshold** — high-value implies higher trust requirements.
3. **On a profile change** — address change to a different country, name change, etc.

The [re-verification tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/verification/re-verification-trigger) covers the full implementation. For scheduled re-verification (every N months for regulated regimes), use the dashboard's scheduled re-verification feature instead of building it yourself.

## How long is verification data retained?

Two retention windows:

* **Raw images** (document fronts, backs, selfies) — 30 days by default. Configurable from 1 day to 7 years in **Settings → Identity → Retention**.
* **Extracted data and decisions** (name, DOB, document number, decision reason) — 7 years by default. Required by most regulatory regimes.

For customer deletion requests under GDPR/CCPA, see [Data retention → Customer deletion requests](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/compliance/data-retention#customer-deletion-requests).

## Can I see the verified data on the customer record?

Yes, from **Identity → Sessions → [session]**. Verified PII (extracted name, DOB, address) shows in the session detail page. Be careful exposing this to other parts of your team — leakage of verified PII to the wrong dashboard view is the most-cited compliance issue we see.

The [audit log](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/compliance/audit-logs) records every PII view, with `pii.accessed` events tied to the team member.

## What is watchlist screening, and do I need it?

Watchlist screening checks an identity against sanctions lists (OFAC, UN, EU, UK HMT), PEP lists, adverse media, and your own internal blocklists.

You probably need it if:
* You operate in a regulated vertical (financial services, money transmission, gambling, crypto).
* You're a marketplace and your sellers are subject to payment-aggregator obligations.
* Your bank or auditor has told you that you need it.

You probably don't need it for typical e-commerce or community products.

Watchlist screening is Enterprise-only. See [Watchlist screening](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/identity-verification/watchlist-screening).

## How does ongoing monitoring work?

For verified businesses (KYB), Evolve re-screens against the latest sanctions lists weekly. If a previously-clear entity matches a newly-added entry, you get a `screening.match_added` webhook and a dashboard alert.

Most teams suspend the entity pending a manual review. The cost is included with the original KYB at no extra fee.

## What's the difference between Plaid instant and micro-deposits?

| | Plaid instant | Micro-deposits |
| --- | --- | --- |
| Speed | 30–60 seconds | 1–2 business days |
| Coverage | ~12,000 US banks | Any US bank |
| Cost | $2.50/verification | $0.80/verification |
| Customer effort | Sign in to bank | Wait for deposits, type amounts |
| Risk signals | Yes (balance, NSF history) | No |

Most teams use Plaid first with micro-deposits as fallback — covered automatically when you set `method: "auto"`. Walked through in the [Plaid bank verification tutorial](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/verification/plaid-bank-verification).

## Where can I find more answers?

* [Community: KYB beneficial-ownership](https://gitbookio.github.io/evolve-demo/connections/community/kyb-beneficial-ownership-edge-cases.html)
* [YouTube: KYB end-to-end](https://gitbookio.github.io/evolve-demo/connections/youtube/kyb-end-to-end.html)
* [Identity product space](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/)
* [Tutorials: Verify customers and businesses](https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/#verify-customers-and-businesses)
