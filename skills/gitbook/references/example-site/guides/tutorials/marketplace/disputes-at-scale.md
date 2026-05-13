---
icon: gavel
description: Route disputes to the responsible seller, gather evidence automatically, and protect your platform's dispute rate.
---

# Handle disputes and refunds at scale

By the end of this tutorial you'll have a multi-seller dispute management flow that delegates evidence collection to sellers, automates evidence gathering where possible, and keeps your platform-level dispute rate below the network thresholds. The build takes about 2 hours.

This is one of the most operationally complex parts of running a marketplace at scale. The platform is the merchant of record for card-network purposes — meaning the platform's dispute rate is what the networks watch, regardless of which seller caused the dispute.

{% hint style="info" %}
**Prerequisites.** [Onboard sellers](onboard-sellers.md) and [Split payments](split-payments.md) finished. Read [Connect → Refunds and disputes](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/platform-setup/refunds-and-disputes) for the model.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Decide your dispute policy

Three policies for who absorbs the dispute:

* **Pass to seller** — seller's balance covers the disputed amount + fee. Most common.
* **Platform absorbs** — platform balance covers everything. For premium-tier sellers as a perk.
* **Split** — platform takes the $15 fee, seller takes the disputed amount. Some platforms use this as a middle-ground.

Set the platform default in **Connect → Settings → Dispute policy**. Override per-seller as needed.

{% endstep %}

{% step %}

### Subscribe to dispute events

Two key events:

* `dispute.created` — a new dispute opened. Funds are withdrawn from the responsible balance immediately.
* `dispute.evidence_required` — reminder that the response window is closing.

{% endstep %}

{% step %}

### Route dispute notifications to the seller

Most platforms delegate evidence collection to the seller. When a dispute opens against one of their charges:

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "dispute.created") {
  const dispute = event.data.object;
  const seller = await db.sellers.findOne({
    evolve_account_id: dispute.connected_account,
  });

  await sendEmail(seller.email, "dispute_opened", {
    disputeId: dispute.id,
    amount: dispute.amount,
    reasonCode: dispute.reason,
    deadline: dispute.evidence_due_by,
    portalUrl: `https://yourapp.com/disputes/${dispute.id}`,
  });

  await db.disputes.create({
    evolve_dispute_id: dispute.id,
    seller_id: seller.id,
    status: "awaiting_seller",
    deadline: dispute.evidence_due_by,
  });
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "dispute.created":
    dispute = event.data.object
    seller = db.sellers.find_by_account(dispute.connected_account)

    send_email(
        seller.email,
        "dispute_opened",
        dispute_id=dispute.id,
        amount=dispute.amount,
        reason_code=dispute.reason,
        deadline=dispute.evidence_due_by,
        portal_url=f"https://yourapp.com/disputes/{dispute.id}",
    )

    db.disputes.create(
        evolve_dispute_id=dispute.id,
        seller_id=seller.id,
        status="awaiting_seller",
        deadline=dispute.evidence_due_by,
    )
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Build a seller-facing dispute portal

Sellers shouldn't see the Evolve dashboard directly — they see your portal. Build a per-dispute page where they can:

1. Read the dispute details (reason code, customer's claim, deadline).
2. Upload evidence — shipping receipts, customer-communication logs, signed agreements.
3. Choose to fight or accept.
4. Submit.

Auto-collect what you can — for `product_not_received` disputes on shipped goods, your fulfillment system already has the tracking number. Pre-fill the response.

{% endstep %}

{% step %}

### Submit evidence to Evolve

When the seller submits, your code packages it and sends to Evolve:

{% tabs %}
{% tab title="Node" %}
```js
app.post("/disputes/:id/respond", async (req, res) => {
  const dispute = await db.disputes.findOne(req.params.id);

  await evolve.disputes.update(dispute.evolve_dispute_id, {
    evidence: {
      product_description: req.body.productDescription,
      shipping_carrier: req.body.carrier,
      shipping_tracking_number: req.body.trackingNumber,
      customer_communication: req.body.commsLog,
    },
    submit: req.body.action === "submit",
  });

  await db.disputes.update(dispute.id, { status: "submitted" });
  res.json({ ok: true });
});
```
{% endtab %}

{% tab title="Python" %}
```python
@app.post("/disputes/<id>/respond")
def respond(id):
    dispute = db.disputes.find(id)

    evolve.Dispute.modify(
        dispute.evolve_dispute_id,
        evidence={
            "product_description": request.json["product_description"],
            "shipping_carrier": request.json["carrier"],
            "shipping_tracking_number": request.json["tracking_number"],
            "customer_communication": request.json["comms_log"],
        },
        submit=request.json["action"] == "submit",
    )

    db.disputes.update(dispute.id, status="submitted")
    return {"ok": True}
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Set a default-action policy for non-responsive sellers

Some sellers won't respond. Your platform needs a default action when the deadline approaches with no submission:

{% tabs %}
{% tab title="Node" %}
```js
async function handleEvidenceDeadline(dispute) {
  if (dispute.status === "awaiting_seller") {
    if (config.default_action === "accept") {
      await evolve.disputes.accept(dispute.evolve_dispute_id);
    } else if (config.default_action === "submit_minimal") {
      await evolve.disputes.update(dispute.evolve_dispute_id, {
        evidence: { product_description: "Order auto-fulfilled per platform records." },
        submit: true,
      });
    }
  }
}
```
{% endtab %}

{% tab title="Python" %}
```python
def handle_evidence_deadline(dispute):
    if dispute.status == "awaiting_seller":
        if config.default_action == "accept":
            evolve.Dispute.accept(dispute.evolve_dispute_id)
        elif config.default_action == "submit_minimal":
            evolve.Dispute.modify(
                dispute.evolve_dispute_id,
                evidence={"product_description": "Order auto-fulfilled per platform records."},
                submit=True,
            )
```
{% endtab %}
{% endtabs %}

For most marketplaces, "submit minimal" produces better outcomes than "accept" — at least the network knows you tried.

{% endstep %}

{% step %}

### Monitor per-seller dispute rates

A small number of bad sellers can drag down the platform's dispute rate. Build a daily report:

* Per-seller dispute rate (disputes / charges, last 90 days).
* Sellers above 1% — auto-flag for review.
* Sellers above 1.5% — auto-pause.

Use the Connect API to retrieve dispute stats per connected account, or pull the per-seller report and calculate yourself.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Our platform-level dispute rate is fine but rising"</summary>

Pull a per-seller breakdown and look for the bottom 10% of sellers (by dispute rate). Most platforms find that 5% of sellers cause 50% of disputes. Tighten onboarding requirements, add a dispute-rate clause to your seller terms, and apply per-seller reserves to the high-risk cohort.

</details>

<details>

<summary>"A seller's dispute rate is high but they bring high revenue"</summary>

Hard call. Some platforms maintain a "high-risk cohort" with explicit risk pricing — these sellers pay a higher take rate that covers the expected dispute losses. Others terminate the cohort entirely. Decide based on your unit economics; whatever you do, make the policy explicit in your seller terms.

</details>

<details>

<summary>"Sellers complain that legitimate sales are getting disputed"</summary>

Some of this is unavoidable. The biggest preventable category is `unrecognized` disputes — fix the statement descriptor (see [Prevent chargebacks](../payment-flows/chargeback-prevention.md)). For `product_not_received`, make sure tracking is recorded automatically — sellers who manually-attach tracking forget half the time.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Prevent chargebacks</strong></td><td>The platform-wide chargeback playbook.</td><td><a href="../payment-flows/chargeback-prevention.md">chargeback-prevention.md</a></td></tr><tr><td><h3><i class="fa-money-bill-transfer" style="color:$primary;">:money-bill-transfer:</i></h3></td><td><strong>Per-seller payout schedules</strong></td><td>Reserves and dispute holds.</td><td><a href="payout-schedules.md">payout-schedules.md</a></td></tr><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>3-D Secure</strong></td><td>Liability shift on the disputable charges.</td><td><a href="../payment-flows/3d-secure.md">3d-secure.md</a></td></tr></tbody></table>
