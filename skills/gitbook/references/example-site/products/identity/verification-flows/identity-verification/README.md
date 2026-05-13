---
icon: id-card
description: Verify an individual customer with a government-issued document and a live selfie.
---

# Identity verification

Identity verification is Evolve's flow for confirming that a person is who they say they are. It runs two checks together — a **document review** of a government-issued ID, and a **selfie liveness check** that matches the photo on the document to a live capture of the customer's face.

For most consumer-facing products this is the only verification you need. For higher-risk products and Enterprise customers, an optional **watchlist screening** check can be layered on top.

## What the customer experiences

The hosted flow takes 60–90 seconds end to end, on average:

{% stepper %}
{% step %}

### Pick a country and document

The customer picks the country that issued their ID and the document type. Evolve supports passports, driver's licenses, and national ID cards in <code class="expression">space.vars.document_supported_countries</code> countries.

{% endstep %}

{% step %}

### Capture the document

The flow opens the camera and walks the customer through capturing the front (and back, where required). Glare and blur detection give live feedback so the captures are usable.

{% endstep %}

{% step %}

### Capture a selfie

A 3-second passive liveness capture. The customer holds the camera in front of them; no head turns or specific gestures required.

{% endstep %}

{% step %}

### Decision

The result lands in your dashboard within seconds — Verified, Failed, or (in a small fraction of cases) Manual review.

{% endstep %}
{% endstepper %}

## The checks

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-file-magnifying-glass" style="color:$primary;">:file-magnifying-glass:</i></h3></td><td><strong>Document review</strong></td><td>Authenticity, expiry, tampering, and data extraction.</td><td><a href="document-review.md">document-review.md</a></td></tr><tr><td><h3><i class="fa-face-smile" style="color:$primary;">:face-smile:</i></h3></td><td><strong>Selfie and liveness</strong></td><td>Confirms the person matches the document.</td><td><a href="selfie-and-liveness.md">selfie-and-liveness.md</a></td></tr></tbody></table>

## Decisions and reasons

Every verification ends in one of three outcomes. The reason is on the timeline:

| Outcome | What it means | Common reasons |
| --- | --- | --- |
| **Verified** | All checks passed; you can trust the identity. | — |
| **Failed** | One or more checks failed; the identity is not trusted. | `document_expired`, `document_tampered`, `selfie_mismatch`, `liveness_failed` |
| **Manual review** | An edge case Evolve isn't confident about. A human reviewer (yours or ours) gets a second look. | `low_confidence_match`, `document_partially_obscured` |

Manual review typically resolves within an hour during business hours, longer overnight. You can configure who reviews — your team, Evolve's review team, or both — in **Settings → Identity → Manual review**.

## Configurable strictness

You can tune how strict each check is in **Settings → Identity → Strictness**. Three presets cover most cases:

* **Standard** (default) — balanced for consumer onboarding. Used by most teams.
* **Strict** — tighter thresholds, more manual reviews. Right for higher-risk products like crypto, gambling, or pharmacy.
* **Permissive** — looser thresholds, fewer manual reviews. Right for low-stakes flows like creator platforms or community products.

You can also build custom rules — e.g. "Strict for transactions over $1,000, Standard otherwise" — in the same settings panel.

## Re-running for the same customer

If a customer's first attempt fails, you can let them retry. By default, each customer gets up to 3 attempts within a 24-hour window before being locked out. The retry policy is in **Settings → Identity → Retry policy**.

A separate **re-verification** API lets you re-run the full flow against an existing customer at any later point — for example, after a chargeback or before a high-value transaction.

## Related

* [Document review](document-review.md) — how Evolve authenticates the document.
* [Selfie and liveness](selfie-and-liveness.md) — the biometric match.
* [Watchlist screening](watchlist-screening.md) — optional Enterprise screening layer.
* [Compliance → Audit logs](../../compliance/audit-logs.md) — every decision is logged.
