---
icon: building
description: Multi-subsidiary journal entries, custom segment mapping, multi-currency reconciliation.
---

# NetSuite

The Evolve NetSuite integration is the heavier-duty cousin of [QuickBooks](../quickbooks/README.md) — designed for multi-subsidiary, multi-currency, NetSuite-customized accounting setups. It runs as a SuiteApp installed in your NetSuite environment, with daily journal entries posted from Evolve.

This is for Enterprise and large Growth customers. Setup takes a NetSuite administrator about 4 hours; ongoing maintenance is minimal.

## What it does

* **Daily journal entries** with full NetSuite custom-field mapping (departments, classes, locations, custom segments).
* **Multi-subsidiary support** — different Evolve accounts (or different `metadata.subsidiary_id` values) post to different NetSuite subsidiaries.
* **Multi-currency** with NetSuite's native FX gain/loss accounting.
* **Customer sync** with bidirectional updates between Evolve customers and NetSuite Entities.
* **SuiteScript hooks** — for teams with custom logic, the bundle exposes events your scripts can react to.

## Install the SuiteApp

{% stepper %}
{% step %}

### Get the bundle ID

In Evolve, **Settings → Integrations → NetSuite → Setup** shows your unique bundle ID. Copy it.

{% endstep %}

{% step %}

### Install in NetSuite

In NetSuite, **Customization → SuiteBundler → Search & Install Bundles**. Paste the bundle ID and install. The bundle adds:

* Custom record types: `Evolve Settlement`, `Evolve Charge`, `Evolve Refund`.
* Custom fields on Customer and Subsidiary.
* Saved searches for reconciliation.
* Daily scheduled scripts that pull from Evolve.

{% endstep %}

{% step %}

### Authenticate

Generate a TBA (Token-Based Authentication) token in NetSuite under **Setup → Users/Roles → Access Tokens**. Paste the consumer key, consumer secret, token, and token secret into the Evolve dashboard.

For SAML-SSO environments, use NetSuite's OAuth 2.0 flow instead — supported on Evolve Enterprise.

{% endstep %}

{% step %}

### Map subsidiaries

If you operate multiple NetSuite subsidiaries, map each Evolve account (or metadata-tagged subsidiary) to a NetSuite subsidiary in the bundle's setup screen. See [Custom field mapping](custom-field-mapping.md) for the multi-subsidiary patterns.

{% endstep %}

{% step %}

### Run the first sync

The bundle's daily scheduled script runs at 7am in your NetSuite account's timezone. To run an immediate first sync, click **Sync now** in the bundle's setup screen. It backfills the last 30 days of settlements by default.

Verify the journal entries in NetSuite. Most NetSuite admins involve their accountant to confirm the first three days of entries before letting it run unattended.

{% endstep %}
{% endstepper %}

## Multi-subsidiary mapping

Three patterns most teams use:

| Pattern | Setup |
| --- | --- |
| **One Evolve account per subsidiary** | Each subsidiary has its own Evolve account; the bundle maps account → subsidiary 1:1. Simplest. |
| **Single Evolve account, metadata-tagged** | One Evolve account; every charge has `metadata.subsidiary_id`. The bundle reads the metadata and posts to the right subsidiary. |
| **Routing rules** | One Evolve account; charges are routed to subsidiaries based on configurable rules (currency, country, product line). |

The choice depends on your NetSuite OneWorld setup. Most platforms with truly separate subsidiaries (different legal entities, different banks) use Pattern 1. Single-entity multi-divisional companies use Pattern 2 or 3.

## Custom segments

NetSuite's custom segments (departments, classes, locations, custom-defined) are exposed in the bundle's mapping screen. Tag each Evolve metadata key with the corresponding NetSuite segment, and journal entries get the right segment values automatically. Full mapping reference on [Custom field mapping](custom-field-mapping.md).

## Customer sync

Bidirectional. New Evolve customers can sync to NetSuite Entities; updated NetSuite Entities can sync back to Evolve customer records. Most teams enable one direction (typically Evolve → NetSuite) and disable the reverse to avoid sync loops.

For matching existing customers, the bundle uses email as the default key. For B2B with shared contact emails, you can switch to a tax-ID match instead.

## Last reviewed

Reviewed in early 2026. NetSuite bundle releases happen quarterly; release notes go through [change requests on the docs repo](https://github.com/GitbookIO/evolve-demo).

## Related

* [Custom field mapping](custom-field-mapping.md) — the deeper mapping options.
* [QuickBooks integration](../quickbooks/README.md) — for non-NetSuite teams.
* [Settlement files](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reconciliation/settlement-files) — the source data.
