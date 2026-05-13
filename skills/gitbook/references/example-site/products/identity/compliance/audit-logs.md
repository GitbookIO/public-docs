---
icon: clipboard-list
description: Every verification, decision, and override is logged — searchable, exportable, immutable.
---

# Audit logs

Every action Evolve takes on your behalf — and every action your team takes in the dashboard — is recorded in the audit log. It's the artifact your auditor, your bank, or your regulator will ask for first when something needs to be explained.

Logs are append-only. You can't edit or delete an entry; even Evolve's own staff can't.

## What's logged

Every entry includes the **what**, the **who**, the **when**, and the **why**. The full schema:

| Field | Description | Example |
| --- | --- | --- |
| `event` | The action taken | `verification.completed` |
| `actor_type` | What kind of entity acted | `evolve_system`, `team_member`, `customer`, `api_client` |
| `actor_id` | Who exactly | `user_3K2pL9q`, `cust_a8N3mF` |
| `subject_type` | What was acted on | `verification_session`, `customer`, `business` |
| `subject_id` | Specifically | `vs_3KsM12pL9qXa7` |
| `timestamp` | When | `2026-04-30T14:22:01.341Z` |
| `metadata` | Action-specific details | `{ "reason": "manual_override", "note": "false positive..." }` |
| `request_id` | The request that triggered the entry | `req_8h2nF6m4Lp` |

## Categories of event

The events that show up most often, grouped by what they're about:

<details>

<summary>Verification events</summary>

* `verification.created` — a new session was created (by API or dashboard)
* `verification.completed` — final decision reached
* `verification.failed` — explicit failure, with reason
* `verification.manually_reviewed` — a human reviewer made the call
* `verification.overridden` — a team member changed the automated decision
* `verification.expired` — the session timed out before completion

</details>

<details>

<summary>Document events</summary>

* `document.uploaded`
* `document.reviewed`
* `document.flagged_for_tampering`
* `document.deleted` — per retention policy or manual deletion

</details>

<details>

<summary>Screening events</summary>

* `screening.run`
* `screening.match_found`
* `screening.match_overridden` — false-positive override, with required reason
* `screening.match_added` — ongoing monitoring detected a new match

</details>

<details>

<summary>Configuration events</summary>

* `settings.changed` — any change to a workspace setting
* `team.member_added` / `team.member_removed`
* `permissions.changed`
* `api_key.created` / `api_key.revoked` / `api_key.rolled`

</details>

<details>

<summary>Data access events</summary>

* `pii.accessed` — when a team member views a verification's PII
* `pii.exported` — when PII is included in a CSV or report download
* `pii.deleted` — manual or scheduled deletion

</details>

## Searching the log

In **Compliance → Audit log**, you can filter by:

* **Date range** (down to the second)
* **Event type** (any of the events above)
* **Actor** (specific team member, system, or customer)
* **Subject** (a specific verification, customer, or business)
* **Free text** in the metadata

The default view shows the last 30 days; you can go back as far as your retention policy allows.

## Exporting

Three ways to get the log out:

* **CSV download** from the dashboard, with current filters applied.
* **Scheduled export** to SFTP, S3, or your data warehouse — same destinations as [Payments reporting](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reporting/sharing-exports).
* **API pull** for real-time integration into a SIEM (Splunk, Datadog, etc.).

For SOC 2 and ISO 27001 audit support, the standard scheduled export — full log, daily, in CSV, to your auditor's SFTP — is the most common setup.

## Retention

Audit log entries are retained for **7 years by default** — long enough for most regulatory regimes (BSA/AML in the US is 5 years; many EU regimes are 5–10 years). You can configure a longer retention if you need it; you can't configure a shorter one for the action log itself, since that would defeat the audit trail's purpose.

PII referenced in the log (specific document images, selfie images) follows your [data retention policy](data-retention.md), separately from the log entry itself. After PII is purged, log entries that referenced it remain — they just point to a "purged per retention policy" placeholder instead of the original data.

## Tamper-evidence

The log is append-only and hashed: every entry's hash includes the previous entry's hash, forming a Merkle-style chain. Evolve's internal infrastructure cannot insert a backdated entry without breaking the chain.

For Enterprise customers, the daily root hash is published to a public timestamp service, so you can prove the log existed in its current form at a specific date. This is overkill for most teams but matters for highly regulated verticals.

## Permissions

Audit log access is gated by role:

| Role | Can see |
| --- | --- |
| Viewer | Aggregate counts only |
| Compliance | Full log, including PII access events |
| Admin | Full log, plus permission to schedule exports |

The dashboard surfaces "who looked at what" — every PII view is itself an audit log entry, visible to your compliance team.

## Related

* [Data retention](data-retention.md) — how long PII is kept; logs persist longer.
* [Regional requirements](regional-requirements.md) — what regulators require to be in the log.
* [Payments / Reporting](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reporting/sharing-exports) — schedule the same kind of export.
