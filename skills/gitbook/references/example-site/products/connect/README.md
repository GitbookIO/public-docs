---
icon: circles-overlap
description: Embed payments in your platform — accept money on behalf of your sellers, take a cut, and pay them out.
cover: .gitbook/assets/connect-cover.png
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

# Connect

{% columns %}
{% column %}
Evolve Connect is the platform layer of Evolve Payments. If you operate a marketplace, a SaaS that takes payments on behalf of customers, or a vertical platform with embedded financial services, Connect handles the parts that get hard at the platform scale: onboarding sellers, splitting each payment, paying them out, and managing refunds and disputes across many accounts.

<button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">Ask the Evolve docs</button>

<button type="button" class="button secondary" data-action="ask" data-query="How do I onboard my first seller?" data-icon="user-plus">First seller</button> <button type="button" class="button secondary" data-action="ask" data-query="How do application fees work?" data-icon="percent">Application fees</button> <button type="button" class="button secondary" data-action="ask" data-query="Hosted vs embedded checkout?" data-icon="window-maximize">Hosted vs embedded</button>
{% endcolumn %}

{% column %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

This space demonstrates **synced blocks reused from Payments** — the test/live environments table on [Test mode and live mode](quickstart/test-and-live-mode.md) is the same block used in the Payments and Identity spaces.

{% if !visitor.claims.unsigned.persona %}
Try a persona to see adaptive content in action across the site:

<a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=new&#x26;visitor.plan=growth" class="button secondary" data-icon="seedling">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona %}
<i class="fa-id-card-clip" style="color:$info;">:id-card-clip:</i> You are currently <code class="expression">visitor.claims.unsigned.persona === "prospect" ? "a prospect user exploring the product" : visitor.claims.unsigned.persona === "new" ? "a new user" : visitor.claims.unsigned.persona === "existing" ? "an existing user" : visitor.claims.unsigned.persona === "partner" ? "a partner" : ""</code><code class="expression">visitor.claims.unsigned.plan ? " on the " + visitor.claims.unsigned.plan.charAt(0).toUpperCase() + visitor.claims.unsigned.plan.slice(1) + " plan" : ""</code>. [<mark style="color:$primary;">Reset</mark>](https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=)
{% endif %}

{% if visitor.claims.unsigned.persona === "prospect" %}
<a class="button primary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=new&#x26;visitor.plan=growth" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a class="button primary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=new&#x26;visitor.plan=growth" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a class="button primary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=new&#x26;visitor.plan=growth" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/connect?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a class="button primary" data-icon="handshake-angle">Partner</a>
{% endif %}
{% endhint %}
{% endcolumn %}
{% endcolumns %}

***

## <i class="fa-sparkle" style="color:$info;">:sparkle:</i> Picked for you

{% if visitor.claims.unsigned.persona === "prospect" %}
{% hint style="info" icon="store" %}
**Evaluating Connect for your platform?** The basics of how the buyer/seller/platform money flow works.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-circles-overlap" style="color:$primary;">:circles-overlap:</i></h3></td><td><h3><strong>How Connect fits</strong></h3></td><td>Buyer, seller, platform — and the money flow between them.</td><td><a href="README.md">connect</a></td></tr><tr><td><h3><i class="fa-percent" style="color:$primary;">:percent:</i></h3></td><td><strong>Splitting payments</strong></td><td>Application fees, flat fees, conditional rules.</td><td><a href="platform-setup/splitting-payments.md">splitting-payments</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
{% hint style="info" icon="hand-wave" %}
**New to Connect?** Onboard your first test seller in five minutes.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><h3><strong>Onboard your first seller</strong></h3></td><td>End-to-end walkthrough — connected account, hosted onboarding, first transfer.</td><td><a href="quickstart/onboard-your-first-seller.md">onboard-your-first-seller</a></td></tr><tr><td><h3><i class="fa-window-maximize" style="color:$primary;">:window-maximize:</i></h3></td><td><strong>Pick a checkout shape</strong></td><td>Hosted, embedded, or fully custom buyer experience.</td><td><a href="embedded-checkout/hosted-vs-embedded.md">hosted-vs-embedded</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
{% hint style="info" icon="arrows-left-right" %}
**Coming from Stripe Connect?** Connected accounts, application fees, and transfers all work the same. Account types are unified.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-arrows-left-right" style="color:$primary;">:arrows-left-right:</i></h3></td><td><h3><strong>Migrate from Stripe</strong></h3></td><td>The full cutover plan, including Connect-specifics.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/migrate-from-stripe">migrate-from-stripe</a></td></tr><tr><td><h3><i class="fa-user-plus" style="color:$primary;">:user-plus:</i></h3></td><td><strong>Onboarding sellers</strong></td><td>The unified account model that replaces Express/Standard/Custom.</td><td><a href="platform-setup/onboarding-sellers.md">onboarding-sellers</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
{% hint style="info" icon="building" %}
**Building a custom platform?** White-label embedded checkout, custom seller onboarding, consolidated KYC are Enterprise capabilities.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><h3><strong>Custom Connect onboarding</strong></h3></td><td>Programmatic onboarding for teams that want their own UX.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/marketplace/custom-onboarding">custom-onboarding</a></td></tr><tr><td><h3><i class="fa-paint-roller" style="color:$primary;">:paint-roller:</i></h3></td><td><strong>White-label checkout</strong></td><td>Per-seller domains, fonts, custom CSS for premium sellers.</td><td><a href="embedded-checkout/customization.md">customization</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona %}
***
{% endif %}

{% if !visitor.claims.unsigned.persona %}
## Get started
{% endif %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><strong>Quickstart</strong></td><td>Onboard your first seller in five minutes.</td><td><a href="quickstart/onboard-your-first-seller.md">onboard-your-first-seller</a></td></tr><tr><td><h3><i class="fa-window-maximize" style="color:$primary;">:window-maximize:</i></h3></td><td><strong>Embedded checkout</strong></td><td>The buyer-facing flow — hosted, embedded, or fully custom.</td><td><a href="embedded-checkout/README.md">embedded-checkout</a></td></tr><tr><td><h3><i class="fa-sliders" style="color:$primary;">:sliders:</i></h3></td><td><strong>Platform setup</strong></td><td>Onboarding, splitting, payouts, and dispute handling.</td><td><a href="platform-setup/README.md">platform-setup</a></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>API reference</strong></td><td>Endpoints, SDKs, and try-it.</td><td><a href="https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/connect-api/">connect-api</a></td></tr></tbody></table>

## Where Connect fits

A typical Connect transaction touches three parties — the **buyer**, the **seller** (your customer), and **you** (the platform). Connect orchestrates the money so each one ends up with the right amount.

{% columns %}
{% column width="33%" %}

### <i class="fa-cart-shopping" style="color:$primary;">:cart-shopping:</i> Buyer

Pays once, sees one charge on their statement (yours or the seller's, your choice). Refunds and support flow back through your platform.

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-store" style="color:$primary;">:store:</i> Seller

Onboarded once via your platform, then receives payouts on a schedule you set. Their identity, banking, and tax records are handled by [Identity](https://enterprise-demos.gitbook.io/evolve-docs/identity).

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-circles-overlap" style="color:$primary;">:circles-overlap:</i> Platform

Takes a percentage of each transaction as an application fee, plus optional flat fees. Sees consolidated reporting across all sellers in one dashboard.

{% endcolumn %}
{% endcolumns %}

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
