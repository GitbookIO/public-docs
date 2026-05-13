---
icon: id-card
description: Verify customers and partners — documents, selfies, bank accounts, and business records.
cover: .gitbook/assets/identity-cover.png
coverY: 0
layout:
  width: wide
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Identity

{% columns %}
{% column %}
Evolve Identity verifies the people and businesses you transact with — through document review, biometric selfie checks, bank account verification, and business records (KYB). It's the same platform as Payments, with the same dashboard, the same auth, and the same settlement of fees.

<button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">Ask the Evolve docs</button>

<button type="button" class="button secondary" data-action="ask" data-query="Which verification flow should I use?" data-icon="route">Which flow?</button> <button type="button" class="button secondary" data-action="ask" data-query="What documents are accepted in each country?" data-icon="passport">Documents</button> <button type="button" class="button secondary" data-action="ask" data-query="How do I screen against watchlists?" data-icon="shield-halved">Screening</button>
{% endcolumn %}

{% column %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

This space demonstrates **nested page groups** — Verification flows has parent pages (Identity, Bank, Business) each with their own subpages. It also includes a **hidden page**: [Watchlist screening](verification-flows/identity-verification/watchlist-screening.md) doesn't appear in the sidebar nav but is accessible via direct link.

{% if !visitor.claims.unsigned.persona %}
Try a persona to see adaptive content in action across the site:

<a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="seedling">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona %}
<i class="fa-id-card-clip" style="color:$info;">:id-card-clip:</i> You are currently <code class="expression">visitor.claims.unsigned.persona === "prospect" ? "a prospect user exploring the product" : visitor.claims.unsigned.persona === "new" ? "a new user" : visitor.claims.unsigned.persona === "existing" ? "an existing user" : visitor.claims.unsigned.persona === "partner" ? "a partner" : ""</code><code class="expression">visitor.claims.unsigned.plan ? " on the " + visitor.claims.unsigned.plan.charAt(0).toUpperCase() + visitor.claims.unsigned.plan.slice(1) + " plan" : ""</code>. [<mark style="color:$primary;">Reset</mark>](https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=)
{% endif %}

{% if visitor.claims.unsigned.persona === "prospect" %}
<a class="button primary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a class="button primary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a class="button primary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/identity?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a class="button primary" data-icon="handshake-angle">Partner</a>
{% endif %}
{% endhint %}
{% endcolumn %}
{% endcolumns %}

***

## <i class="fa-sparkle" style="color:$info;">:sparkle:</i> Picked for you

{% if visitor.claims.unsigned.persona === "prospect" %}
{% hint style="info" icon="store" %}
**Evaluating Evolve Identity?** Get an overview of how the verification flows fit together.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-list-check" style="color:$primary;">:list-check:</i></h3></td><td><h3><strong>Verification flows</strong></h3></td><td>Identity, bank, and business verification — when to use which.</td><td><a href="verification-flows/README.md">verification-flows</a></td></tr><tr><td><h3><i class="fa-receipt" style="color:$primary;">:receipt:</i></h3></td><td><h3><strong>Per-verification pricing</strong></h3></td><td>What each flow costs across Starter, Growth, and Enterprise.</td><td><a href="quickstart/test-and-live-mode.md">test-and-live-mode</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
{% hint style="info" icon="hand-wave" %}
**New to Identity?** Run a verification in five minutes — no integration required.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><h3><strong>Run your first verification</strong></h3></td><td>Send a verification link, complete it with test data, see the result land.</td><td><a href="quickstart/run-your-first-verification.md">run-your-first-verification</a></td></tr><tr><td><h3><i class="fa-id-card" style="color:$primary;">:id-card:</i></h3></td><td><strong>Identity verification flow</strong></td><td>Document + selfie liveness, configurable strictness.</td><td><a href="verification-flows/identity-verification/README.md">identity-verification</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
{% hint style="info" icon="arrows-left-right" %}
**Coming from Stripe Identity?** Most flows map directly — document + selfie, bank verification, and watchlist screening.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-arrows-left-right" style="color:$primary;">:arrows-left-right:</i></h3></td><td><h3><strong>Migrate from Stripe Identity</strong></h3></td><td>Field mapping, parallel-run pattern, and the cutover checklist.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/migrate-from-stripe">migrate-from-stripe</a></td></tr><tr><td><h3><i class="fa-building-columns" style="color:$primary;">:building-columns:</i></h3></td><td><strong>Bank verification with Plaid</strong></td><td>Instant verification with micro-deposit fallback.</td><td><a href="verification-flows/bank-account/plaid-instant.md">plaid-instant</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
{% hint style="info" icon="building" %}
**Setting up enterprise compliance?** Watchlist screening, KYB, and ongoing monitoring are the Enterprise-tier capabilities.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-briefcase" style="color:$primary;">:briefcase:</i></h3></td><td><h3><strong>Business verification (KYB)</strong></h3></td><td>Beneficial ownership, sanctions screening, ongoing monitoring.</td><td><a href="verification-flows/business/README.md">business</a></td></tr><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>Watchlist screening</strong></td><td>OFAC, UN, EU, UK HMT, PEP, and adverse media. Enterprise only.</td><td><a href="verification-flows/identity-verification/watchlist-screening.md">watchlist-screening</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona %}
***
{% endif %}

{% if !visitor.claims.unsigned.persona %}
## Get started
{% endif %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><strong>Quickstart</strong></td><td>Run your first verification in five minutes.</td><td><a href="quickstart/run-your-first-verification.md">run-your-first-verification</a></td></tr><tr><td><h3><i class="fa-list-check" style="color:$primary;">:list-check:</i></h3></td><td><strong>Verification flows</strong></td><td>Identity, bank, and business verification — when to use which.</td><td><a href="verification-flows/README.md">verification-flows</a></td></tr><tr><td><h3><i class="fa-scale-balanced" style="color:$primary;">:scale-balanced:</i></h3></td><td><strong>Compliance</strong></td><td>Audit logs, retention, regional requirements.</td><td><a href="compliance/audit-logs.md">audit-logs</a></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>API reference</strong></td><td>Endpoints, SDKs, and try-it.</td><td><a href="https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/identity-api/">identity-api</a></td></tr></tbody></table>

## What's new

* **Live document capture in 195 countries** — every country except the dozen on the OFAC blocklist. [Read more](verification-flows/identity-verification/document-review.md).
* **Selfie liveness 2.0** — passive liveness, no head turns required. Lifts completion rates by ~12%. [Read more](verification-flows/identity-verification/selfie-and-liveness.md).
* **Plaid instant for businesses** — same one-tap flow, now for business bank accounts. [Read more](verification-flows/bank-account/plaid-instant.md).

## Get help

{% columns %}
{% column width="50%" %}
#### Talk to support

For account-specific questions, compliance reviews, or production incidents, contact your account team or open a ticket from the dashboard.

<a href="https://gitbook.com" class="button primary">Open a ticket</a>
{% endcolumn %}

{% column width="50%" %}
#### Search the docs

Looking for something specific? The Assistant pulls answers from this site, the API reference, and the community forum.

<button type="button" class="button secondary" data-action="search" data-icon="magnifying-glass">Search...</button>
{% endcolumn %}
{% endcolumns %}
