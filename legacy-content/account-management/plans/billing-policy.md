# Billing policy

This policy covers GitBook’s current plans on [Plans](./).

Our billing model combines site pricing and member pricing:

* **Basic** costs **$0 per site per month** and includes **one member**.
* **Premium** costs **$65 per site per month** plus **$12 per member per month**.
* **Ultimate** costs **$249 per site per month** plus **$12 per member per month**.
* **Enterprise** uses custom pricing and billing terms.

For paid self-serve plans, we bill your site plan and current member count when the plan starts and when it renews.

If you add or remove members during a billing period, we calculate a prorated adjustment and apply it to your next invoice unless an annual true-up applies.

If you pay annually and your subscription increases during the term, we bill that increase as part of your annual true-up. This can be issued on a separate invoice before your next renewal.

{% hint style="info" %}
This page covers current billing only. If you’re on retired pricing, see [Legacy pricing](legacy-plans.md).
{% endhint %}

{% hint style="info" %}
Review our [terms of service](https://gitbook.com/docs/policies/terms), especially the section on [payment](https://gitbook.com/docs/policies/terms#id-3.-payment-terms).
{% endhint %}

## Pro rata pricing example

Let’s say you start **Premium** on **April 7** with **six members** and monthly billing.

Your monthly price is **$65** for the site plus **6 × $12** for members. That totals **$137 per month**.

On **April 17**, you add two members, bringing the total to eight. With **20 days** left in a **30-day** billing period, the prorated member charge is **2 × $12 × 20 / 30 = $16**. We add that **$16** adjustment to your next invoice.

On **April 27**, you remove one member, bringing the total to seven. With **10 days** left in the billing period, the prorated credit is **1 × $12 × 10 / 30 = $4**. We apply that **$4** credit to your next invoice.

On **May 7**, your next invoice includes:

1. **$149** for the new billing period. This is **$65** for Premium and **7 × $12** for members.
2. A **$16** prorated charge for the two members you added on April 17.
3. A **-$4** prorated credit for the member you removed on April 27.

Your total on **May 7** is **$161**.

{% hint style="info" %}
This example shows member proration on a paid self-serve plan. If you change your site plan mid-cycle, we calculate the adjustment using the same prorated approach.
{% endhint %}

## Charges

For self-serve plans, billing is handled through Stripe. GitBook doesn’t store sensitive payment information, and you can manage your billing details through the billing dashboard.

Enterprise billing follows the terms in your contract and can include invoicing.

For paid self-serve plans, we charge your payment method on file in these cases:

1. When you start a paid plan.
2. On your monthly or annual renewal date. This invoice can include your current site plan, your current member count, and any prorated adjustments from the previous period.
3. If you pay annually and your subscription increases during the term, we bill that increase through an annual true-up. This can be issued on an additional invoice before renewal.

### Invoices

Your invoice history is available in Stripe from your organization settings under **Billing**. You can review the summary for each invoice there and download invoices by date.
