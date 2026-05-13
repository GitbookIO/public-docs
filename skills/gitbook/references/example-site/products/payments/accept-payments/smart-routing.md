---
icon: route
description: Pick the route most likely to approve each payment — automatically.
---

# Smart routing

Most card payments can take more than one path to the issuer. Smart routing picks the path most likely to approve, based on the card's BIN, the transaction context, and historical success rates Evolve has observed across millions of payments.

For most teams, smart routing recovers 1–3% of payments that would otherwise be declined — without any code changes on your end.

{% if visitor.claims.unsigned.plan === "starter" %}

{% hint style="warning" icon="lock" %}
**Smart routing is a Growth and Enterprise feature.** Starter accounts use a single default acquirer per region. To enable smart routing, [upgrade your plan](https://gitbook.com).
{% endhint %}

{% endif %}

## What it does

For each card payment, Evolve evaluates:

* **Card BIN** — which issuer, which country, which network.
* **Transaction shape** — amount, currency, merchant category, customer history.
* **Acquirer history** — recent approval rates for similar cards on each available acquirer.

It then routes the payment through the acquirer with the best expected approval rate. If that acquirer declines with a soft decline (issuer unavailable, processing error), it can also retry through a backup acquirer — turning a near-miss into an approval.

{% hint style="info" %}
Smart routing only changes which acquirer processes the payment. It never changes the customer-facing flow, the receipt, or the funds path back to you.
{% endhint %}

## Turning it on

In **Settings → Routing**, toggle **Smart routing** on. The defaults are sensible — most teams don't customize further. Evolve picks acquirers from your existing acquirer agreements; it never adds a new processor without your sign-off.

You can override the defaults with rules:

| Condition | Action |
| --- | --- |
| Currency is `eur` and amount > €500 | Prefer acquirer A (lower interchange) |
| Card is American Express | Always use Amex direct |
| Customer is on a soft-decline retry | Allow up to 2 alternate acquirers |
| Merchant category is `subscription` | Skip retry on `do_not_honor` (avoid issuer annoyance) |

## How approvals improve

The biggest gains come from three sources:

<details>

<summary>Per-card-type acquirer affinity</summary>

Some acquirers have stronger relationships with certain issuers — they share more authorization data, get better fraud signals back, and approve more cards as a result. Smart routing picks the acquirer that's been winning the most lately for cards that look like the one in front of it.

</details>

<details>

<summary>Network token usage</summary>

When the card has a network token available (most US cards do), routing through an acquirer that supports network tokens lifts approval rates by ~1.5% on average. Smart routing takes this into account.

</details>

<details>

<summary>Soft-decline retry</summary>

About 0.4% of declines are "soft" — the issuer's auth system was momentarily unavailable, the network had a glitch, or the message was malformed somewhere in the chain. Smart routing retries those through a different acquirer within a few hundred milliseconds, often turning a decline into an approval before the customer notices.

</details>

## Watching it work

The dashboard shows the route Evolve picked for each payment on the timeline:

<figure><img src="../.gitbook/assets/payment-routing-timeline.png" alt="A payment timeline showing Smart routing picked Acquirer A, with a backup retry on Acquirer B"><figcaption><p>The routing decision and any retries appear in the payment timeline.</p></figcaption></figure>

For aggregate visibility, the **Routing report** under **Reports → Routing** shows per-acquirer approval rates over time, so you can see the lift from smart routing against your previous baseline.

## What it doesn't do

* Smart routing isn't a price-shopping engine. It optimizes for approval rate, not interchange. If you want to bias toward lower-interchange acquirers, configure that explicitly in the rules.
* It won't paper over a real decline. `insufficient_funds` and `card_declined` for fraud are honored as-is.
* It doesn't change which payment methods are offered. That's still configured under [Payment methods](../concepts/payment-methods.md).

## Related

* [Failover and retries](failover.md) — broader resilience to acquirer outages. *Enterprise.*
* [3-D Secure and SCA](3d-secure.md) — pairing 3DS with the most likely-to-approve route.
* [Routing report](../reporting/standard-reports.md#routing-report) — measuring the lift.
