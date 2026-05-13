---
icon: calculator
description: Auto-create journal entries from each settlement. QuickBooks Online and Desktop.
---

# QuickBooks

The Evolve QuickBooks integration writes journal entries to your QuickBooks file each day, mapping settlement-file line items to your chart of accounts. Most teams set it up once at month-end-close-time and let it run unattended.

Two flavors:

* **QuickBooks Online** — direct OAuth integration, real-time sync.
* **QuickBooks Desktop** — IIF file export with daily download or SFTP delivery. Manual import into Desktop.

## What it does

* For each daily settlement file, generate a journal entry in QuickBooks with:
  * Revenue (gross from charges) → your revenue account.
  * Processing fees → your fees account.
  * Refunds → reduce revenue.
  * Disputes (lost) → bad-debt expense.
  * Net to bank → your Evolve clearing account → bank account.
* Sync customer records (optional) so QuickBooks knows about Evolve customers.
* Provide a daily reconciliation report you can sign off on.

## Connect QuickBooks Online

{% stepper %}
{% step %}

### Authorize the app

In Evolve, **Settings → Integrations → QuickBooks → Connect**. You'll be redirected to QuickBooks Online to authorize. Pick the company file and approve.

{% endstep %}

{% step %}

### Map your accounts

The mapping page asks for one QuickBooks account per Evolve line type. Defaults are:

| Evolve line | QuickBooks account |
| --- | --- |
| Charge revenue | Sales Income |
| Processing fees | Bank Charges |
| Refunds | Returns and Allowances |
| Dispute losses | Bad Debt Expense |
| Evolve clearing | Other Current Asset (create if needed) |

You can override any of these to match your chart of accounts. See [Reconciliation mapping](reconciliation-mapping.md) for the deeper mapping options.

{% endstep %}

{% step %}

### Pick a sync schedule

Three options:

* **After each settlement** — journal entry posts to QB within minutes of the settlement file. Most teams use this.
* **Daily batch** — all entries for the prior day post at 8am local time.
* **On-demand** — entries queue up; you click **Sync now** to post.

{% endstep %}

{% step %}

### Verify the first sync

After the first settlement, check the journal entry in QuickBooks. Most teams have their accountant verify the first three days of entries before letting it run unattended. The Evolve dashboard shows a sync log under **Settings → Integrations → QuickBooks → History**.

{% endstep %}
{% endstepper %}

## Connect QuickBooks Desktop

QuickBooks Desktop doesn't have an OAuth API, so the integration uses an IIF file:

1. **Settings → Integrations → QuickBooks → Desktop → Configure**.
2. Pick the same account mapping as above.
3. Choose delivery method — daily email, SFTP push, or manual download from the dashboard.
4. In QuickBooks Desktop, import each day's IIF file. Most accounting teams script this with a Windows scheduled task.

For QuickBooks Desktop on a network with security restrictions, the SFTP-push option is the cleanest — Evolve pushes to your file server, your network does the rest.

## Customer sync

Optional. When enabled, Evolve customer records flow to QuickBooks Customer records on creation. Useful when your accountant needs per-customer revenue tracking inside QuickBooks (not just per-day aggregates).

Disable this if your QuickBooks file is already populated by your CRM — you'd end up with duplicates.

## Multi-currency

QuickBooks Online supports multi-currency on its higher-tier plans. Evolve's integration auto-detects whether your QB file has multi-currency enabled:

* **Multi-currency on** — each currency settles to its own clearing account; QB handles the FX gain/loss accounting.
* **Multi-currency off** — Evolve converts to your home currency at the daily mid-rate before posting, with the FX margin booked as a fee.

For Connect platforms with international sellers, multi-currency on is almost always the right choice.

## Last reviewed

Last reviewed in early 2026. Mapping conventions occasionally update with new QuickBooks releases; track changes via the [docs repo](https://github.com/GitbookIO/evolve-demo).

## Related

* [Reconciliation mapping](reconciliation-mapping.md) — the detailed account-mapping options.
* [Settlement files](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reconciliation/settlement-files) — the source data the integration writes against.
* [NetSuite integration](../netsuite/README.md) — for higher-end accounting needs.
