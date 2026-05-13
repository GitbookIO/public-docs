---
icon: graduation-cap
description: Step-by-step builds for common Evolve workflows.
cover: .gitbook/assets/tutorials-cover.png
coverY: 0
layout:
  width: wide
  tableOfContents:
    visible: false
---

# Tutorials

{% columns %}
{% column width="50%" %}
Hands-on walkthroughs for the workflows we get the most questions about. Each tutorial follows the same structure — short intro, video walkthrough, stepper with the actual build, common pitfalls, and pointers to what's next.

**Looking for conceptual material?** The product spaces — [Payments](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/), [Identity](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/), [Connect](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/) — cover the underlying mechanics and dashboard workflows. Tutorials cover end-to-end builds that combine multiple features.
{% endcolumn %}

{% column width="50%" %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

Every tutorial in this section uses the same **content template** — frontmatter, intro, prerequisites hint, video embed, stepper, common-pitfalls expandables, what's-next cards. That consistency is intentional: it makes the structure scannable for repeat readers, and easier for the team to author new ones.

The blocks demoed across these pages: **stepper**, **tabs** (multi-language code samples), **expandable**, **embed** (the YouTube video), **hint**, and **cards**.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

## Build common payment flows

Practical end-to-end builds for the things every payments team needs early.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-cart-shopping" style="color:$primary;">:cart-shopping:</i></h3></td><td><strong>Accept a one-time payment with Checkout</strong></td><td>From zero to a real charge in under an hour.</td><td><a href="payment-flows/accept-one-time-payment.md">accept-one-time-payment.md</a></td></tr><tr><td><h3><i class="fa-arrows-rotate" style="color:$primary;">:arrows-rotate:</i></h3></td><td><strong>Build a subscription billing system</strong></td><td>Recurring billing with mandates, retries, dunning.</td><td><a href="payment-flows/subscription-billing.md">subscription-billing.md</a></td></tr><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>Set up 3-D Secure for high-value charges</strong></td><td>Liability shift on the transactions where it matters most.</td><td><a href="payment-flows/3d-secure.md">3d-secure.md</a></td></tr><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><strong>Save cards for repeat customers</strong></td><td>Network tokens, mandates, account updater.</td><td><a href="payment-flows/save-cards.md">save-cards.md</a></td></tr><tr><td><h3><i class="fa-arrows-left-right" style="color:$primary;">:arrows-left-right:</i></h3></td><td><strong>Migrate from Stripe</strong></td><td>Field-by-field cutover plan and parallel-run pattern.</td><td><a href="payment-flows/migrate-from-stripe.md">migrate-from-stripe.md</a></td></tr><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Build a chargeback-prevention checklist</strong></td><td>The handful of habits that cut dispute rates by half.</td><td><a href="payment-flows/chargeback-prevention.md">chargeback-prevention.md</a></td></tr></tbody></table>

## Verify customers and businesses

End-to-end Identity flows tied to product use cases.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-id-card" style="color:$primary;">:id-card:</i></h3></td><td><strong>Add identity verification to sign-up</strong></td><td>Document + selfie wired into your onboarding form.</td><td><a href="verification/identity-on-signup.md">identity-on-signup.md</a></td></tr><tr><td><h3><i class="fa-briefcase" style="color:$primary;">:briefcase:</i></h3></td><td><strong>Verify a business (KYB)</strong></td><td>Beneficial-ownership collection plus sanctions screening.</td><td><a href="verification/kyb.md">kyb.md</a></td></tr><tr><td><h3><i class="fa-building-columns" style="color:$primary;">:building-columns:</i></h3></td><td><strong>Connect a bank account with Plaid</strong></td><td>Instant verification with micro-deposit fallback.</td><td><a href="verification/plaid-bank-verification.md">plaid-bank-verification.md</a></td></tr><tr><td><h3><i class="fa-rotate-right" style="color:$primary;">:rotate-right:</i></h3></td><td><strong>Build a re-verification trigger</strong></td><td>Re-verify on chargebacks, large transactions, and account changes.</td><td><a href="verification/re-verification-trigger.md">re-verification-trigger.md</a></td></tr></tbody></table>

## Run a marketplace with Connect

Platform and marketplace patterns. Heaviest on Connect, with reaches into Identity and Payments.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-user-plus" style="color:$primary;">:user-plus:</i></h3></td><td><strong>Onboard your first sellers</strong></td><td>Hosted-onboarding-flow walkthrough end to end.</td><td><a href="marketplace/onboard-sellers.md">onboard-sellers.md</a></td></tr><tr><td><h3><i class="fa-percent" style="color:$primary;">:percent:</i></h3></td><td><strong>Split each payment with application fees</strong></td><td>Flat percentages, conditional rules, pass-through fees.</td><td><a href="marketplace/split-payments.md">split-payments.md</a></td></tr><tr><td><h3><i class="fa-money-bill-transfer" style="color:$primary;">:money-bill-transfer:</i></h3></td><td><strong>Configure per-seller payout schedules</strong></td><td>Daily, weekly, monthly, and on-demand.</td><td><a href="marketplace/payout-schedules.md">payout-schedules.md</a></td></tr><tr><td><h3><i class="fa-gavel" style="color:$primary;">:gavel:</i></h3></td><td><strong>Handle disputes and refunds at scale</strong></td><td>Routing per-seller, evidence collection, policy automation.</td><td><a href="marketplace/disputes-at-scale.md">disputes-at-scale.md</a></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>Build a custom Connect onboarding flow</strong></td><td>Programmatic onboarding for teams that want their own UX.</td><td><a href="marketplace/custom-onboarding.md">custom-onboarding.md</a></td></tr></tbody></table>

## Get help

{% columns %}
{% column width="50%" %}

### Talk to support

For account-specific questions, integration help, or production incidents, open a ticket from the dashboard.

<p><a href="https://gitbook.com" class="button primary">Open a ticket</a></p>

{% endcolumn %}

{% column width="50%" %}

### Search the docs

Looking for something specific? The Assistant pulls answers from this site, the API reference, and the community forum.

<p><button type="button" class="button secondary" data-action="search" data-icon="magnifying-glass">Search...</button></p>

{% endcolumn %}
{% endcolumns %}
