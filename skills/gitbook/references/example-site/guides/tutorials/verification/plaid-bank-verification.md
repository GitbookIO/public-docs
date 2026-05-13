---
icon: building-columns
description: Verify a customer's bank account with Plaid instant — with micro-deposits as fallback.
---

# Connect a bank account with Plaid

By the end of this tutorial you'll have a bank-account verification flow that uses Plaid instant for ~70% of customers and falls back to micro-deposits for the rest, with a single user-facing UX. The build takes about 60 minutes.

This is the right pattern any time you need a verified bank account — to debit ACH, to send a payout, or to onboard a marketplace seller.

{% hint style="info" %}
**Prerequisites.** A Growth or Enterprise account (bank verification isn't on Starter). Test API keys. A working customer onboarding flow.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Create a bank verification session

Set `method: "auto"` to enable the Plaid-first-with-fallback pattern:

{% tabs %}
{% tab title="Node" %}
```js
const verification = await evolve.identity.bankVerifications.create({
  customer: "cus_4n2P3qR5sT6uV",
  method: "auto",
  return_url: "https://yourapp.com/bank-verified",
});

res.json({ verifyUrl: verification.url });
```
{% endtab %}

{% tab title="Python" %}
```python
verification = evolve.BankVerification.create(
    customer="cus_4n2P3qR5sT6uV",
    method="auto",
    return_url="https://yourapp.com/bank-verified",
)
return jsonify(verifyUrl=verification.url)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Send the customer to the hosted flow

The customer clicks through to a hosted page that:

1. Shows a list of supported banks (Plaid coverage).
2. The customer either picks their bank (→ Plaid flow) or clicks "My bank isn't here" (→ micro-deposits flow).
3. Plaid customers complete in 30–60 seconds. Micro-deposits customers enter routing + account numbers and come back in 1–2 days to confirm amounts.

{% endstep %}

{% step %}

### Listen for the verified webhook

For Plaid, you get the result within seconds. For micro-deposits, 1–2 business days later (after the deposits land and the customer confirms):

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "bank_verification.verified") {
  const v = event.data.object;
  await db.bankAccounts.create({
    customer_id: v.customer,
    method: v.method,
    last4: v.account_last4,
    routing: v.routing,
    bank_name: v.bank_name,
    verified_at: new Date(),
  });
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "bank_verification.verified":
    v = event.data.object
    db.bank_accounts.create(
        customer_id=v.customer,
        method=v.method,
        last4=v.account_last4,
        routing=v.routing,
        bank_name=v.bank_name,
        verified_at=datetime.utcnow(),
    )
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Use the verified account

Once verified, the bank account is attached to the customer. To debit it via ACH:

{% tabs %}
{% tab title="Node" %}
```js
const charge = await evolve.charges.create({
  amount: 50000,
  currency: "usd",
  customer: "cus_4n2P3qR5sT6uV",
  payment_method_type: "ach_debit",
  description: "Subscription renewal",
});
```
{% endtab %}

{% tab title="Python" %}
```python
charge = evolve.Charge.create(
    amount=50000,
    currency="usd",
    customer="cus_4n2P3qR5sT6uV",
    payment_method_type="ach_debit",
    description="Subscription renewal",
)
```
{% endtab %}
{% endtabs %}

For Connect payouts, just attach the account to the connected account during onboarding — Evolve handles the rest.

{% endstep %}

{% step %}

### Handle the failure cases

Three failure modes:

* **Plaid auth failed** — customer's online banking creds didn't work. The flow auto-falls back to micro-deposits.
* **Routing/account invalid** — wrong numbers entered. `bank_verification.failed` fires; show the customer a retry path.
* **Customer abandoned** — didn't return for micro-deposits. After 7 days, the verification expires; `bank_verification.expired` fires. Email them a fresh link if they haven't completed.

{% endstep %}

{% step %}

### Test in test mode

Test mode includes:

| Test scenario | How to trigger |
| --- | --- |
| Plaid happy path | Pick "Test Bank" in the institution list, use creds `user_good` / `pass_good`. |
| Plaid auth failure | Pick "Test Bank", use creds `user_good` / `wrong`. Falls back to micro-deposits. |
| Micro-deposits success | Use routing `110000000` and any 9-digit account; the test deposits "land" instantly. |
| Micro-deposits failure | Use routing `123456789` (invalid). |

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Customers complete the flow but the webhook fires hours later for Plaid"</summary>

Plaid is fast for the supported banks but slower (~10–30 minutes) for some smaller institutions. Don't treat the redirect-back as confirmation; rely on the webhook. Show a "verifying…" state in your UI when the customer returns, transitioning to "verified" only when the webhook lands.

</details>

<details>

<summary>"Some customers never see Plaid — they go straight to micro-deposits"</summary>

Plaid's bank list is region-aware. US customers see most major banks; EU/UK customers see a much smaller list. For international customers, micro-deposits or open-banking flows specific to their region are the path. Configure regional methods in **Settings → Identity → Bank verification → Regions**.

</details>

<details>

<summary>"Why did a $1.00 micro-deposit show up on my customer's bank statement before they verified?"</summary>

That's the verification step — those deposits are how we prove the customer owns the account. They're refundable; in test mode they don't move money. In live mode the total cost (deposits + fee) is the per-verification charge.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-id-card" style="color:$primary;">:id-card:</i></h3></td><td><strong>Identity verification on sign-up</strong></td><td>Verify the person before debiting their account.</td><td><a href="identity-on-signup.md">identity-on-signup.md</a></td></tr><tr><td><h3><i class="fa-user-plus" style="color:$primary;">:user-plus:</i></h3></td><td><strong>Onboard your first sellers</strong></td><td>For Connect, bank verification is part of onboarding.</td><td><a href="../marketplace/onboard-sellers.md">onboard-sellers.md</a></td></tr><tr><td><h3><i class="fa-arrows-rotate" style="color:$primary;">:arrows-rotate:</i></h3></td><td><strong>Subscription billing</strong></td><td>ACH-backed subscriptions are a common pattern.</td><td><a href="../payment-flows/subscription-billing.md">subscription-billing.md</a></td></tr></tbody></table>
