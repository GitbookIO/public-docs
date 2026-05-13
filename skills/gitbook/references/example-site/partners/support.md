---
icon: headset
hidden: true
description: Direct line to your partner success manager, escalation paths, and partner Slack.
---

# Partner support

{% if visitor.claims.unsigned.persona !== "partner" %}

{% hint style="warning" icon="lock" %}
**This page is for active Evolve partners.** [Sign in to the partner portal](https://gitbook.com) to access partner support contacts. Not yet a partner? [Apply to the program](README.md).
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.persona === "partner" %}

Partners get direct access to a partner success manager (PSM), a private Slack channel, and a dedicated escalation path for technical and customer issues.

## Your partner success manager

Every active partner is assigned a PSM. They're your single point of contact for:

* Strategic partnership questions.
* Deal registration help and roadmap-influence requests.
* Quarterly business reviews.
* Co-marketing program coordination.
* Customer escalations that need executive attention.

Your PSM's contact details are on the **Account** tab in the partner portal. Most PSMs prefer Slack for day-to-day; email or video call for anything substantial.

## Partner Slack

The Evolve partner Slack workspace has channels for:

* `#general` — partner-to-partner discussion.
* `#technical-help` — engineering escalation, monitored by the Evolve solutions team during business hours.
* `#deal-help` — sales and pricing questions, monitored by partner-success leadership.
* `#announcements` — Evolve product updates aimed at the partner audience.
* Per-partner private channels with your PSM and a few of our team.

<p><a href="https://gitbook.com" class="button primary">Open the workspace</a></p>

## Escalation paths

Three escalation levels, in order:

{% stepper %}
{% step %}

### Your PSM

For most things — partner program questions, deal help, customer escalations, roadmap requests. Slack DM or email; response time is typically within 4 business hours.

{% endstep %}

{% step %}

### Partner team leadership

When your PSM is out or the issue is bigger than a single PSM can handle. Email [partners@evolve.com](mailto:partners@evolve.com) with "ESCALATION" in the subject. Response within 1 business day.

{% endstep %}

{% step %}

### Executive sponsor

For partner-program-level issues that need a higher altitude. Each partner with $1M+ annual referred volume gets an executive sponsor on the Evolve leadership team — your PSM has the contact details.

{% endstep %}
{% endstepper %}

## Customer escalations

When one of your referred customers has a production issue that needs urgent attention:

1. **First**: have the customer open a support ticket via the standard [<code class="expression">space.vars.dashboard_live</code>/support](https://gitbook.com) flow.
2. If the issue is critical (production-impacting, security, etc.), Slack-DM your PSM with the ticket number — they'll route to the right team and get a real-time update for you.
3. For incidents affecting multiple customers, [<code class="expression">space.vars.status_page</code>](https://gitbook.com) is the canonical source.

Don't message your PSM with non-urgent customer questions — those should flow through the standard support channel so they're tracked.

## Office hours

Live drop-in sessions on the second Tuesday of each month, 11am ET / 4pm GMT. Whatever you bring, partner-success leadership and rotating product/engineering folks are there.

Office hours are recorded; recordings live in [Training → Recordings](training.md#recordings).

## SLAs

* **Slack technical-help**: response within 4 business hours.
* **PSM**: response within 4 business hours; resolution depends on the request.
* **Escalation email**: response within 1 business day.
* **Critical customer escalation**: real-time triage; resolution per the customer's contracted SLA.

## Status and incidents

Platform status: [<code class="expression">space.vars.status_page</code>](https://gitbook.com).

For incidents affecting your customers specifically, your PSM will reach out within 30 minutes of incident detection. Subscribe to status-page updates via email or RSS for the firehose.

## Related

* [Deal registration](deal-registration.md) — protect commissions on the deals you're closing.
* [Marketing resources](marketing-resources.md) — assets for joint sales activities.
* [Training](training.md) — certification, recordings, sales enablement.

{% endif %}
