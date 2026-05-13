---
icon: shield-halved
hidden: true
description: Screen verified identities against sanctions, PEP, and adverse media lists. Enterprise only.
---

# Watchlist screening

{% hint style="warning" %}
**This page is intentionally hidden from the main navigation.** Watchlist screening is an advanced compliance feature that most teams don't need. If you're not on Enterprise, or you're not in a regulated vertical, you can safely ignore this page.
{% endhint %}

Watchlist screening checks an identity against four kinds of list:

* **Government sanctions lists** — OFAC SDN, UN, EU, UK HMT, and ~40 country-specific lists.
* **Politically exposed persons (PEPs)** — current and former senior public officials, their family, and close associates.
* **Adverse media** — recent news mentions tying the person to financial crime, terrorism, or other reputational risks.
* **Internal blocklists** — names you've added yourself, e.g. customers you've terminated for fraud.

It's run on top of an identity verification — the document and selfie checks confirm the person is who they say, and the watchlist check decides whether you're allowed to do business with them.

{% if visitor.claims.unsigned.plan !== "enterprise" %}

{% hint style="warning" icon="lock" %}
**Watchlist screening is Enterprise-only.** It requires the data partnerships and ongoing-monitoring infrastructure available only on the Enterprise plan. [Talk to your account team](mailto:support@evolve.com).
{% endhint %}

{% endif %}

## When you need it

You probably need watchlist screening if:

* You operate in a regulated vertical (financial services, money transmission, crypto, gambling, pharma).
* You're a marketplace and your sellers are subject to sanctions screening as a payment-aggregator obligation.
* You've been told by your bank, your auditor, or your compliance team that you need it.

You probably don't need it for typical e-commerce, SaaS, or community products.

## How matching works

Watchlist matching is a fuzzy-name match, not an exact-string lookup. Names on lists vary in spelling, transliteration, and order — Mohammed vs. Mohammad, Vladimir Vladimirovich Putin vs. Putin, Vladimir. Evolve's matcher accounts for all of this.

For each identity verified, the matcher returns:

| Result | What it means |
| --- | --- |
| **Clear** | No matches above the configured threshold. |
| **Match** | One or more names matched at high confidence. Verification status becomes `failed` and the customer cannot proceed without manual override. |
| **Possible match** | Match at moderate confidence. Verification goes to manual review. |

The threshold is configurable in **Settings → Identity → Screening sensitivity**. Most teams keep the default — it's calibrated to balance false-positive rate against the consequences of missing a true match.

## Ongoing monitoring

A clear screening result today doesn't stay clear forever — sanctions lists update daily, and a previously unsanctioned person can be added at any time. Evolve runs **ongoing monitoring** automatically:

* Every verified identity is **re-screened weekly** against the latest list snapshots.
* If a previously clear identity matches a newly added entry, you get a `screening.match_added` webhook and a dashboard alert.
* You decide what to do — most teams suspend the customer pending a manual review.

The cost is $0.10 per re-screen, billed against your monthly verification volume. You can opt out of ongoing monitoring per-verification via the strictness settings if a one-time check is sufficient.

## Adverse media

Adverse media screening is the loosest of the four categories — it returns any news mentions tying the person to specific risk topics:

* Money laundering and financial crime
* Terrorism financing
* Corruption and bribery
* Trafficking
* Cyber-crime and fraud

Because adverse media draws from open-source news, it produces more false positives than sanctions or PEP lists. Most teams treat adverse media matches as a manual-review trigger rather than an automatic block.

## What's logged

Every screening result is a permanent entry in your [audit log](../../compliance/audit-logs.md), including:

* The lists checked, with version timestamps.
* The matches found (or absence thereof).
* Any manual override applied, by whom, with the stated reason.

This is the audit trail your auditor and your bank will want to see.

## Related

* [Identity verification](README.md) — screening sits on top of identity verification.
* [Business verification → Sanctions screening](../business/sanctions-screening.md) — the equivalent check for businesses.
* [Audit logs](../../compliance/audit-logs.md) — the screening audit trail.
* [Regional requirements](../../compliance/regional-requirements.md) — when screening is mandatory.
