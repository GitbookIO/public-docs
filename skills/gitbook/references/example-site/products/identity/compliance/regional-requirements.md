---
icon: globe
description: KYC, AML, and privacy obligations that vary by where your customers are.
---

# Regional requirements

The regulations that govern identity verification vary widely by country, and sometimes by state or province. Evolve is built to satisfy the major regimes — but the obligation to comply sits with you, not us. This page summarizes the rules that most affect Evolve customers and points to the specific Evolve features that help you satisfy them.

{% hint style="info" %}
**This page is a summary, not legal advice.** Talk to qualified counsel before launching in a new jurisdiction. The specifics of what you need to verify, retain, and report depend on your business model and customer base.
{% endhint %}

## United States

The federal floor is set by the Bank Secrecy Act (BSA) and Customer Identification Program (CIP) rules. State-level rules layer on top.

### Customer Identification Program (CIP)

For financial institutions and money-transmitter-licensed businesses, CIP requires you to:

* Collect **name, date of birth, address, and a government identifier** (SSN, ITIN, or passport number for non-residents).
* Verify the identity using documents, non-documentary methods, or both.
* **Retain records for 5 years** after the customer relationship ends.

Evolve's identity verification flow collects all the required fields and Evolve retains the verification record per your [data retention](data-retention.md) policy (default 7 years, configurable down to 5).

### OFAC

OFAC (Office of Foreign Assets Control) maintains the SDN list and other US sanctions programs. You must screen customers and counterparties against these lists. Evolve's [watchlist screening](../verification-flows/identity-verification/watchlist-screening.md) and [sanctions screening](../verification-flows/business/sanctions-screening.md) cover the OFAC lists by default.

### State-level

* **California** — CCPA and CPRA give consumers privacy rights including deletion. Evolve supports per-customer deletion (see [Data retention](data-retention.md#customer-deletion-requests)).
* **New York** — NY DFS Part 500 (cybersecurity rules) requires logged, audit-able access to PII. Evolve's [audit logs](audit-logs.md) cover this.

## European Union and EEA

The EU has the broadest set of obligations of any major region.

### GDPR

The General Data Protection Regulation imposes:

* A **lawful basis** for processing PII — typically "performance of a contract" or "compliance with legal obligation" for verification.
* **Data minimization** — only collect what you need. Don't run KYB if all you need is identity verification.
* **Right to access, correction, and erasure** for individuals.
* **Breach notification** within 72 hours.
* **Transfers outside the EU** require an adequacy decision or Standard Contractual Clauses.

Evolve is GDPR-compliant by default. Specific helps:

* Per-region retention policies (configurable to GDPR-aligned shorter windows).
* Per-customer deletion via dashboard or API.
* Data residency in EU regions for Enterprise customers.

### AMLD6

The Sixth Anti-Money-Laundering Directive sets the EU's KYC/KYB floor. Most of it overlaps with US BSA/CIP, with two notable additions:

* **Beneficial ownership at 25% or more** — same as US, but the EU verifies against national registers.
* **Adverse media checks** are explicitly required for higher-risk customers.

Evolve's [beneficial ownership](../verification-flows/business/beneficial-ownership.md) flow handles the 25% rule, and [sanctions screening](../verification-flows/business/sanctions-screening.md) includes EU adverse-media sources.

### eIDAS

For high-value transactions in the EU, eIDAS-compliant electronic identity verification is required. Evolve's identity verification flow can produce an **eIDAS-compatible audit trail** when configured for that mode (Settings → Identity → eIDAS mode).

## United Kingdom

UK rules largely mirror EU AMLD6, with UK-specific lists:

* **HMRC and JMLSG guidance** for AML compliance.
* **HMT consolidated list** for sanctions (in addition to UN, EU, OFAC).
* **Data Protection Act 2018** — UK's GDPR-equivalent, with one notable difference: shorter retention for some categories.

Evolve's UK setup uses HMT alongside the standard sanctions sources, and applies UK-specific retention defaults when you set the workspace region to UK.

## Other regions

Brief notes on regions Evolve supports today:

<details>

<summary>Canada</summary>

PIPEDA (federal privacy), provincial privacy regimes (notably Quebec's Law 25), and FINTRAC's PCMLTFA for AML. Evolve supports Canadian provincial driver's licenses and provincial ID cards in identity verification, and screens against the Canadian Consolidated Sanctions list.

</details>

<details>

<summary>Australia</summary>

Privacy Act 1988 (federal) and AUSTRAC's AML/CTF rules. Australian passports, driver's licenses, and Medicare cards are supported in identity verification. AUSTRAC screening lists are included in Enterprise sanctions screening.

</details>

<details>

<summary>Singapore</summary>

PDPA (privacy) and MAS (financial services). Singapore IC and FIN cards supported. MyInfo integration available for instant data prefill (Enterprise only).

</details>

<details>

<summary>India</summary>

Aadhaar verification supported via Evolve's UIDAI partnership (Enterprise only, for customers with the appropriate license). RBI KYC rules apply for financial-services customers.

</details>

<details>

<summary>Other countries</summary>

For countries not listed here, identity verification works (passports are universal), but country-specific document types may not all be supported. The full list is in **Settings → Identity → Supported documents**.

</details>

## Re-verification cadence

Most regimes don't require re-verification on a fixed cadence, but several recommend it. Common patterns:

| Regime | Recommended re-verification |
| --- | --- |
| US (BSA / CIP) | On material customer-relationship change (e.g. address change, large transaction). |
| EU (AMLD6) | Every 1–3 years for higher-risk customers; on trigger event. |
| UK (HMRC) | Every 1–3 years; risk-based. |
| Canada (PCMLTFA) | Every 2 years for high-risk; on trigger event. |

Evolve's re-verification API lets you trigger a fresh flow against an existing customer at any time. Combined with [audit logs](audit-logs.md), this gives you the cadence your regime requires plus the documented record of having done it.

## Related

* [Audit logs](audit-logs.md) — the trail your auditor needs.
* [Data retention](data-retention.md) — region-specific retention configuration.
* [Beneficial ownership](../verification-flows/business/beneficial-ownership.md) — the 25% rule under FinCEN, EU AMLD6, and UK MLRs.
* [Watchlist screening](../verification-flows/identity-verification/watchlist-screening.md) — OFAC, UN, EU, UK lists.
