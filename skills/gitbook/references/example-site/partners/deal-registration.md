---
icon: handshake-angle
hidden: true
description: Register a deal, track its status, see your protection windows.
---

# Deal registration

{% if visitor.claims.unsigned.persona !== "partner" %}

{% hint style="warning" icon="lock" %}
**This page is for active Evolve partners.** [Sign in to the partner portal](https://gitbook.com) to access deal registration. Not yet a partner? [Apply to the program](README.md).
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}

Registering deals early protects your commission for the duration of the deal cycle and gives the Evolve team enough context to support you in the sales process.

## Register a new deal

<p><a href="https://gitbook.com" class="button primary">Open registration form</a></p>

The form takes about 3 minutes. You'll need:

* The prospect's company name and primary contact.
* The expected use case — Payments, Identity, Connect, or some combination.
* The deal stage (qualified, proposal, contract).
* Estimated annual transaction volume or verification volume.

## Protection windows

Once a deal is registered and accepted, your protection window depends on the deal stage:

| Stage at registration | Protection window |
| --- | --- |
| **Qualified** | 60 days |
| **Proposal** | 90 days |
| **Contract sent** | 120 days |

If the deal closes within the window, you're the partner of record and earn full commission. After the window expires, the deal returns to the open pool and any partner (including direct sales) can claim it.

## What disqualifies a deal

A handful of conditions prevent registration acceptance:

* The prospect is already an active Evolve customer.
* The prospect is already in another partner's open registration.
* The prospect is in active direct-sales conversation with the Evolve team (we'll let you know within 48 hours of registration).
* The prospect is on the OFAC blocklist or in a vertical Evolve doesn't serve.

If your registration is rejected for any reason, you'll get a notification with the reason within 2 business days.

## Tracking deal status

The dashboard's **Deal status** view shows every deal you've registered with its current stage, days remaining in protection, and last-touch from the Evolve team.

For deals that have stalled, your partner success manager (PSM) can help re-engage. The "Request PSM help" button on each deal opens a Slack thread with your PSM included.

## Commission timing

Commissions are calculated quarterly based on referred-customer activity in the prior quarter. Payment lands in your registered bank account on the 15th of the second month after quarter close (so Q1 commissions pay May 15th).

The dashboard's **Commission preview** shows projected payout based on activity to date.

## Related

* [Marketing resources](marketing-resources.md) — co-marketing assets for joint sales activities.
* [Training](training.md) — sales certification, technical deep-dives.
* [Partner support](support.md) — your PSM contact details and escalation paths.

{% endif %}
