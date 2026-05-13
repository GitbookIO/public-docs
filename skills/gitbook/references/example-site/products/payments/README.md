---
description: Route, reconcile, and report on every payment.
icon: credit-card
cover: .gitbook/assets/payments-cover.png
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

# Payments

{% columns %}
{% column %}
Evolve Payments handles the work between a customer's "pay" click and the money landing in your account — card and bank-rail processing, network routing, 3-D Secure, settlement, and reporting. This space covers everything from the first test charge to enterprise routing rules.

<button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">Ask the Evolve docs</button>

<button type="button" class="button secondary" data-action="ask" data-query="How do I accept my first payment?" data-icon="rocket">First payment</button> <button type="button" class="button secondary" data-action="ask" data-query="When do I need 3-D Secure?" data-icon="shield-halved">3-D Secure</button> <button type="button" class="button secondary" data-action="ask" data-query="How do I route around card declines?" data-icon="route">Smart routing</button>
{% endcolumn %}

{% column %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

This space is the deepest in the demo and shows off three GitBook features: **adaptive content** (hints and entire blocks change with the visitor), **space variables** (URLs and constants pulled from `vars.yaml`), and **synced blocks** (the test/live environments table is reused across all three product spaces).

{% if !visitor.claims.unsigned.persona %}
Try a persona to see adaptive content in action across the site:

<a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="seedling">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona %}
<i class="fa-id-card-clip" style="color:$info;">:id-card-clip:</i> You are currently <code class="expression">visitor.claims.unsigned.persona === "prospect" ? "a prospect user exploring the product" : visitor.claims.unsigned.persona === "new" ? "a new user" : visitor.claims.unsigned.persona === "existing" ? "an existing user" : visitor.claims.unsigned.persona === "partner" ? "a partner" : ""</code><code class="expression">visitor.claims.unsigned.plan ? " on the " + visitor.claims.unsigned.plan.charAt(0).toUpperCase() + visitor.claims.unsigned.plan.slice(1) + " plan" : ""</code>. [<mark style="color:$primary;">Reset</mark>](https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=)
{% endif %}

{% if visitor.claims.unsigned.persona === "prospect" %}
<a class="button primary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a class="button primary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=partner&#x26;plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a class="button primary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=new&#x26;plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/payments?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a class="button primary" data-icon="handshake-angle">Partner</a>
{% endif %}
{% endhint %}


{% endcolumn %}
{% endcolumns %}





***



## <i class="fa-sparkle" style="color:$info;">:sparkle:</i> Picked for you

{% if visitor.claims.unsigned.persona === "prospect" %}
{% hint style="info" icon="store" %}
**Evaluating Evolve?** Get up and running with Payments with the resources below.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><h3><strong>Accept your first payment</strong></h3></td><td>Take your first test payment in five minutes.</td></tr><tr><td><h3><i class="fa-receipt" style="color:$primary;">:receipt:</i></h3></td><td><h3><strong>Fees and pricing</strong></h3></td><td>What each plan costs, what's included, and how fees show up in your settlements.</td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
{% hint style="info" icon="hand-wave" %}
**New to Evolve Payments?** The dashboard works on its own — get a real test charge in five minutes, no code required.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><h3><strong>Accept your first payment</strong></h3></td><td>Take your first test payment in five minutes — no integration required.</td><td><a href="quickstart/accept-your-first-payment.md">accept-your-first-payment</a></td></tr><tr><td><h3><i class="fa-flask" style="color:$primary;">:flask:</i></h3></td><td><h3><strong>Test mode and live mode</strong></h3></td><td>What changes when you flip from test to live, and the cutover checklist.</td><td><a href="quickstart/test-and-live-mode.md">test-and-live-mode</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
{% hint style="info" icon="arrows-left-right" %}
**Migrating from Stripe?** Most APIs map cleanly. Start with the migration guide and the saved-method patterns.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-arrows-left-right" style="color:$primary;">:arrows-left-right:</i></h3></td><td><h3><strong>Migrate from Stripe</strong></h3></td><td>Field mapping, parallel-run pattern, and the cutover checklist.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/migrate-from-stripe">migrate-from-stripe</a></td></tr><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><h3><strong>Save cards for repeat customers</strong></h3></td><td>How Stripe's Customer/PaymentMethod model maps to Evolve.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/save-cards">save-cards</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
{% hint style="info" icon="building" %}
**Setting up enterprise features?** Smart routing, failover, and same-day payouts are the highest-leverage Enterprise capabilities.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-route" style="color:$primary;">:route:</i></h3></td><td><h3><strong>Smart routing</strong></h3></td><td>Per-network success-rate optimization. 1–3% lift in approval rate.</td><td><a href="accept-payments/smart-routing.md">smart-routing</a></td></tr><tr><td><h3><i class="fa-arrows-spin" style="color:$primary;">:arrows-spin:</i></h3></td><td><h3><strong>Failover and retries</strong></h3></td><td>Stay up when an acquirer or network goes down.</td><td><a href="accept-payments/failover.md">failover</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona %}
***
{% endif %}

{% if !visitor.claims.unsigned.persona %}
## Get started
{% endif %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><strong>Quickstart</strong></td><td>Take your first test payment in five minutes.</td><td><a href="quickstart/accept-your-first-payment.md">accept-your-first-payment.md</a></td></tr><tr><td><h3><i class="fa-book-open" style="color:$primary;">:book-open:</i></h3></td><td><strong>Concepts</strong></td><td>How payments move through Evolve.</td><td><a href="concepts/payment-lifecycle.md">payment-lifecycle.md</a></td></tr><tr><td><h3><i class="fa-bolt" style="color:$primary;">:bolt:</i></h3></td><td><strong>Accept payments</strong></td><td>Charges, saved methods, 3-D Secure, routing.</td><td><a href="accept-payments/">accept-payments</a></td></tr><tr><td><h3><i class="fa-scale-balanced" style="color:$primary;">:scale-balanced:</i></h3></td><td><strong>Reconciliation</strong></td><td>Settlement files, refunds, disputes.</td><td><a href="reconciliation/">reconciliation</a></td></tr><tr><td><h3><i class="fa-chart-line" style="color:$primary;">:chart-line:</i></h3></td><td><strong>Reporting</strong></td><td>Daily reports, exports, and finance pushes.</td><td><a href="reporting/">reporting</a></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>API reference</strong></td><td>Endpoints, SDKs, and try-it.</td><td><a href="https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api/">payments-api</a></td></tr></tbody></table>



## What's new

The biggest recent shipments — see the full [changelog](https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/ErQsbFsgm6eg9BApdmPl/) for the back-catalog.

* **Smart routing v2** — per-network success-rate optimization, available on Growth and Enterprise. [Read more](accept-payments/smart-routing.md).
* **Same-day payouts** — opt-in for Enterprise customers in the US. [Read more](concepts/money-movement.md).
* **Disputes API** — programmatic evidence submission, replacing the legacy CSV upload. [Read more](reconciliation/disputes.md).

## Get help

{% columns %}
{% column width="50%" %}
#### Talk to support

For account-specific questions, billing, or production incidents, contact your account team or open a ticket from the dashboard.

<a href="https://gitbook.com" class="button primary">Open a ticket</a>
{% endcolumn %}

{% column width="50%" %}
#### Search the docs

Looking for something specific? The Assistant pulls answers from this site, the API reference, and the community forum.

<button type="button" class="button secondary" data-action="search" data-icon="magnifying-glass">Search...</button>
{% endcolumn %}
{% endcolumns %}
