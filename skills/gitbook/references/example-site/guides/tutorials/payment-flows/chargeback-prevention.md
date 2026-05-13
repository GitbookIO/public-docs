---
icon: shield-check
description: A short, practical checklist that cuts dispute rates by 30–50% for most teams.
---

# Build a chargeback-prevention checklist

By the end of this tutorial you'll have a chargeback-prevention plan tuned to your business — not a vague list of best practices, but a specific set of changes you can ship in a day. The build takes about 60 minutes plus engineering time per fix.

This is for teams with a working payments integration that wants to lower dispute rates. If your dispute rate is over 0.5%, this tutorial is the highest-ROI thing you can do.

{% hint style="info" %}
**Prerequisites.** A live Evolve account with at least 30 days of payment history (you need data to find patterns). Read access to your Disputes report.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Pull your last 90 days of disputes

In **Reports → Disputes**, filter to the last 90 days. Export to CSV. The report has reason codes; the distribution across them tells you which prevention to focus on.

For most teams, the distribution looks something like:

| Reason | % of disputes |
| --- | --- |
| `fraudulent` | 40% |
| `unrecognized` | 20% |
| `product_not_received` | 15% |
| `defective` / `not_as_described` | 10% |
| Everything else | 15% |

Your distribution is what matters. Focus the next steps on your top two reasons.

{% endstep %}

{% step %}

### Fix your statement descriptor

The single highest-leverage fix for `unrecognized` disputes. In **Settings → Billing → Statement descriptor**, set it to your most-recognizable brand name within 22 characters. Customers see this on their bank statement weeks later — if it doesn't match what they remember buying, the bank gets a phone call.

If your brand name doesn't fit in 22 chars, add a **dynamic descriptor** per charge that includes the order number:

```
EVOLVE*ACME #1042
```

The base "EVOLVE*ACME" stays consistent; the order number makes the charge searchable in your customer support tooling.

{% endstep %}

{% step %}

### Add a self-serve refund path

The single highest-leverage fix for `fraudulent` disputes that aren't actually fraud. Most "I didn't make this charge" calls to banks are really "I made the charge and want a refund but couldn't figure out how."

* Add a **Get a refund** link to your receipt email.
* Add a **Get a refund** link to the order confirmation page.
* Make the link's destination either auto-refund (for low-value, low-risk products) or a one-click refund request that lands in your support inbox.

{% endstep %}

{% step %}

### Enable 3-D Secure for high-value charges

If `fraudulent` is in your top two and your average ticket is over $200, walk through [Set up 3-D Secure](3d-secure.md). The liability shift means you almost always win these disputes, and the 1–3% checkout-abandonment cost is usually less than the dispute losses.

{% endstep %}

{% step %}

### Wire up dispute alerts

Connect Verifi (Mastercard) and Ethoca (Amex) under **Settings → Risk → Dispute alerts**. These services notify you when a customer initiates a dispute *before* it becomes an official chargeback — usually 24–72 hours of warning.

Use that window to issue a pre-emptive refund. The dispute closes before it counts against your dispute rate or costs the $15 fee.

{% hint style="success" %}
For most marketplaces, dispute alerts pay for themselves in the first month. The $1 per alert is far less than the $15 dispute fee plus the disputed amount you'd have lost.
{% endhint %}

{% endstep %}

{% step %}

### For physical products: send tracking with shipment

Most `product_not_received` disputes are won with tracking and proof of delivery. Wire your fulfillment system to:

1. Send the tracking number to the customer in a shipment email (with a link to the carrier's tracking page).
2. Attach the tracking number to the Evolve charge as metadata:

{% tabs %}
{% tab title="Node" %}
```js
await evolve.charges.update(chargeId, {
  metadata: {
    tracking_number: "1Z999AA10123456784",
    carrier: "ups",
  },
});
```
{% endtab %}

{% tab title="Python" %}
```python
evolve.Charge.modify(
    charge_id,
    metadata={
        "tracking_number": "1Z999AA10123456784",
        "carrier": "ups",
    },
)
```
{% endtab %}
{% endtabs %}

When a `product_not_received` dispute opens, the metadata is auto-included in your evidence response.

{% endstep %}

{% step %}

### Set a dispute-rate threshold alarm

In **Settings → Alerts**, configure an alert when your rolling 30-day dispute rate exceeds 0.75%. The card networks' threshold is 1.0% — getting an alert at 0.75 gives you time to investigate before you hit a monitoring program.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"My dispute rate is fine but rising — what should I look at?"</summary>

Pull a per-product or per-cohort breakdown. A rising dispute rate is usually concentrated in a small slice of your business — a specific SKU with quality issues, a specific traffic source with high fraud, a specific country with weak fraud signals. Once you find it, the fix is targeted (pull the SKU, block the traffic source, require 3DS for the country) rather than systemic.

</details>

<details>

<summary>"We're a marketplace — most disputes are seller-driven"</summary>

The platform-level rate is what the networks watch, regardless of which seller caused them. Two patterns: (1) per-seller dispute monitoring with auto-pause above a threshold, (2) explicit risk pricing — sellers with higher historical dispute rates pay a higher take rate or carry a reserve. See [Handle disputes and refunds at scale](../marketplace/disputes-at-scale.md).

</details>

<details>

<summary>"Customer says they got a refund but the bank dispute came through anyway"</summary>

Sometimes happens — the dispute was already in flight when the refund posted. Submit evidence including the refund receipt; the network sees it and closes in your favor. The refund stays as a refund and the dispute closes "won" without double-deducting.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>3-D Secure</strong></td><td>For the fraud-dispute side.</td><td><a href="3d-secure.md">3d-secure.md</a></td></tr><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><strong>Save cards for repeat customers</strong></td><td>Recognized charges are non-disputed charges.</td><td><a href="save-cards.md">save-cards.md</a></td></tr><tr><td><h3><i class="fa-gavel" style="color:$primary;">:gavel:</i></h3></td><td><strong>Disputes at scale (Connect)</strong></td><td>For marketplace-specific patterns.</td><td><a href="../marketplace/disputes-at-scale.md">disputes-at-scale.md</a></td></tr></tbody></table>
