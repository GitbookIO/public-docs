---
icon: user-plus
description: Onboard sellers onto your marketplace with the hosted Connect onboarding flow.
---

# Onboard your first sellers

By the end of this tutorial you'll have a working seller onboarding flow — your platform sends an invite, the seller completes a hosted form (legal info, identity, banking), and they're ready to take payments through your marketplace. The build takes about 90 minutes.

This is the right starting point for any marketplace, B2B platform, or vertical SaaS that takes payments on behalf of customers.

{% hint style="info" %}
**Prerequisites.** A Growth or Enterprise account with Connect enabled. Test API keys. Read [Connect → Onboarding sellers](https://app.gitbook.com/s/Xtfxb7OHGyrdfIsObmnu/platform-setup/onboarding-sellers) for the conceptual model.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Create a connected account

When a seller signs up to your marketplace, your server creates a connected account and gets back a hosted onboarding URL:

{% tabs %}
{% tab title="Node" %}
```js
const account = await evolve.connect.connectedAccounts.create({
  type: "individual",
  country: "US",
  email: req.body.sellerEmail,
  metadata: {
    internal_seller_id: seller.id,
  },
});

await db.sellers.update(seller.id, {
  evolve_account_id: account.id,
  onboarding_status: "pending",
});

res.json({ onboardingUrl: account.onboarding_url });
```
{% endtab %}

{% tab title="Python" %}
```python
account = evolve.ConnectedAccount.create(
    type="individual",
    country="US",
    email=request.json["seller_email"],
    metadata={"internal_seller_id": seller.id},
)

db.sellers.update(
    seller.id,
    evolve_account_id=account.id,
    onboarding_status="pending",
)

return jsonify(onboardingUrl=account.onboarding_url)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Send the seller to the hosted flow

The hosted flow walks the seller through:

1. Personal info (legal name, DOB, address).
2. Government-issued ID (document + selfie).
3. Bank account for payouts (Plaid or micro-deposits).
4. Tax form (W-9 for US individuals, W-8 for international).

Most US individuals complete in under 10 minutes.

{% endstep %}

{% step %}

### Listen for the verification webhook

The full account-verified webhook fires when all the steps are done:

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "account.verified") {
  const account = event.data.object;
  await db.sellers.update(
    { evolve_account_id: account.id },
    {
      onboarding_status: "verified",
      can_charge: account.capabilities.charges_enabled,
      can_payout: account.capabilities.payouts_enabled,
    }
  );
  notifySellerActivated(account.metadata.internal_seller_id);
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "account.verified":
    account = event.data.object
    db.sellers.update_where(
        evolve_account_id=account.id,
        values={
            "onboarding_status": "verified",
            "can_charge": account.capabilities["charges_enabled"],
            "can_payout": account.capabilities["payouts_enabled"],
        },
    )
    notify_seller_activated(account.metadata["internal_seller_id"])
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Surface the seller's status in your UI

Sellers have one of five states. Show this clearly in their dashboard:

| State | Meaning | What seller can do |
| --- | --- | --- |
| `pending` | Onboarding link sent, not yet started | Click the link |
| `incomplete` | Started, missing some required info | Resume onboarding |
| `processing` | Submitted, Evolve is reviewing | Nothing — wait |
| `verified` | All checks passed | Take payments, receive payouts |
| `restricted` | Risk team has restricted the account | Contact you for next steps |

Provide a "Resume onboarding" button for `incomplete` accounts that re-generates a hosted URL.

{% endstep %}

{% step %}

### Handle requirement updates

Onboarding occasionally needs more info — a clearer ID photo, a tax form, address verification. When this happens, the `account.requirements_updated` event fires:

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "account.requirements_updated") {
  const account = event.data.object;
  if (account.requirements.currently_due.length > 0) {
    notifySeller(
      account.metadata.internal_seller_id,
      "additional_info_needed",
      { url: account.onboarding_url }
    );
  }
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "account.requirements_updated":
    account = event.data.object
    if account.requirements["currently_due"]:
        notify_seller(
            account.metadata["internal_seller_id"],
            "additional_info_needed",
            url=account.onboarding_url,
        )
```
{% endtab %}
{% endtabs %}

The `onboarding_url` on the account is always valid — it deep-links the seller back to whatever's missing.

{% endstep %}

{% step %}

### Test the verification fixtures

Test mode includes fixtures for each end-state:

| Email used | Result |
| --- | --- |
| `pass@example.com` | Verifies on first submit |
| `manual_review@example.com` | Goes to manual review (admin must approve in dashboard) |
| `requirements_due@example.com` | Onboards with `currently_due` populated |
| `restricted@example.com` | Restricted (risk-flagged) |

Walk through each. Confirm your UI handles all four states.

{% endstep %}

{% step %}

### Pre-fill what you already know

Most platforms collect some of the seller's info during sign-up. Pre-fill it:

{% tabs %}
{% tab title="Node" %}
```js
const account = await evolve.connect.connectedAccounts.create({
  type: "individual",
  country: "US",
  email: seller.email,
  prefill: {
    legal_name: seller.full_name,
    address: seller.business_address,
    dob: seller.date_of_birth,
  },
  metadata: { internal_seller_id: seller.id },
});
```
{% endtab %}

{% tab title="Python" %}
```python
account = evolve.ConnectedAccount.create(
    type="individual",
    country="US",
    email=seller.email,
    prefill={
        "legal_name": seller.full_name,
        "address": seller.business_address,
        "dob": seller.date_of_birth,
    },
    metadata={"internal_seller_id": seller.id},
)
```
{% endtab %}
{% endtabs %}

The seller can still edit; pre-fill just saves typing.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Sellers don't return after we send the email"</summary>

Most-cited cause: the email looked transactional and got buried. Send it from a recognizable name (not `noreply@`), use a clear subject ("Finish setting up your seller account"), and put the CTA button above the fold. After 24 hours, send a follow-up. After 7 days, archive the lead — onboarding-incomplete sellers rarely resurrect.

</details>

<details>

<summary>"My seller's account is `verified` but `payouts_enabled` is false"</summary>

That means identity passed but bank verification didn't. Check `requirements.currently_due` — usually they need to complete the bank step (Plaid auth failed or micro-deposits never confirmed). Send them back to the onboarding URL.

</details>

<details>

<summary>"How do I verify business sellers (LLCs, corporations)?"</summary>

Use `type: "company"` instead of `"individual"`. The flow extends with KYB — beneficial-ownership collection and business sanctions screening. See [Verify a business (KYB)](../verification/kyb.md) for the deeper walkthrough.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-percent" style="color:$primary;">:percent:</i></h3></td><td><strong>Split each payment</strong></td><td>Application fees and conditional rules.</td><td><a href="split-payments.md">split-payments.md</a></td></tr><tr><td><h3><i class="fa-money-bill-transfer" style="color:$primary;">:money-bill-transfer:</i></h3></td><td><strong>Per-seller payout schedules</strong></td><td>Daily, weekly, monthly, on-demand.</td><td><a href="payout-schedules.md">payout-schedules.md</a></td></tr><tr><td><h3><i class="fa-code" style="color:$primary;">:code:</i></h3></td><td><strong>Custom onboarding flow</strong></td><td>When the hosted flow isn't enough.</td><td><a href="custom-onboarding.md">custom-onboarding.md</a></td></tr></tbody></table>
