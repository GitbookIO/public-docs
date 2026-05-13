---
icon: paint-roller
description: Brand the checkout — colors, fonts, logos, fields, and per-seller overrides.
---

# Customization

The default Connect checkout looks neutral and modern, with the seller's name and your platform's name in the right places. Most platforms customize at least the colors and logo to match their brand. Some go further — custom fonts, custom layouts, white-label per-seller branding.

This page covers what you can customize, where, and at which integration shape.

## Visual customization

What you control depends on the shape:

| | Hosted | Embedded | Direct API |
| --- | :---: | :---: | :---: |
| Logo | ✅ | ✅ | ✅ |
| Brand color (primary) | ✅ | ✅ | ✅ |
| Brand color (secondary) | ✅ | ✅ | ✅ |
| Custom font | — | ✅ | ✅ |
| Field layout | — | ✅ | ✅ |
| Custom CSS / classes | — | Limited | ✅ |
| Background image | ✅ | ✅ | ✅ |

Settings live in **Connect → Branding** in the dashboard. Changes apply immediately on hosted and embedded; for direct API integrations, they're hints — your code does the actual rendering.

## Per-seller branding

By default, all sellers on your platform use the platform's branding. For sellers with strong brands of their own — established stores on a marketplace, B2B sellers under enterprise contracts — you can let them override:

{% if visitor.claims.unsigned.plan === "enterprise" %}

{% hint style="success" icon="layer-group" %}
**You're on Enterprise** — full per-seller branding (including custom domains and per-seller CSS) is available. Configure in **Connect → Branding → Per-seller overrides**.
{% endhint %}

{% endif %}

{% if visitor.claims.unsigned.plan === "growth" %}

{% hint style="info" icon="layer-group" %}
**You're on Growth** — per-seller logo and brand color overrides are available. Custom fonts and CSS require Enterprise.
{% endhint %}

{% endif %}

| Override | Growth | Enterprise |
| --- | :---: | :---: |
| Per-seller logo | ✅ | ✅ |
| Per-seller brand colors | ✅ | ✅ |
| Per-seller font | — | ✅ |
| Per-seller CSS | — | ✅ |
| Per-seller subdomain (`acme.checkout.evolve.com`) | — | ✅ |
| Custom domain (`pay.acme.com`) | — | ✅ |

## Custom fields

The default checkout collects:

* Card details (number, expiry, CVC).
* Billing name and ZIP.
* Email (for the receipt).

You can add custom fields per session — order numbers, fulfillment dates, dietary preferences, anything your platform's data model needs:

{% columns %}
{% column width="50%" %}

### <i class="fa-text-width" style="color:$primary;">:text-width:</i> Text fields

Free-text input. Validation rules: required, min/max length, regex.

{% endcolumn %}

{% column width="50%" %}

### <i class="fa-list-check" style="color:$primary;">:list-check:</i> Dropdowns

Predefined options. Useful for shipping methods, gift wrap, etc.

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column width="50%" %}

### <i class="fa-square-check" style="color:$primary;">:square-check:</i> Checkboxes

Single boolean. Common use: opt-in to marketing or terms acceptance.

{% endcolumn %}

{% column width="50%" %}

### <i class="fa-calendar" style="color:$primary;">:calendar:</i> Date pickers

For delivery dates, appointments, gift-card send dates.

{% endcolumn %}
{% endcolumns %}

Custom field values land on the charge as metadata, visible in the dashboard, on receipts, in webhook payloads, and on the [settlement file](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/reconciliation/settlement-files).

## Localization

The hosted and embedded checkouts auto-detect the buyer's locale from their browser and translate the structural text — labels, error messages, button copy — into 30+ languages. The seller's product description and the platform's branded text stay in whatever language you provide.

Override the auto-detection by setting `locale` on the checkout session:

```http
POST /v1/checkout_sessions
{
  "amount": 4200,
  "currency": "usd",
  "locale": "fr"
}
```

For languages not in the default 30, Enterprise customers can supply a translation file and Evolve will use it.

## Receipts

The receipt email template is customizable separately from the checkout itself. Three layers:

1. **Template content** — what shows up in the email body.
2. **From address** — `receipts@evolve.com` by default; can be your own domain.
3. **Reply-to** — defaults to your platform's support; can be set per-seller.

Configure under **Connect → Email templates**.

## What you can't customize

A few things are locked, for compliance and trust reasons:

* The list of payment methods Evolve supports — sellers can't add a network we don't process.
* The card-collection iframe in embedded — the actual `<input>`s are Evolve's, for PCI scope reasons.
* The "Powered by Evolve" footer on hosted checkouts (Growth plan); removable on Enterprise.
* The receipt's required legal disclosures (varies by region).

## Related

* [Hosted vs embedded](hosted-vs-embedded.md) — what's available at each shape.
* [Buyer experience](buyer-experience.md) — what the customizations look like to the buyer.
