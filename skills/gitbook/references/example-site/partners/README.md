---
icon: handshake
description: Build your business on Evolve. Partner with us to deliver payments, identity, and platform solutions to your customers.
cover: .gitbook/assets/partners-cover.png
coverY: 0
layout:
  width: wide
  tableOfContents:
    visible: false
---

{% hint style="success" icon="gitbook" %}
**A note from GitBook**

This space demonstrates the public/authenticated **flip**: anonymous visitors see the partner pitch below; authenticated partners see a portal home in the same place. The flip is driven by adaptive content on `visitor.claims.unsigned.persona`. Once you flip into partner mode, the linked portal pages (deal registration, marketing resources, etc.) become accessible — they're **hidden pages**, not in the public sidebar nav, but reachable via direct link or from the portal home.

{% if visitor.claims.unsigned.persona === "partner" %}
<i class="fa-id-card-clip" style="color:$info;">:id-card-clip:</i> You are currently signed in as a partner<code class="expression">visitor.claims.unsigned.plan ? " on the " + visitor.claims.unsigned.plan.charAt(0).toUpperCase() + visitor.claims.unsigned.plan.slice(1) + " plan" : ""</code>. [<mark style="color:$primary;">Reset</mark>](https://enterprise-demos.gitbook.io/evolve-docs/partners?visitor.persona=)
{% endif %}

{% if visitor.claims.unsigned.persona !== "partner" %}
<a class="button primary" data-icon="globe">Public</a> <a href="https://enterprise-demos.gitbook.io/evolve-docs/partners?visitor.persona=partner&#x26;visitor.plan=enterprise" class="button secondary" data-icon="handshake-angle">Signed-in partner</a>
{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}
<a href="https://enterprise-demos.gitbook.io/evolve-docs/partners?visitor.persona=" class="button secondary" data-icon="globe">Public</a> <a class="button primary" data-icon="handshake-angle">Signed-in partner</a>
{% endif %}
{% endhint %}

{% if visitor.claims.unsigned.persona !== "partner" %}

# Partner with Evolve

Whether you build software for businesses, implement payments for clients, or operate a marketplace platform, Evolve has a partner program that fits — with revenue share, co-marketing, and dedicated support.

<p><a href="https://gitbook.com" class="button primary">Apply to become a partner</a> <a href="https://gitbook.com" class="button secondary">Sign in to the partner portal</a></p>

## Why partner with Evolve

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-percent" style="color:$primary;">:percent:</i></h3></td><td><strong>Revenue share</strong></td><td>Earn a share of every transaction your referrals process — for the lifetime of the relationship.</td><td></td></tr><tr><td><h3><i class="fa-headset" style="color:$primary;">:headset:</i></h3></td><td><strong>Dedicated support</strong></td><td>Direct line to a partner success manager. Slack channel for technical escalation.</td><td></td></tr><tr><td><h3><i class="fa-bullhorn" style="color:$primary;">:bullhorn:</i></h3></td><td><strong>Co-marketing</strong></td><td>Joint case studies, conference appearances, and curated lead lists for active partners.</td><td></td></tr></tbody></table>

## Partner types

{% columns %}
{% column width="33%" %}

### <i class="fa-cubes" style="color:$primary;">:cubes:</i> Solution Partners

You build software that integrates Evolve — checkout plugins, marketplace platforms, vertical SaaS. Earn revenue share on every customer who uses your integration.

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-screwdriver-wrench" style="color:$primary;">:screwdriver-wrench:</i> Implementation Partners

You implement Evolve for clients. Earn referral fees on every client you bring on, plus access to our certified-implementer program for marketing visibility.

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-circle-nodes" style="color:$primary;">:circle-nodes:</i> Technology Partners

You build a complementary product (CRM, analytics, fraud detection). Get listed in our [integrations directory](https://app.gitbook.com/s/MBT3EDUK7DzXmR0k9cje/) and access early-look APIs.

{% endcolumn %}
{% endcolumns %}

## What partners are saying

{% columns %}
{% column width="50%" %}

> "We integrated Evolve into our marketplace platform last year. The revenue share covers 40% of our infrastructure costs now — and our customers' approval rates went up 2.3% on average."
>
> **— Maria Chen, CTO, Stride Commerce**

{% endcolumn %}

{% column width="50%" %}

> "We're a regional implementation shop and Evolve's partner program is the most generous we've seen. Their team actually returns calls — that's worth more than the rev share."
>
> **— Devon Reilly, Reilly Payments Group**

{% endcolumn %}
{% endcolumns %}

## How the program works

{% stepper %}
{% step %}

### Apply

Tell us about your business. Most applications get a response within 5 business days; technology partners typically clear faster than implementation partners since the diligence is lighter.

{% endstep %}

{% step %}

### Onboarding

Once approved, you get portal access, an assigned partner success manager, and a 30-minute kickoff call. We walk through portal tools and answer your specific integration or sales questions.

{% endstep %}

{% step %}

### Refer or build

Solution and Technology partners build their integration; Implementation partners start referring clients. Either way, every transaction tracked to you earns revenue share.

{% endstep %}

{% step %}

### Grow

Quarterly reviews with your partner success manager — what's working, what to invest in, what new features matter to your customers.

{% endstep %}
{% endstepper %}

## Frequently asked questions

<details>

<summary>Is there a fee to join the program?</summary>

No. Evolve doesn't charge any application fee or annual membership. Revenue share is paid out on a quarterly basis based on referred-customer activity.

</details>

<details>

<summary>Do I need to be Evolve-certified?</summary>

For Implementation Partners, certification is required to use the "Certified Evolve Implementer" badge — but optional otherwise. Certification is free; it's a 4-hour online course plus a final exam. See the partner portal for details.

</details>

<details>

<summary>What about exclusivity?</summary>

Non-exclusive. Most of our partners work with multiple payment providers; we'd rather earn the right to be your preferred option than contract our way to it.

</details>

<details>

<summary>How is revenue share calculated?</summary>

A percentage of net Evolve revenue from referred customers — typically 10–25% depending on partner tier and customer commitment. Specifics are in your partner agreement.

</details>

## Apply

<p><a href="https://gitbook.com" class="button primary">Start your application</a> <a href="mailto:partners@evolve.com" class="button secondary">Email the partner team</a></p>

{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}

# Partner Portal

Welcome back. Here's what's new and where to find what you need.

<p><a href="deal-registration.md" class="button primary">Register a new deal</a> <a href="https://gitbook.com" class="button secondary">Open partner Slack</a></p>

## Quick links

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-handshake-angle" style="color:$primary;">:handshake-angle:</i></h3></td><td><strong>Deal registration</strong></td><td>Register an opportunity, track deal status, see protection windows.</td><td><a href="deal-registration.md">deal-registration.md</a></td></tr><tr><td><h3><i class="fa-bullhorn" style="color:$primary;">:bullhorn:</i></h3></td><td><strong>Marketing resources</strong></td><td>Logos, brand kit, case studies, co-marketing templates.</td><td><a href="marketing-resources.md">marketing-resources.md</a></td></tr><tr><td><h3><i class="fa-graduation-cap" style="color:$primary;">:graduation-cap:</i></h3></td><td><strong>Training</strong></td><td>Certification programs, sales enablement, technical deep-dives.</td><td><a href="training.md">training.md</a></td></tr><tr><td><h3><i class="fa-headset" style="color:$primary;">:headset:</i></h3></td><td><strong>Partner support</strong></td><td>Direct line to your partner success manager. Escalation paths.</td><td><a href="support.md">support.md</a></td></tr></tbody></table>

## Recent updates

{% updates format="full" %}

{% update date="2026-04-25" %}
## Q2 partner kit refresh

Updated logo guidelines, brand kit, and three new case studies (Stride Commerce, Reilly Payments Group, Northwind SaaS) live in [Marketing resources](marketing-resources.md).
{% endupdate %}

{% update date="2026-04-10" %}
## New deal-registration UI

The deal-registration form is now mobile-friendly, supports multi-stakeholder fields, and shows real-time deal status. [Try it](deal-registration.md).
{% endupdate %}

{% update date="2026-03-22" %}
## Spring partner summit recordings

Recordings from the March summit (keynote, technical sessions, Q&A) are in [Training → Recordings](training.md#recordings).
{% endupdate %}

{% endupdates %}

## Need help?

{% columns %}
{% column width="50%" %}

### <i class="fa-headset" style="color:$primary;">:headset:</i> Your partner success manager

Direct line to the person on our team who knows your account.

<p><a href="support.md" class="button secondary">Contact details</a></p>

{% endcolumn %}

{% column width="50%" %}

### <i class="fa-comments" style="color:$primary;">:comments:</i> Partner Slack

Technical and sales discussion with other Evolve partners and our team.

<p><a href="https://gitbook.com" class="button secondary">Open Slack</a></p>

{% endcolumn %}
{% endcolumns %}

{% endif %}
