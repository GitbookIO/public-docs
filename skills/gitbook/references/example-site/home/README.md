---
description: >-
  Payments, identity, and platform infrastructure — built for businesses that
  scale.
icon: house
cover: .gitbook/assets/home-cover.png
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
    visible: false
  outline:
    visible: false
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Welcome to Evolve

{% columns %}
{% column width="50%" %}
Take payments, verify customers, and run a marketplace — all on one platform. Evolve is the financial infrastructure for modern businesses, used by thousands of teams from early-stage startups to global enterprises.

<button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">Ask the Evolve docs</button>

<button type="button" class="button secondary" data-action="ask" data-query="How do I take my first payment?" data-icon="rocket">First payment</button> <button type="button" class="button secondary" data-action="ask" data-query="How do I verify a customer&#x27;s identity?" data-icon="id-card">Verification</button> <button type="button" class="button secondary" data-action="ask" data-query="How do I onboard sellers on a marketplace?" data-icon="circles-overlap">Marketplace</button>
{% endcolumn %}

{% column width="50%" %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

This site is a demo of GitBook's enterprise features applied to a fictional fintech, **Evolve**. It shows what a real customer-facing docs site looks like end-to-end — adaptive content, OpenAPI variants, the AI Assistant with Connections, change-request workflows, hidden pages with public/authenticated flips, and more.

{% if !visitor.claims.unsigned.persona %}
Try a persona to see adaptive content in action across the site:

<a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="seedling">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona %}
<i class="fa-id-card-clip" style="color:$info;">:id-card-clip:</i> You are currently <code class="expression">visitor.claims.unsigned.persona === "prospect" ? "a prospect user exploring the product" : visitor.claims.unsigned.persona === "new" ? "a new user" : visitor.claims.unsigned.persona === "existing" ? "an existing user" : visitor.claims.unsigned.persona === "partner" ? "a partner" : ""</code><code class="expression">visitor.claims.unsigned.plan ? " on the " + visitor.claims.unsigned.plan.charAt(0).toUpperCase() + visitor.claims.unsigned.plan.slice(1) + " plan" : ""</code>. [<mark style="color:$primary;">Reset</mark>](https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=)
{% endif %}

{% if visitor.claims.unsigned.persona === "prospect" %}
<a class="button primary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a class="button primary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=partner&#x26;plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=new&#x26;visitor.plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a class="button primary" data-icon="rocket">Migrator</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=prospect" class="button secondary" data-icon="bag-shopping">Prospect</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=new&#x26;plan=starter" class="button secondary" data-icon="arrow-right-to-bracket">New user</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=existing&#x26;visitor.plan=growth" class="button secondary" data-icon="rocket">Migrator</a> <a class="button primary" data-icon="handshake-angle">Partner</a>
{% endif %}
{% endhint %}
{% endcolumn %}
{% endcolumns %}



{% if visitor.claims.unsigned.persona %}
***

# <i class="fa-sparkle" style="color:$info;">:sparkle:</i> Picked for you
{% endif %}

{% if visitor.claims.unsigned.persona === "prospect" %}
{% hint style="info" icon="store" %}
**Evaluating Evolve?** Use the resources below to get an overview of how to get started.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-wallet" style="color:$primary;">:wallet:</i></h3></td><td><h3><strong>Payment methods</strong></h3></td><td>Which payment methods Evolve supports, and which ones are available on each plan.</td><td><a href="https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/payment-methods">Payment methods</a></td></tr><tr><td><h3><i class="fa-life-ring" style="color:$primary;">:life-ring:</i></h3></td><td><h3><strong>Help Center</strong></h3></td><td>Frequently-asked questions about pricing, going live, and supported countries</td><td><a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/NA4Ikc8fQtsXC5U53xJu/">Troubleshooting</a></td></tr><tr><td><h3><i class="fa-receipt" style="color:$primary;">:receipt:</i></h3></td><td><h3><strong>Fees and pricing</strong></h3></td><td>What each plan costs, what's included, and how fees show up in your settlements.</td><td><a href="https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/concepts/fees-and-pricing">Fees and pricing</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "new" %}
{% hint style="info" icon="hand-wave" %}
**Welcome to Evolve.** Start with these — get to a working test charge fast, then explore the things every new account does first.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-rocket" style="color:$primary;">:rocket:</i></h3></td><td><h3><strong>Take your first payment</strong></h3></td><td>Five-minute test charge from the dashboard. No integration required.</td><td><a href="https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/quickstart/accept-your-first-payment">accept-your-first-payment</a></td></tr><tr><td><h3><i class="fa-key" style="color:$primary;">:key:</i></h3></td><td><h3><strong>Developer Quickstart</strong></h3></td><td>The same flow with a real API call, in Node, Python, Go, or Ruby.</td><td><a href="https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/quickstart">quickstart</a></td></tr><tr><td><h3><i class="fa-graduation-cap" style="color:$primary;">:graduation-cap:</i></h3></td><td><h3><strong>Tutorials</strong></h3></td><td>15 step-by-step builds for the most-asked-about workflows.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/">tutorials</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "existing" %}
{% hint style="info" icon="arrows-left-right" %}
**Migrating from Stripe?** Most concepts map cleanly. Start with the migration tutorial — most teams complete in 2–6 weeks of calendar time.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-arrows-left-right" style="color:$primary;">:arrows-left-right:</i></h3></td><td><h3><strong>Migrate from Stripe</strong></h3></td><td>Field mapping, parallel-run pattern, and the cutover checklist.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/migrate-from-stripe">migrate-from-stripe</a></td></tr><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><h3><strong>Save cards for repeat customers</strong></h3></td><td>Network tokens, mandates, account updater — and how Stripe Customers map.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/save-cards">save-cards</a></td></tr><tr><td><h3><i class="fa-arrows-rotate" style="color:$primary;">:arrows-rotate:</i></h3></td><td><h3><strong>Subscription billing</strong></h3></td><td>Recurring billing, mandates, retries, dunning — direct port from Stripe Subscriptions.</td><td><a href="https://app.gitbook.com/s/Nankrp40VchJsUblU6h6/payment-flows/subscription-billing">subscription-billing</a></td></tr></tbody></table>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
{% hint style="info" icon="handshake" %}
**Welcome back.** Your portal has deal registration, marketing assets, training, and a direct line to your partner success manager.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-handshake-angle" style="color:$primary;">:handshake-angle:</i></h3></td><td><h3><strong>Register a deal</strong></h3></td><td>Protect your commission. Status, protection windows, payout timing.</td><td><a href="https://app.gitbook.com/s/R0VawBV5xcQ4exP2PlWS/deal-registration">deal-registration</a></td></tr><tr><td><h3><i class="fa-bullhorn" style="color:$primary;">:bullhorn:</i></h3></td><td><h3><strong>Marketing resources</strong></h3></td><td>Logos, brand kit, case studies, co-marketing programs.</td><td><a href="https://app.gitbook.com/s/R0VawBV5xcQ4exP2PlWS/marketing-resources">marketing-resources</a></td></tr><tr><td><h3><i class="fa-graduation-cap" style="color:$primary;">:graduation-cap:</i></h3></td><td><h3><strong>Training</strong></h3></td><td>Three certifications, self-paced courses, monthly live sessions.</td><td><a href="https://app.gitbook.com/s/R0VawBV5xcQ4exP2PlWS/training">training</a></td></tr></tbody></table>
{% endif %}





***



## Three products, one platform

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-credit-card" style="color:$primary;">:credit-card:</i></h3></td><td><h3><strong>Payments</strong></h3></td><td>Accept card and bank-rail payments. Smart routing, 3-D Secure, settlement, reporting.</td><td><a href="https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/">payments</a></td></tr><tr><td><h3><i class="fa-id-card" style="color:$primary;">:id-card:</i></h3></td><td><h3><strong>Identity</strong></h3></td><td>Verify customers and businesses. Document review, selfie liveness, bank verification, KYB.</td><td><a href="https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/">identity</a></td></tr><tr><td><h3><i class="fa-circles-overlap" style="color:$primary;">:circles-overlap:</i></h3></td><td><h3><strong>Connect</strong></h3></td><td>Embed payments in your platform. Onboard sellers, split payments, run a marketplace.</td><td><a href="https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/">connect</a></td></tr></tbody></table>

## For developers

API references, SDKs, and the agent integrations across all three products. Pick where to dive in:

{% columns %}
{% column width="25%" %}
<i class="fa-rocket" style="color:$primary;">:rocket:</i> **Quickstart**

Make your first API call in five minutes.

<a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/Si95BtOt1VRLWjT7A67V/" class="button primary">Quickstart</a>
{% endcolumn %}

{% column width="25%" %}
<i class="fa-key" style="color:$primary;">:key:</i> **Authentication**

Keys, restricted scopes, signature verification.

<a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/Si95BtOt1VRLWjT7A67V/" class="button secondary">Authenticated</a>
{% endcolumn %}

{% column width="25%" %}
<i class="fa-cubes" style="color:$primary;">:cubes:</i> **SDKs**

Node, Python, Go, Ruby — official and idiomatic.

<a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/Si95BtOt1VRLWjT7A67V/" class="button secondary">SDKs</a>
{% endcolumn %}

{% column width="25%" %}
<i class="fa-robot" style="color:$primary;">:robot:</i> **AI agents**

llms.txt, MCP server, agent best practices.

<a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/Si95BtOt1VRLWjT7A67V/" class="button secondary">For AI agents</a>
{% endcolumn %}
{% endcolumns %}

## Learn and explore

{% columns %}
{% column width="66.66666666666666%" %}
#### <i class="fa-compass" style="color:$primary;">:compass:</i> Guides

Everything you need to get the most out of the Evolve platform.

<details open>

<summary><i class="fa-graduation-cap" style="color:$primary;">:graduation-cap:</i> <strong>Tutorials</strong></summary>

Step-by-step builds for common workflows. 15 tutorials with video walkthroughs.

<a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/Nankrp40VchJsUblU6h6/" class="button secondary">Start building</a>

</details>

<details open>

<summary><i class="fa-graduation-cap" style="color:$primary;">:graduation-cap:</i> <strong>Help Center</strong></summary>

Focused answers to common questions. The Assistant pulls from here, the forum, and YouTube.

<button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">How can we help?</button><a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/NA4Ikc8fQtsXC5U53xJu/" class="button secondary">View all</a>

</details>

<details open>

<summary><i class="fa-puzzle-piece" style="color:$primary;">:puzzle-piece:</i> <strong>Integration guides</strong></summary>

Slack, Zapier, Segment, QuickBooks, NetSuite — and more in active development.

<a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/MBT3EDUK7DzXmR0k9cje/" class="button secondary">Browse integrations</a>

</details>
{% endcolumn %}

{% column width="33.33333333333334%" %}
### <i class="fa-clock-rotate-left">:clock-rotate-left:</i> What's new

Our biggest recent releases

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-route" style="color:$primary;">:route:</i></h3></td><td><h3><strong>Smart routing v2</strong></h3></td><td>Per-network success-rate optimization. 1–3% lift in approval rate, no code changes.</td><td><a href="#smart-routing-v2">Broken link</a></td></tr><tr><td><h3><i class="fa-flask" style="color:$primary;">:flask:</i></h3></td><td><h3><strong>Payments API v3-beta</strong></h3></td><td>Renamed Payment object, capture_method enum, 30-day auth, multi-currency capture.</td><td><a href="#payments-api-v3-beta-available">Broken link</a></td></tr><tr><td><h3><i class="fa-face-smile" style="color:$primary;">:face-smile:</i></h3></td><td><h3><strong>Selfie liveness 2.0</strong></h3></td><td>Passive liveness — no head turns. Lifts completion rates by ~12%.</td><td><a href="#selfie-liveness-2.0">Broken link</a></td></tr></tbody></table>

<a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/ErQsbFsgm6eg9BApdmPl/" class="button secondary" data-icon="clock-rotate-left">View complete changelog</a>
{% endcolumn %}
{% endcolumns %}

***

## Partner with Evolve

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><h3><i class="fa-handshake" style="color:$primary;">:handshake:</i> <strong>Become a partner</strong></h3></td><td>Solution, implementation, and technology partners earn revenue share, get co-marketing support, and a direct line to your partner success manager.</td><td><a href="https://gitbook.com/enterprise" class="button primary">Apply to the program</a> <a href="https://app.gitbook.com/o/2DnmWBpytIOUKeXExonU/s/R0VawBV5xcQ4exP2PlWS/" class="button secondary">Learn more</a></td></tr><tr><td><h3><i class="fa-key" style="color:$primary;">:key:</i> <strong>Already a partner?</strong></h3></td><td>Sign in to the partner portal for deal registration, marketing resources, training, and support.</td><td><a href="https://enterprise-demos.gitbook.io/evolve-docs?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button primary">Sign in</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/partners?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary">Open the portal</a></td></tr></tbody></table>

## Get help

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><h3><i class="fa-headset" style="color:$primary;">:headset:</i> <strong>Talk to support</strong></h3></td><td>For account-specific questions, integration help, or production incidents, open a ticket by starting a chat below.</td><td><button type="button" class="button primary" data-action="ask" data-icon="gitbook-assistant">How can we help?</button></td></tr><tr><td><h3><i class="fa-circle-check" style="color:$primary;">:circle-check:</i> <strong>Platform status</strong></h3></td><td>Real-time status of every Evolve service. Subscribe via email or RSS for incident updates.</td><td><a href="https://gitbook.com" class="button secondary">View status</a></td></tr><tr><td><h3><i class="fa-comments" style="color:$primary;">:comments:</i> <strong>Community</strong></h3></td><td>Real-time discussion with other Evolve customers and our team. Most product questions have a thread.</td><td><a href="https://gitbook.com" class="button secondary">Join the forum</a></td></tr></tbody></table>
