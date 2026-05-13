---
description: Product updates across Payments, Identity, Connect, and the platform.
icon: clock-rotate-left
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: false
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Changelog

{% columns %}
{% column width="50%" %}
Everything we've shipped across Evolve in the last six months. Filter by product tag using the controls in the top right of the timeline.

New entries land roughly weekly. Subscribe via [RSS](https://gitbook.com) or follow [@evolvepay](https://gitbook.com) for major releases.
{% endcolumn %}

{% column width="50%" %}
{% hint style="success" icon="gitbook" %}
**A note from GitBook**

This page is a single **Updates block** — a timeline of dated entries with **tags** (defined in `.gitbook/tags.yaml`). The four tags here are `payments`, `identity`, `connect`, `platform`; multi-tagged entries get all their tags. **RSS** is auto-generated for the page.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

{% updates format="full" %}
{% update date="2026-04-29" tags="payments" %}
## Smart routing v2

Per-network success-rate optimization is now generally available on Growth and Enterprise. Most teams see a 1–3% lift in approval rate on cards that previously routed through a single acquirer.

The new model picks acquirers based on per-card-type historical approval rates, network token availability, and transaction shape — and falls back to a secondary acquirer on soft declines without the customer noticing.

Smart routing is on by default for accounts where it's eligible. To opt out or customize routing rules, see **Settings → Routing**.
{% endupdate %}

{% update date="2026-04-22" tags="identity" %}
## Selfie liveness 2.0

Passive liveness — no head turns, no smile-on-command, no spelling out numbers. The customer just holds the camera in front of their face for about three seconds.

Completion rates are up \~12% in our beta cohort, with a small drop in fraud-detection rate that we've offset by tighter document-tampering checks. Active rollout to all accounts over the next two weeks.
{% endupdate %}

{% update date="2026-04-18" tags="identity" %}
## Plaid instant for businesses

Bank account verification on connected accounts now uses Plaid's business-bank integration where supported. Same one-tap UX as the consumer flow, with verified business owner names checked against the connected account's beneficial owners.
{% endupdate %}

{% update date="2026-04-12" tags="connect" %}
## Per-seller subdomains

Enterprise platforms can now route per-seller checkout to a custom subdomain (`acme.checkout.evolve.com`). Useful for marketplaces with strong-brand sellers who want their checkout URL to match their brand. Configure in **Connect → Branding → Per-seller overrides**.
{% endupdate %}

{% update date="2026-04-05" tags="platform" %}
## Audit log export to S3 and GCS

Push your audit log to S3 or Google Cloud Storage on a schedule. Useful for SIEM ingestion (Splunk, Datadog) and long-term retention beyond our 7-year built-in window.
{% endupdate %}

{% update date="2026-04-01" tags="payments,platform" %}
## Payments API v3-beta available

A preview of the next major version of the Payments API. Highlights:

* `Charge` is renamed to `Payment` (`pay_*` IDs).
* `capture: true|false` is replaced by a `capture_method` enum: `automatic`, `manual`, `automatic_async`.
* Authorization window extended from 7 to 30 days.
* Multi-currency capture — authorize in one currency, capture in another.

v3-beta is preview-only. Don't run production traffic on it without coordinating with your account team. v2 stays the stable default; v3-beta will graduate when we've completed the beta-customer cohort.

The variant dropdown in [Developers](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api/) lets you flip between v1, v2, and v3 to compare.
{% endupdate %}

{% update date="2026-03-26" tags="connect" %}
## Application fees report improvements

The platform-revenue report under **Reports → Application fees** now supports per-seller cohort breakdowns and CSV export with full metadata. Useful for daily revenue reconciliation.
{% endupdate %}

{% update date="2026-03-21" tags="payments" %}
## Same-day payouts (Enterprise)

US Enterprise accounts can now opt in to same-day payouts for an additional 0.4% per transfer. Funds land in your bank account within hours rather than the next business day. Configure in **Settings → Payouts**.

For platforms running Connect, same-day payouts are also available per-seller.
{% endupdate %}

{% update date="2026-03-14" tags="identity" %}
## KYB in 12 new countries

Business verification now covers Argentina, Brazil, Chile, Colombia, India, Indonesia, Malaysia, Mexico, Peru, Philippines, Thailand, Vietnam — all with national-register integrations and local sanctions screening.
{% endupdate %}

{% update date="2026-03-07" tags="platform" %}
## Datadog APM integration

Drop-in OpenTelemetry support in all four official SDKs. Trace spans from your application code through Evolve's edge in your Datadog APM views. Off by default; enable with `EVOLVE_OTEL_ENABLED=true`.
{% endupdate %}

{% update date="2026-03-01" tags="payments" %}
## Disputes API generally available

Programmatic evidence submission is now GA, replacing the legacy CSV upload. The new API supports up to 10 file attachments per dispute, structured evidence fields per reason code, and pre-emptive refunds via Verifi/Ethoca alerts (Enterprise).
{% endupdate %}

{% update date="2026-02-26" tags="connect" %}
## Bulk seller onboarding via CSV

Migrating from another platform? Upload a CSV of seller info under **Connect → Seller bulk import**. Evolve generates per-seller hosted onboarding URLs you can email out from your side.
{% endupdate %}

{% update date="2026-02-19" tags="identity" %}
## Adverse media screening

Watchlist screening now includes an adverse-media category — news mentions tying a verified identity to specific risk topics (financial crime, terrorism, sanctions evasion). Available on Enterprise. Most teams treat adverse-media matches as manual-review triggers rather than automatic rejection — the false-positive rate is non-trivial.
{% endupdate %}

{% update date="2026-02-14" tags="platform" %}
## SCIM provisioning

Auto-provision team members from your IdP (Okta, Microsoft Entra ID, OneLogin, others). Configure under **Settings → Security → SCIM**. Available on Growth and Enterprise.
{% endupdate %}

{% update date="2026-02-08" tags="payments" %}
## Refund window extended on Enterprise

Enterprise accounts can now refund a charge up to 180 days after capture, up from 90 on Growth. Useful for slow-fulfillment goods and B2B with longer reconciliation cycles.
{% endupdate %}

{% update date="2026-02-03" tags="connect" %}
## Failover for international acquirers

Enterprise platforms with sellers in multiple regions now have failover support for the EU and UK acquirers as well as US. Configure per-region routing under **Settings → Routing → Failover**.
{% endupdate %}

{% update date="2026-01-31" tags="platform" %}
## New dashboard search

The dashboard's global search now returns ranked results across customers, charges, payouts, verification sessions, and connected accounts, with relevance based on your team's recent searches and your role's data scope.
{% endupdate %}

{% update date="2026-01-25" tags="identity" %}
## Re-verification webhook improvements

The `verification_session.reverification_required` event now includes the trigger reason (`chargeback`, `large_transaction`, `address_change`, `scheduled`) so your handler can route to different downstream flows.
{% endupdate %}

{% update date="2026-01-22" tags="payments" %}
## Multi-currency capture preview

Authorize in one currency, capture in another at the daily wholesale rate plus your configured FX margin. Available in v3-beta. Useful for marketplaces with international sellers — authorize in the buyer's currency, pay out in the seller's.
{% endupdate %}

{% update date="2026-01-17" tags="connect" %}
## Embedded checkout customization

Enterprise platforms can now customize the embedded checkout's font, layout, and CSS. Per-seller font and CSS overrides also supported. Configure under **Connect → Branding**.
{% endupdate %}

{% update date="2026-01-12" tags="platform" %}
## SDK v2 — Node, Python, Go, Ruby

The 2.x lines of all four official SDKs are now stable, tracking the v2 Payments API. Highlights:

* Auto-generated idempotency keys on every write call (configurable).
* Auto-retries with exponential backoff on transient errors.
* Built-in webhook signature verification.
* Native async support in Node and Python.
* Strict module boundaries in Go (per-resource packages).

The 1.x lines are still maintained for the v1 Payments API; they reach end-of-life when v1 sunsets on 2026-12-31. See [Developers / SDKs](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/sdks).
{% endupdate %}

{% update date="2026-01-08" tags="identity" %}
## Document support in 12 new countries

Driver's-license and national-ID-card support added for Bangladesh, Egypt, Ghana, Kenya, Morocco, Nigeria, Pakistan, Saudi Arabia, South Africa, Tunisia, UAE, and Vietnam. Brings supported document countries to 195.
{% endupdate %}

{% update date="2026-01-05" tags="payments" %}
## Improved decline-code messages

The `message` field on declined charges is now consistent across all SDKs (previously varied by SDK locale). The `code` and `decline_code` fields are unchanged — build your error handling around those rather than the message text.
{% endupdate %}

{% update date="2025-12-19" tags="platform" %}
## Year-end maintenance window

A scheduled 30-minute maintenance window on December 23, 02:00 UTC. No expected downtime; a brief reduction in async processing capacity. See [<code class="expression">space.vars.status_page</code>](https://gitbook.com) for live updates.
{% endupdate %}

{% update date="2025-12-15" tags="connect" %}
## On-demand payouts (Enterprise)

Enterprise platforms can now offer their sellers an on-demand payout button — instant cash to the seller's bank for a 1% fee. Configure in **Connect → Settings → Instant payouts**.
{% endupdate %}

{% update date="2025-12-09" tags="payments" %}
## Disputes API beta

Beta release of the new disputes API ahead of GA in March. Sign up for the beta cohort under **Settings → Beta features**.
{% endupdate %}

{% update date="2025-12-04" tags="identity" %}
## Manual review queue improvements

The manual review queue now supports bulk actions, saved filters, and per-reviewer assignment. Useful for compliance teams handling more than 50 reviews/week.
{% endupdate %}

{% update date="2025-12-01" tags="platform" %}
## SOC 2 Type II report — 2025

Our 2025 SOC 2 Type II audit completed with no exceptions. Report is available under NDA from your account team. ISO 27001 recertification is also complete; PCI-DSS Level 1 attestation expected mid-January.
{% endupdate %}

{% update date="2025-11-26" tags="connect" %}
## Application fees report

A new daily/weekly/monthly aggregate report under **Reports → Application fees**, showing platform revenue, take rate, and per-seller fee earnings. Exportable to CSV and the standard scheduled-export destinations.
{% endupdate %}

{% update date="2025-11-21" tags="payments" %}
## 3-D Secure 2.2 support

Updated 3DS-2 implementation to spec version 2.2 across all card networks. Better browser-fingerprinting accuracy improves the frictionless-flow rate by \~5%.
{% endupdate %}

{% update date="2025-11-15" tags="identity" %}
## Bank verification fallback improvements

When Plaid instant fails (e.g. unsupported bank), the flow now falls back to micro-deposits seamlessly within the same hosted session — no separate session creation needed.
{% endupdate %}

{% update date="2025-11-10" tags="platform" %}
## SDK telemetry

Anonymous SDK usage telemetry (version, request shape, error class) is now collected by default to help us catch regressions. Disable with `EVOLVE_TELEMETRY=off`. No request bodies, no PII, no card data.
{% endupdate %}

{% update date="2025-11-04" tags="payments" %}
## Saved payment methods improvements

The `setup_future_usage` field on Checkout sessions now supports `on_session` (one-tap reuse) in addition to `off_session` (recurring). Better mandate handling reduces friction on the network's side, with about a 0.7% lift in repeat-purchase approval rates.
{% endupdate %}
{% endupdates %}

## Older releases

For releases before November 2025, the [archive](https://gitbook.com) covers the prior 24 months. Major releases are also tagged on our [GitHub repo](https://github.com/GitbookIO/evolve-demo) for the SDK side.

For platform incidents and maintenance windows, the [status page](https://gitbook.com) maintains a separate incident log.
