---
icon: file-magnifying-glass
description: How Evolve confirms a government-issued ID is genuine, valid, and matches the customer.
---

# Document review

The document-review check is the first half of an identity verification. It looks at the photo of a government-issued ID — passport, driver's license, or national ID card — and decides whether it's real, current, and matches what the customer typed in.

## What's checked

Every document goes through five separate sub-checks:

| Sub-check | What it does |
| --- | --- |
| **Authenticity** | Compares the document against a database of templates for that country and type. Flags photoshopped documents, fake templates, and known forgery patterns. |
| **Expiry** | Reads the expiry date and rejects expired documents. |
| **Tampering** | Pixel-level analysis for image manipulation — re-glued laminates, replaced photos, edited text. |
| **MRZ / barcode parity** | For documents with machine-readable zones or PDF417 barcodes, confirms the printed data matches the encoded data. |
| **Data extraction** | Pulls the name, date of birth, document number, and expiry. Returns this on the verification result. |

The result is a per-sub-check pass/fail, plus an overall confidence score. The overall decision uses your strictness setting (see [Identity verification](README.md#configurable-strictness)).

## Supported documents

| Document type | Coverage |
| --- | --- |
| **Passport** | Every country except the OFAC-blocked list (~190 countries). |
| **Driver's license** | All 50 US states + DC, all Canadian provinces, all EU/EEA countries, UK, Australia, NZ, Japan. |
| **National ID card** | EU/EEA, UK, Singapore, Hong Kong, India (Aadhaar), and ~40 others. |
| **Residence permit** | EU/EEA, UK, US, Canada — for non-citizen residents. |

The full list is in **Settings → Identity → Supported documents**, with a search by country.

## What the customer sees

The hosted flow walks them through the capture:

{% stepper %}
{% step %}

### Pick country and type

A dropdown of countries (defaulted to the customer's IP-inferred country), then a list of document types valid for that country. If they don't have any of the listed documents, they can pick "Other" and the verification will land in manual review.

{% endstep %}

{% step %}

### Front capture

The camera opens with an outline overlay. Real-time feedback tells them when the document is in frame, in focus, and well-lit. Glare and motion blur are detected before submission.

{% endstep %}

{% step %}

### Back capture (if needed)

Driver's licenses and national ID cards typically have data on the back (barcode, magnetic stripe). Passports don't. Evolve only prompts for back capture when needed for the document type.

{% endstep %}
{% endstepper %}

The whole document phase typically takes 30–45 seconds.

## Failure reasons

When document review fails, the reason on the timeline tells you why:

<details>

<summary>document_expired</summary>

The document's expiry date is in the past. The customer needs to provide a current document — they can retry with one if they have one.

</details>

<details>

<summary>document_tampered</summary>

Pixel analysis detected manipulation — usually a replaced photo or edited text. This is treated as a fraud signal; the customer is locked out of retries until you (or Evolve's manual reviewers) approve another attempt.

</details>

<details>

<summary>document_unrecognized</summary>

The document doesn't match any template in our database. Most often this is a partial capture (the camera missed an edge), but it can also be an unsupported document type the customer didn't realize was unsupported. Retries usually succeed once the customer recaptures.

</details>

<details>

<summary>data_mismatch</summary>

The data extracted from the document doesn't match what the customer typed in (typically a different name spelling). The customer can correct their input and retry.

</details>

## Reviewing failed verifications

Failed verifications appear in **Identity → Sessions → Failed**. Each one shows the document image, the per-sub-check result, and the extracted data. If you believe a verification was incorrectly failed, you can submit it for human re-review with one click — it goes to Evolve's reviewer team and typically resolves within an hour.

## Privacy and storage

Documents are encrypted at rest with per-tenant keys and retained per your [retention policy](../../compliance/data-retention.md) (default: 30 days). They're never used for training Evolve's models without explicit, per-account opt-in.

## Related

* [Selfie and liveness](selfie-and-liveness.md) — the second half of identity verification.
* [Identity verification](README.md) — the parent flow.
* [Audit logs](../../compliance/audit-logs.md) — every document review is logged.
