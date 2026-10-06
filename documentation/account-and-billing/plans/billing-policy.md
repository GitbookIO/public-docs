# Billing policy

This policy covers GitBook’s current [plans](./).

Our billing model combines site pricing and member pricing. Prices depend on whether you pay annually or monthly:

| Plan       | Annual billing                             | Monthly billing                            |
| ---------- | ------------------------------------------ | ------------------------------------------ |
| Free       | $0 per site/month, one member              | $0 per site/month, one member              |
| Essential  | $65 per site/month + $12 per member/month  | $79 per site/month + $15 per member/month  |
| Ultimate   | $249 per site/month + $12 per member/month | $299 per site/month + $15 per member/month |
| Enterprise | Custom pricing and billing terms           | Custom pricing and billing terms           |

For the latest prices, see our [pricing page](https://www.gitbook.com/pricing).

AI features use [AI credits](ai-credits.md). Essential and Ultimate sites include a monthly credit allowance, and you can add a monthly credit pack if you need more.

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

Let’s say you start **Essential** on **April 7** with **six members** and monthly billing.

Your monthly price is **$79** for the site plus **6 × $15** for members. That totals **$169 per month**.

On **April 17**, you add two members, bringing the total to eight. With **20 days** left in a **30-day** billing period, the prorated member charge is **2 × $15 × 20 / 30 = $20**. We add that **$20** adjustment to your next invoice.

On **April 27**, you remove one member, bringing the total to seven. With **10 days** left in the billing period, the prorated credit is **1 × $15 × 10 / 30 = $5**. We apply that **$5** credit to your next invoice.

On **May 7**, your next invoice includes:

1. **$184** for the new billing period. This is **$79** for Essential and **7 × $15** for members.
2. A **$20** prorated charge for the two members you added on April 17.
3. A **-$5** prorated credit for the member you removed on April 27.

Your total on **May 7** is **$199**.

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
4. Every month for AI credit packs and AI usage, including on annual plans. In your renewal month, these appear on the same invoice as your site and member charges.

### Invoices

Your invoice history is available in Stripe from your organization settings under **Billing**. You can review the summary for each invoice there and download invoices by date.
