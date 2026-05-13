---
icon: people-roof
description: Identify and verify the people who actually own a business — typically anyone with 25% or more.
---

# Beneficial ownership

When you verify a business, you're really verifying the people behind it — the **beneficial owners**. Regulators care about this because shell companies are how illicit money moves; if you don't know the humans behind the LLC, you don't really know the business.

Evolve's KYB flow handles ownership collection and verification together. The business operator declares the owners, Evolve verifies each one, and the result is a complete owner-by-owner verification record attached to the business.

## What counts as a beneficial owner

The definition Evolve uses (matching FinCEN's Customer Due Diligence rule and most equivalent EU/UK rules):

* Anyone who **owns 25% or more** of the business, directly or indirectly.
* Anyone who **exercises significant control** — typically a CEO, managing director, general partner, or trustee.

For most small businesses, that's 1–4 people. For businesses with complex ownership (parent companies, trusts, fund structures), it can require traversing several layers.

{% hint style="info" %}
The 25% threshold is a regulatory floor, not a ceiling. Some banks and Enterprise customers configure Evolve to verify owners down to 10% or even 5% for higher-risk verticals. Set this in **Settings → Identity → Business verification → Ownership threshold**.
{% endhint %}

## How owners are collected

The hosted KYB form walks the operator through declaring ownership:

{% stepper %}
{% step %}

### Add each owner

For each owner, the operator enters: legal name, date of birth, residential address, ownership percentage, and role (Owner, Officer, or both).

{% endstep %}

{% step %}

### Confirm 100% accounted

The form requires that declared ownership totals at least 75% (since anyone under 25% isn't a beneficial owner under the rule). If ownership is split among many small holders, the operator can declare "Ownership distributed below threshold" and Evolve only verifies the controllers.

{% endstep %}

{% step %}

### Each owner verifies separately

For each declared owner, Evolve generates an [identity verification](../identity-verification/README.md) link. The owner clicks it (typically in an email Evolve sends) and completes a document + selfie verification on their own device. They don't need to be in the same place as the operator.

{% endstep %}
{% endstepper %}

## Verifying complex ownership

For businesses owned in part by other entities — a holding company, a trust, a fund — Evolve walks down the chain:

* If an entity owns ≥25% of your customer business, Evolve adds that entity as a sub-KYB.
* The sub-KYB collects *its* beneficial owners.
* Each layer is verified independently.

This can take weeks for genuinely complex structures. The dashboard shows the full ownership tree with per-node status, so you can see what's blocking completion.

## What you get back

When all owners are verified, the business record shows:

* Each owner's name, ownership %, role, verification status, and screening result.
* The full ownership tree (as a graph in the dashboard).
* A consolidated **KYB status** of `verified`, `failed`, or `manual_review`.

For audit purposes, every artifact Evolve gathered (declaration form, verification IDs, sanctions screening results) is retained and downloadable as a single PDF report from the dashboard.

## Re-verifying when ownership changes

Beneficial ownership isn't static — businesses sell shares, partners leave, founders dilute. The dashboard's **Business → Ownership monitoring** tracks public records (state filings, SEC filings, Companies House) and alerts you when:

* A new majority owner is recorded.
* A previously verified owner's stake drops below the threshold.
* The business's registration or corporate status changes.

When an alert fires, the right move is usually to re-verify any new owners and confirm the existing record is still accurate. The hosted re-verification flow makes this a one-click operation for the business operator.

## Privacy

Beneficial owner PII is treated the same as any individual identity verification — encrypted at rest, retained per your [retention policy](../../compliance/data-retention.md), and accessible only to authorized members of your team.

Specifically, you can configure who on your team can see beneficial owners' PII vs. just the verification status. Most teams restrict PII access to compliance staff and use anonymized identifiers everywhere else.

## Related

* [Business verification (KYB)](README.md) — the parent flow.
* [Sanctions screening](sanctions-screening.md) — runs against each owner.
* [Identity verification](../identity-verification/README.md) — the per-owner check.
* [Compliance → Regional requirements](../../compliance/regional-requirements.md) — country-specific ownership rules.
