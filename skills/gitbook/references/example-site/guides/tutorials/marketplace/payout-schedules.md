---
icon: money-bill-transfer
description: Configure how often each seller gets paid — daily, weekly, monthly, on demand.
---

# Configure per-seller payout schedules

By the end of this tutorial you'll have a payout system where sellers can pick their own schedule (within the limits you set), where on-demand payouts are available for fast-cash sellers, and where reserves apply automatically to high-risk cohorts. The build takes about 60 minutes.

This is the seller-cash-flow side of Connect — the schedule directly affects seller satisfaction and is one of the most-asked-about features by sellers themselves.

{% hint style="info" %}
**Prerequisites.** [Onboard your first sellers](onboard-sellers.md) and [Split payments](split-payments.md) finished. At least one verified connected account with a successful test payment.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Pick the platform default

In **Connect → Settings → Default payout schedule**, set the default for new sellers. Three patterns we see most:

* **Daily** — best for cash-flow-sensitive sellers (gig economy, delivery). Highest seller satisfaction.
* **Weekly** — best for SaaS marketplaces and B2B platforms. Aligns with seller's invoicing cadence.
* **Monthly** — best for high-margin businesses where seller cash flow doesn't drive churn.

Pick the one that matches your typical seller. Override per-seller as needed.

{% endstep %}

{% step %}

### Let sellers override

Sellers may have a strong preference. Surface a control in their dashboard:

{% tabs %}
{% tab title="Node" %}
```js
app.post("/sellers/:id/payout-schedule", async (req, res) => {
  const seller = await db.sellers.findOne(req.params.id);
  const allowedSchedules = ["daily", "weekly", "monthly"];

  if (!allowedSchedules.includes(req.body.schedule)) {
    return res.status(400).json({ error: "Invalid schedule" });
  }

  await evolve.connect.connectedAccounts.update(seller.evolve_account_id, {
    payout_schedule: { interval: req.body.schedule },
  });

  res.json({ ok: true });
});
```
{% endtab %}

{% tab title="Python" %}
```python
@app.post("/sellers/<id>/payout-schedule")
def update_schedule(id):
    seller = db.sellers.find(id)
    allowed = {"daily", "weekly", "monthly"}

    if request.json["schedule"] not in allowed:
        return {"error": "Invalid schedule"}, 400

    evolve.ConnectedAccount.modify(
        seller.evolve_account_id,
        payout_schedule={"interval": request.json["schedule"]},
    )
    return {"ok": True}
```
{% endtab %}
{% endtabs %}

You can restrict allowed values — some platforms don't expose `daily` to all sellers because of cash-management overhead.

{% endstep %}

{% step %}

### Set up reserves for new sellers

In **Connect → Settings → Reserves**, configure a rolling reserve for sellers in their first 90 days:

* **Reserve percentage** — usually 5–10%.
* **Reserve window** — usually 90 days rolling.
* **Applies to** — typically "All new sellers in their first 90 days," graduating to no reserve after.

The reserve protects you against early-account fraud and dispute exposure. It rolls off automatically; sellers see their reserved vs payable balance in their portal.

{% hint style="warning" %}
**Communicate reserves clearly during onboarding.** Sellers who discover a reserve mid-month feel ambushed. Mention it in your seller terms, the onboarding email, and the seller's dashboard.
{% endhint %}

{% endstep %}

{% step %}

### Enable on-demand payouts (Enterprise)

For platforms where seller cash flow is the product (gig apps, instant marketplaces), on-demand payouts are differentiating. In **Connect → Settings → Instant payouts**:

* Enable for all sellers, or for a specific tier.
* Decide who pays the 1% fee — seller, platform, or split.
* Set per-day caps if you want.

Surface in the seller's dashboard with a **Pay me now** button. Most platforms cap to 5 instant payouts per day per seller.

{% endstep %}

{% step %}

### Listen for payout events

Subscribe to:

* `payout.created` — payout scheduled. Useful for "your money's on the way" emails.
* `payout.paid` — payout landed in seller's bank.
* `payout.failed` — closed account, frozen account, wrong details.

For failed payouts, your handler should:

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "payout.failed") {
  const payout = event.data.object;
  await notifySeller(payout.connected_account, "payout_failed", {
    reason: payout.failure_reason,
    amount: payout.amount,
  });
  await pauseFurtherPayouts(payout.connected_account);
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "payout.failed":
    payout = event.data.object
    notify_seller(
        payout.connected_account,
        "payout_failed",
        reason=payout.failure_reason,
        amount=payout.amount,
    )
    pause_further_payouts(payout.connected_account)
```
{% endtab %}
{% endtabs %}

The seller updates their bank account in their portal; your code resumes payouts and the failed amount goes out on the next scheduled payout.

{% endstep %}

{% step %}

### Test the lifecycle

In test mode, use the dashboard's **Test clock** feature in **Connect → Sellers → [seller]**:

* Make a few test charges to build a balance.
* Fast-forward by a day to see a daily payout fire.
* Use the failure-injection toggle to test a failed payout.

Confirm your handler emails the seller correctly and that the dashboard shows the right status.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Sellers see different available balances on different days"</summary>

Available balance fluctuates as new charges land, refunds deduct, and reserves roll off. The seller's portal shows the balance with all three layers explained — make sure your own UI doesn't oversimplify and confuse them.

</details>

<details>

<summary>"A payout failed but the seller swears their bank account is fine"</summary>

Failed payouts include a `failure_reason` from the bank. The most common: account-name mismatch (the seller's name on file with us doesn't match the name on the bank account). The seller fixes this by re-verifying in the portal. Re-trigger the payout once the new bank account is verified.

</details>

<details>

<summary>"On-demand payouts work but cost us money — sellers pay the 1% fee but customers complain about the deduction"</summary>

Common when the fee structure isn't clear. Two fixes: (1) only show the **Pay me now** button when the seller has a balance large enough to make the 1% fee insignificant; (2) absorb the fee yourself for premium-tier sellers as a perk.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-percent" style="color:$primary;">:percent:</i></h3></td><td><strong>Split payments</strong></td><td>What ends up in the seller's balance.</td><td><a href="split-payments.md">split-payments.md</a></td></tr><tr><td><h3><i class="fa-gavel" style="color:$primary;">:gavel:</i></h3></td><td><strong>Disputes at scale</strong></td><td>How disputes affect payouts.</td><td><a href="disputes-at-scale.md">disputes-at-scale.md</a></td></tr><tr><td><h3><i class="fa-building-columns" style="color:$primary;">:building-columns:</i></h3></td><td><strong>Bank verification with Plaid</strong></td><td>Up-front verification prevents most payout failures.</td><td><a href="../verification/plaid-bank-verification.md">plaid-bank-verification.md</a></td></tr></tbody></table>
