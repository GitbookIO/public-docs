---
icon: clock-rotate-left
description: How long Evolve keeps verification PII, why, and how to change the policy.
---

# Data retention

Identity verification produces sensitive PII — government ID images, selfies, bank account numbers, beneficial owner records. The shorter you can hold it, the smaller your privacy footprint. The longer you hold it, the easier it is to satisfy auditors and regulators when something gets questioned later.

The right retention window is a balance between the two, tuned to the regulatory regime you operate in. Evolve gives you the controls; the policy is yours to set.

## Default retention

Out of the box, Evolve retains verification PII as follows:

| Data type | Default retention |
| --- | --- |
| Document images (front and back) | <code class="expression">space.vars.verification_ttl_days</code> days |
| Selfie images | <code class="expression">space.vars.verification_ttl_days</code> days |
| Extracted document data (name, DOB, document number) | 7 years |
| Selfie liveness scores | 7 years |
| Sanctions and PEP screening results | 7 years |
| Bank account numbers (encrypted) | 7 years |
| Audit log entries | 7 years (see [Audit logs](audit-logs.md)) |

The pattern: the **raw images** purge quickly (default 30 days), the **extracted data and decisions** stick around for the regulatory floor.

## Why these defaults

* **30-day raw images** is short enough to minimize PII exposure but long enough that customer-support edge cases can still review the original capture if a verification is contested.
* **7-year extracted data** matches the BSA/AML floor in the US and most EU regimes. It means a regulator asking "show me the verifications you ran in 2023" will have the metadata to answer, even though the images themselves are long gone.
* **7-year audit logs** is the same regulatory floor — and protects your team's ability to demonstrate due process if a decision is later questioned.

## Configuring retention

In **Settings → Identity → Retention**, you can set per-data-type retention windows:

| Setting | Range | Default |
| --- | --- | --- |
| Document images | 1 day to 7 years | 30 days |
| Selfie images | 1 day to 7 years | 30 days |
| Extracted data | 1 year to 10 years | 7 years |
| Audit logs | 7 years (locked) | 7 years |

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="info" %}
**Enterprise-specific:** you can also configure per-region retention to match local rules (e.g. shorter retention for EU residents under GDPR, longer for regulated US verticals). Set these under **Settings → Identity → Regional retention**.
{% endhint %}

{% endif %}

Changes apply going forward; existing data is purged on its existing schedule unless you trigger a one-time backfill.

## Customer deletion requests

GDPR, CCPA, and most modern privacy regimes give individuals the right to request deletion of their data. Evolve supports this:

{% stepper %}
{% step %}

### Customer requests deletion

The customer asks you (via your support channel or a privacy portal you operate) to delete their data.

{% endstep %}

{% step %}

### You issue the deletion

In the dashboard, find the verification or customer and click **Delete data**. You can also issue deletions in bulk via the API for privacy-portal automations.

{% endstep %}

{% step %}

### Evolve purges within 30 days

PII is purged from active and backup systems within 30 days. The audit log retains the deletion event itself, but the PII it references becomes a placeholder.

{% endstep %}
{% endstepper %}

{% hint style="warning" %}
**Some data can't be deleted on request.** If a verification is required by law to be retained (e.g. a sanctions match that triggered a regulatory filing), you cannot delete it — and the customer can't compel you to. The dashboard surfaces these "cannot delete" cases with the legal basis for retention.
{% endhint %}

## What gets purged when

When the retention window for a data type expires, Evolve's purge process runs nightly to:

1. **Identify expired data** — anything past its retention window.
2. **Anonymize references** — log entries pointing to the data update to "purged per retention policy."
3. **Delete from active systems** — the encrypted blob is removed from primary storage.
4. **Delete from backups** — backups containing the data are themselves purged on a 90-day rolling window. Until that, the data is recoverable only by Evolve operations staff under documented break-glass procedures.

The dashboard's **Compliance → Retention** page shows what's been purged in the last 90 days, so you can see the policy operating.

## Encryption at rest

While data is retained, it's encrypted with per-tenant keys (KMS-managed). Even within Evolve, document images and PII are not accessible without specific authorization tied to a request id. Evolve operations staff cannot routinely browse customer data; access is by exception, logged, and time-limited.

For Enterprise customers, you can supply your own KMS keys (BYOK) so encryption depends on a key you control. This is configured in **Settings → Security → Encryption keys**.

## Related

* [Audit logs](audit-logs.md) — what's kept indefinitely (or near-indefinitely) for accountability.
* [Regional requirements](regional-requirements.md) — region-specific retention floors and ceilings.
* [Identity verification](../verification-flows/identity-verification/README.md) — the source of most retained data.
