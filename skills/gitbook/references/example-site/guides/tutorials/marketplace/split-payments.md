---
icon: percent
description: Take your platform's cut on every payment — flat percentages, conditional rules, pass-through fees.
---

# Split each payment with application fees

By the end of this tutorial you'll have a payment split system that takes a flat application fee on every transaction, with hooks to layer conditional rules (per-seller tier, per-product category, per-volume) on top. The build takes about 60 minutes.

This is the platform-revenue side of Connect — your take rate is configured at session creation, the math is automatic, and reporting rolls up across all sellers.

{% hint style="info" %}
**Prerequisites.** [Onboard your first sellers](onboard-sellers.md) finished — you need at least one verified connected account to test against. Read [Connect → Splitting payments](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/platform-setup/splitting-payments) for the underlying model.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Set the platform default

In **Connect → Settings → Default split**, set your platform-wide application fee as a percentage of gross. Most platforms start at 5% and adjust. You can also set a flat-fee component (e.g. 5% + $0.30 per transaction).

This is the default; per-payment overrides take precedence.

{% endstep %}

{% step %}

### Override per checkout session

When you create a Checkout session for a payment that should route to a connected account, pass `application_fee_amount`:

{% tabs %}
{% tab title="Node" %}
```js
const session = await evolve.connect.checkoutSessions.create({
  amount: 10000,                          // $100 gross
  currency: "usd",
  connected_account: seller.evolve_account_id,
  application_fee_amount: computeFee(seller, 10000),
  success_url: "...",
  cancel_url: "...",
});
```
{% endtab %}

{% tab title="Python" %}
```python
session = evolve.connect.CheckoutSession.create(
    amount=10000,
    currency="usd",
    connected_account=seller.evolve_account_id,
    application_fee_amount=compute_fee(seller, 10000),
    success_url="...",
    cancel_url="...",
)
```
{% endtab %}
{% endtabs %}

`compute_fee` is your function — see the next step.

{% endstep %}

{% step %}

### Implement your fee logic

Most platforms outgrow a flat percentage within months. Build the fee function as a single point of truth, then evolve it as your business model matures:

{% tabs %}
{% tab title="Node" %}
```js
function computeFee(seller, grossAmount) {
  // Base rate by seller tier
  let rate;
  switch (seller.tier) {
    case "premium": rate = 0.03; break;  // 3%
    case "standard": rate = 0.05; break; // 5%
    case "new": rate = 0.07; break;      // 7% for first 90 days
    default: rate = 0.05;
  }

  // Volume discount: 1.5% above $10k per transaction
  if (grossAmount > 10_00000) rate = Math.min(rate, 0.015);

  // Promotional 0% on Black Friday weekend
  const today = new Date();
  if (isBlackFridayWeekend(today)) rate = 0;

  return Math.round(grossAmount * rate);
}
```
{% endtab %}

{% tab title="Python" %}
```python
def compute_fee(seller, gross_amount):
    rates = {"premium": 0.03, "standard": 0.05, "new": 0.07}
    rate = rates.get(seller.tier, 0.05)

    if gross_amount > 10_00000:
        rate = min(rate, 0.015)

    if is_black_friday_weekend(date.today()):
        rate = 0

    return round(gross_amount * rate)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Decide who eats the processing fee

By default, the card processing fee comes off the platform's application fee — meaning your effective margin is `application_fee - processing_fee`.

To pass the processing fee through to the seller instead:

{% tabs %}
{% tab title="Node" %}
```js
const session = await evolve.connect.checkoutSessions.create({
  amount: 10000,
  currency: "usd",
  connected_account: seller.evolve_account_id,
  application_fee_amount: 500,
  application_fee_includes_processing: false,  // seller absorbs processing
  success_url: "...",
  cancel_url: "...",
});
```
{% endtab %}

{% tab title="Python" %}
```python
session = evolve.connect.CheckoutSession.create(
    amount=10000,
    currency="usd",
    connected_account=seller.evolve_account_id,
    application_fee_amount=500,
    application_fee_includes_processing=False,
    success_url="...",
    cancel_url="...",
)
```
{% endtab %}
{% endtabs %}

Marketplaces with thin take-rates almost always pass through. Marketplaces competing on seller experience absorb. Pick once at the platform level; keep it consistent.

{% endstep %}

{% step %}

### Watch the splits in the dashboard

In **Reports → Application fees**, you'll see daily/weekly/monthly aggregates of your platform revenue, broken down by seller and by date. Charts you'll watch:

* Total application fees per day.
* Take rate (application fees / gross volume).
* Top sellers by gross volume.
* Top sellers by application fees earned.

For deeper analysis (per-product-category, per-cohort) export the application-fees report and pivot in your data warehouse.

{% endstep %}

{% step %}

### Test with refunds

Refund a charge in test mode. By default, the application fee is refunded proportionally — full refund takes the full application fee, partial refund takes a proportional amount.

To override:

{% tabs %}
{% tab title="Node" %}
```js
const refund = await evolve.refunds.create({
  charge: "ch_3KsM12pL9qXa7",
  refund_application_fee: false,  // platform keeps the fee
});
```
{% endtab %}

{% tab title="Python" %}
```python
refund = evolve.Refund.create(
    charge="ch_3KsM12pL9qXa7",
    refund_application_fee=False,
)
```
{% endtab %}
{% endtabs %}

Useful when the seller is at fault for the refund — the platform keeps its cut.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Sellers complain the dashboard doesn't show what fees they paid"</summary>

The platform's application fee shows up on each charge as a separate line item. From the seller's connected-account dashboard, they see the gross, the application fee deducted, and the net. If sellers complain, walk them to the per-charge detail page — the breakdown is right there.

</details>

<details>

<summary>"Math doesn't match between Evolve and our internal records"</summary>

Most-cited cause: rounding differences. Always work in integer cents, never in float dollars. `round(amount * rate)` in your code; double-check on Evolve's side that the same integer math applies. One sub-cent rounding error per transaction adds up over 10,000 transactions.

</details>

<details>

<summary>"How do I do tiered commissions (e.g. 5% on first $1k, 3% above)"</summary>

Compute it in your fee function. Evolve's API takes a single `application_fee_amount` per session — your platform decides what to put there. The dashboard's reports show the actual per-charge fee, which is enough for sellers to verify.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-money-bill-transfer" style="color:$primary;">:money-bill-transfer:</i></h3></td><td><strong>Per-seller payout schedules</strong></td><td>How seller balances become bank deposits.</td><td><a href="payout-schedules.md">payout-schedules.md</a></td></tr><tr><td><h3><i class="fa-gavel" style="color:$primary;">:gavel:</i></h3></td><td><strong>Disputes at scale</strong></td><td>Refund and dispute splits explained.</td><td><a href="disputes-at-scale.md">disputes-at-scale.md</a></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>Custom onboarding</strong></td><td>For platforms with their own brand.</td><td><a href="custom-onboarding.md">custom-onboarding.md</a></td></tr></tbody></table>
