---
icon: cart-shopping
description: What the buyer actually sees, from the storefront to the receipt.
---

# Buyer experience

The buyer doesn't know or care that your site is built on Connect — they're trying to pay the seller. Your job, as the platform, is to make sure that the parts of the experience the buyer notices feel like one coherent flow, even though there are three parties (buyer, seller, you) involved.

## The five moments

The buyer touches five things during a typical purchase. Each one is a place to get the platform vs seller framing right.

### <i class="fa-store" style="color:$primary;">:store:</i> 1. The storefront

Whatever page the buyer adds an item to a cart from. This is your platform's responsibility — a marketplace homepage, a SaaS app's billing page, a per-seller URL on your domain.

The storefront should make it clear who the seller is. The buyer should never reach checkout without knowing the brand they're paying.

### <i class="fa-credit-card" style="color:$primary;">:credit-card:</i> 2. The checkout

Where the card details get entered. Three integration shapes — see [Hosted vs embedded](hosted-vs-embedded.md). Whichever you pick, the checkout shows:

* The amount.
* The seller's name (and optionally logo).
* The supported payment methods.
* Whether the application fee is disclosed (often it isn't, but some marketplaces show it for transparency).

### <i class="fa-id-card" style="color:$primary;">:id-card:</i> 3. The card statement

The descriptor on the buyer's bank statement, weeks later. This is the most-disputed moment in any payments flow — buyers don't recognize the charge, call their bank, and a chargeback is born.

Most platforms use `PLATFORM*SELLER` — your platform name first (so the buyer knows which app to look in), then the seller's name (so they remember what they actually bought). Both must fit in the network's limit (Visa: 22 chars, Mastercard: 25 chars).

You can configure default behavior in **Settings → Connect → Statement descriptor** and override per-seller for sellers with strong brand recognition.

### <i class="fa-receipt" style="color:$primary;">:receipt:</i> 4. The receipt email

Sent from `receipts@evolve.com` (or your custom domain on Enterprise) immediately after payment. Contains:

* What was bought (description from the charge).
* Who they bought it from (seller's name).
* Who facilitated (your platform).
* A "Need help?" CTA pointing at the seller, the platform, or both — your call.

You can fully customize the template in **Settings → Connect → Email templates**, or replace it with your own outbound email and disable Evolve's default.

### <i class="fa-comments" style="color:$primary;">:comments:</i> 5. Support

When something goes wrong, the buyer reaches out. They might reach out to:

* The seller directly (their email or chat).
* Your platform's support.
* Their card-issuing bank (which means a dispute).

Make the first two easy and you'll get fewer of the third. Your platform's role is usually to **route** the support request to the right party — buyer questions about delivery go to the seller, questions about platform behavior or refunds initiated by the platform stay with you.

## Receipt customization

Three customization layers, each with a different set of decisions:

{% columns %}
{% column width="33%" %}

### <i class="fa-palette" style="color:$primary;">:palette:</i> Visual

Logo, brand colors, fonts. Can be platform-wide or per-seller. Most platforms use platform branding everywhere; some white-label per-seller.

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-language" style="color:$primary;">:language:</i> Localization

Receipt language is set by the buyer's locale, with the seller's locale as a fallback. Evolve translates the structural text; the seller's product description stays in whatever language they wrote it.

{% endcolumn %}

{% column width="33%" %}

### <i class="fa-pen-to-square" style="color:$primary;">:pen-to-square:</i> Custom fields

Order numbers, fulfillment estimates, shipping addresses. Surface anything from your platform's data model on the receipt by configuring custom fields per charge.

{% endcolumn %}
{% endcolumns %}

## Avoiding common buyer-experience mistakes

<details>

<summary>Don't hide the seller's name on the storefront</summary>

Platforms that mask which seller the buyer is paying tend to see higher dispute rates — not because of fraud, but because the buyer doesn't recognize the charge later. Even if your platform is the dominant brand, show the seller's name somewhere on the page where the buyer adds to cart.

</details>

<details>

<summary>Don't surprise the buyer with a different brand at checkout</summary>

If the storefront is your platform's brand and the checkout suddenly says "Pay Acme Corp", buyers get confused and abandon. Either keep the platform brand visible at checkout, or make sure the seller is mentioned consistently from the storefront onward.

</details>

<details>

<summary>Don't bury the support contact</summary>

A buyer who can't find a way to ask for a refund will go to their bank instead. Surface a "Get help" link on the receipt and the storefront, ideally with the seller's contact and a "Or contact platform support" fallback.

</details>

## Related

* [Hosted vs embedded](hosted-vs-embedded.md) — choosing the integration shape.
* [Customization](customization.md) — themes, languages, and per-seller branding.
* [Refunds and disputes](../platform-setup/refunds-and-disputes.md) — what happens when the buyer asks for their money back.
