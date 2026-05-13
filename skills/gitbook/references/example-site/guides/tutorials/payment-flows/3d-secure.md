---
icon: shield-halved
description: Apply 3-D Secure where it earns its keep — high-value charges, fraud-prone cohorts, EU SCA cases.
---

# Set up 3-D Secure for high-value charges

By the end of this tutorial you'll have a 3-D Secure rule set that requires authentication for the transactions where the liability shift is worth the friction, and skips it where it isn't. The build takes about 30 minutes.

The trade-off is real: 3DS adds 5–15 seconds and abandons 1–3% of customers. But on a $1,000 charge with a 50% chance of dispute, the math usually favors requiring it.

{% hint style="info" %}
**Prerequisites.** A working checkout integration ([Accept a one-time payment](accept-one-time-payment.md) is enough). Reading [Payments → 3-D Secure and SCA](https://app.gitbook.com/s/w3LlITSOQye8o4wjsQXV/accept-payments/3d-secure) first will help — this tutorial assumes the conceptual model.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Decide on a strictness preset

In **Settings → Risk → 3-D Secure**, three presets to start from:

* **Required only** (default) — Evolve handles required cases (EEA SCA), everything else skips. Use this if you don't have a strong opinion yet.
* **By rule** — your custom rules layered on top of required cases. Use this for the rest of this tutorial.
* **Always** — every payment goes through 3DS. Use only if you're a regulated vertical that needs maximum liability shift.

Pick **By rule**.

{% endstep %}

{% step %}

### Add a high-value rule

Click **Add rule**. Set the condition: `amount > 500 USD`. Set the action: **Require 3DS**. Save.

This is the most-common starting rule. The threshold to pick depends on your average ticket size — somewhere between 2x and 5x your average is a good zone.

{% endstep %}

{% step %}

### Add a new-customer rule

Click **Add rule** again. Condition: `customer.history.successful_payments == 0`. Action: **Require 3DS**.

Customers with no prior successful payments are higher-risk. Combined with the high-value rule, this catches most of the disputes worth catching.

{% endstep %}

{% step %}

### Test in your checkout

Use these test cards in test mode:

| Card | Result |
| --- | --- |
| `4000 0000 0000 0002` | Approved without 3DS challenge |
| `4000 0027 6000 3184` | Approved after 3DS challenge |
| `4000 0082 6000 3178` | Failed 3DS authentication |

For a $501 charge or a new customer, the second card should now show a 3DS challenge step. Walk through it and confirm the charge succeeds.

{% endstep %}

{% step %}

### Watch it in production

After deploying to live mode, the **Routing report** under **Reports** shows a `3ds_required` column. Monitor for the first week:

* What percentage of charges hit 3DS? Should match your rules.
* What's the abandonment rate at the 3DS step? Should be 1–3%.
* What's your dispute rate vs the previous month? Should drop noticeably for the cohort matching your rules.

If abandonment is much higher than 3%, your rule might be too aggressive — relax the threshold.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"3DS triggers even on existing recurring subscriptions"</summary>

Recurring charges with a recorded mandate should be exempt from SCA via the merchant-initiated transaction (MIT) exemption. If your subscriptions are getting 3DS-challenged on renewal, check that you're saving the mandate properly — see [Save cards for repeat customers](save-cards.md).

</details>

<details>

<summary>"Customer says the 3DS challenge is on a Russian/Chinese page they don't read"</summary>

The 3DS UI is provided by the issuer, not Evolve. Evolve passes the customer's IP locale; the issuer decides language. Most banks support 5–10 languages but not all. If your cohort hits this often, mention it in your checkout copy: "Your bank may ask you to confirm — follow their prompts in your bank's app."

</details>

<details>

<summary>"My dispute rate didn't drop after enabling 3DS"</summary>

Two likely causes: (1) your rules don't cover the disputes you're losing — pull a dispute report and see which charges are losing, then check whether your rule would have caught them; (2) the disputes are not fraud — `product_not_received` and `defective` aren't covered by 3DS's liability shift. See [Prevent chargebacks](chargeback-prevention.md) for the non-fraud side.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Prevent chargebacks</strong></td><td>The non-fraud side of dispute reduction.</td><td><a href="chargeback-prevention.md">chargeback-prevention.md</a></td></tr><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><strong>Save cards for repeat customers</strong></td><td>Mandates and merchant-initiated transactions.</td><td><a href="save-cards.md">save-cards.md</a></td></tr><tr><td><h3><i class="fa-arrows-rotate" style="color:$primary;">:arrows-rotate:</i></h3></td><td><strong>Subscription billing</strong></td><td>Where 3DS exemptions especially matter.</td><td><a href="subscription-billing.md">subscription-billing.md</a></td></tr></tbody></table>
