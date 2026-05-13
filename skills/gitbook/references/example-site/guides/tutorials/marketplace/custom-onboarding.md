---
icon: code
description: Build seller onboarding entirely in your own UI — programmatic field collection without the hosted flow.
---

# Build a custom Connect onboarding flow

By the end of this tutorial you'll have a fully white-labeled seller onboarding flow — your own forms, your own URL, your own branding — that programmatically submits seller data to Evolve and handles the verification responses. The build takes about 4 hours.

This is for platforms with strong brand standards or specific UX needs the hosted flow doesn't cover. Most platforms shouldn't take this path — it's more work and the hosted flow keeps pace with regulatory changes automatically. But for platforms where it matters, here's how.

{% hint style="warning" %}
**Custom onboarding is more compliance-sensitive than hosted.** With hosted onboarding, Evolve handles regional variations and regulatory updates automatically. With custom, your code is on the hook. Make sure you have someone on your team who can keep up with KYC rule changes.
{% endhint %}

{% hint style="info" %}
**Prerequisites.** [Onboard your first sellers](onboard-sellers.md) finished — to understand what the hosted flow does. Enterprise account (custom onboarding is Enterprise-only). Your platform has a designer and at least one engineer with PCI-aware experience.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Create the connected account in custom mode

Pass `onboarding_mode: "custom"` so Evolve doesn't generate a hosted URL:

{% tabs %}
{% tab title="Node" %}
```js
const account = await evolve.connect.connectedAccounts.create({
  type: "individual",
  country: "US",
  email: seller.email,
  onboarding_mode: "custom",
  metadata: { internal_seller_id: seller.id },
});

await db.sellers.update(seller.id, {
  evolve_account_id: account.id,
  onboarding_status: "started",
});
```
{% endtab %}

{% tab title="Python" %}
```python
account = evolve.ConnectedAccount.create(
    type="individual",
    country="US",
    email=seller.email,
    onboarding_mode="custom",
    metadata={"internal_seller_id": seller.id},
)

db.sellers.update(
    seller.id,
    evolve_account_id=account.id,
    onboarding_status="started",
)
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://api.evolve.com/v2/connected_accounts \
  -H "Authorization: Bearer $EVOLVE_SECRET_KEY" \
  -d type=individual \
  -d country=US \
  -d email=seller@example.com \
  -d onboarding_mode=custom \
  -d metadata[internal_seller_id]=42
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Submit the legal info

Build your own form for legal name, DOB, address, and tax ID. Submit each as you collect it (or in one batch):

{% tabs %}
{% tab title="Node" %}
```js
await evolve.connect.connectedAccounts.update(account.id, {
  individual: {
    first_name: form.firstName,
    last_name: form.lastName,
    dob: form.dob,                // "1985-04-12"
    address: form.address,
    ssn_last_4: form.ssnLast4,
  },
});
```
{% endtab %}

{% tab title="Python" %}
```python
evolve.ConnectedAccount.modify(
    account.id,
    individual={
        "first_name": form["first_name"],
        "last_name": form["last_name"],
        "dob": form["dob"],
        "address": form["address"],
        "ssn_last_4": form["ssn_last_4"],
    },
)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Capture identity documents (the hard part)

This is where custom onboarding gets sensitive. You need to collect a government ID and a selfie, and you need to do it without your servers ever touching the raw image — that would put you in PCI-equivalent compliance scope for ID data.

Use Evolve's secure-upload widget, which embeds a managed upload UI in an iframe. The image goes from the customer's browser straight to Evolve's servers; your code never sees the bytes:

```html
<div id="evolve-id-upload"></div>
<script src="https://js.evolve.com/v1/identity.js"></script>
<script>
  const evolve = Evolve('pk_live_...');
  evolve.mountIdentityUpload('#evolve-id-upload', {
    accountId: 'acct_3KsM12pL9q',
    onComplete: (result) => {
      // result.documentId is the reference; submit to your server
      submitToServer(result.documentId);
    },
  });
</script>
```

Your server receives the document ID and attaches it to the connected account:

{% tabs %}
{% tab title="Node" %}
```js
await evolve.connect.connectedAccounts.update(account.id, {
  individual: {
    verification: {
      document: documentId,
    },
  },
});
```
{% endtab %}

{% tab title="Python" %}
```python
evolve.ConnectedAccount.modify(
    account.id,
    individual={"verification": {"document": document_id}},
)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Submit bank info via Plaid Link

Same iframe-based pattern for the bank account. Mount Evolve's Plaid widget; your server receives the verified bank account ID:

```html
<div id="evolve-bank"></div>
<script>
  evolve.mountBankVerification('#evolve-bank', {
    accountId: 'acct_3KsM12pL9q',
    onComplete: (result) => {
      submitBankToServer(result.bankVerificationId);
    },
  });
</script>
```

For sellers without a Plaid-supported bank, you can collect routing + account directly in your form (no PCI scope for ACH numbers) and submit:

{% tabs %}
{% tab title="Node" %}
```js
await evolve.connect.connectedAccounts.update(account.id, {
  external_account: {
    object: "bank_account",
    country: "US",
    currency: "usd",
    routing_number: form.routingNumber,
    account_number: form.accountNumber,
  },
});
```
{% endtab %}

{% tab title="Python" %}
```python
evolve.ConnectedAccount.modify(
    account.id,
    external_account={
        "object": "bank_account",
        "country": "US",
        "currency": "usd",
        "routing_number": form["routing_number"],
        "account_number": form["account_number"],
    },
)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Trigger the verification

Once all required fields are submitted, request verification:

{% tabs %}
{% tab title="Node" %}
```js
await evolve.connect.connectedAccounts.requestVerification(account.id);
```
{% endtab %}

{% tab title="Python" %}
```python
evolve.ConnectedAccount.request_verification(account.id)
```
{% endtab %}
{% endtabs %}

The same `account.verified` / `account.requirements_updated` webhooks fire as in hosted mode.

{% endstep %}

{% step %}

### Handle requirements updates in your UI

When `account.requirements_updated` fires, your code parses `requirements.currently_due` and shows the seller exactly which fields to fix:

{% tabs %}
{% tab title="Node" %}
```js
function buildResumeFlow(account) {
  const due = account.requirements.currently_due;
  const steps = [];
  if (due.includes("individual.verification.document")) steps.push("upload_id");
  if (due.includes("individual.address")) steps.push("address");
  if (due.includes("external_account")) steps.push("bank_account");
  return steps;
}
```
{% endtab %}

{% tab title="Python" %}
```python
def build_resume_flow(account):
    due = account.requirements["currently_due"]
    steps = []
    if "individual.verification.document" in due:
        steps.append("upload_id")
    if "individual.address" in due:
        steps.append("address")
    if "external_account" in due:
        steps.append("bank_account")
    return steps
```
{% endtab %}
{% endtabs %}

This is the part of custom onboarding that's most ongoing-maintenance work — `currently_due` field names occasionally change as Evolve adds new requirements (especially internationally). Plan for quarterly review.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"Why did our PCI scope go up after switching to custom?"</summary>

It shouldn't have, if you're using the secure-upload widgets for ID documents. If you accidentally collected ID images on your own server, you're now in document-data compliance scope. Migrate to the iframe widget immediately — the bytes shouldn't have hit your server in the first place.

</details>

<details>

<summary>"Custom onboarding works in the US but breaks for international sellers"</summary>

International sellers have different required fields per country. Check `requirements.currently_due` per account; the names vary (`individual.id_number` for some countries, `individual.verification.document.front` for others). Build your form dynamically off the requirements list rather than hardcoding fields.

</details>

<details>

<summary>"Should we even be doing custom onboarding?"</summary>

Honestly, probably not unless: (1) your brand standards require it, (2) you have a compliance team that can keep up with KYC changes, (3) your seller cohort is concentrated in one country. The hosted flow handles regulatory variations automatically; custom is more work for the same outcome in most cases.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-user-plus" style="color:$primary;">:user-plus:</i></h3></td><td><strong>Hosted onboarding</strong></td><td>Compare against the hosted approach.</td><td><a href="onboard-sellers.md">onboard-sellers.md</a></td></tr><tr><td><h3><i class="fa-percent" style="color:$primary;">:percent:</i></h3></td><td><strong>Split payments</strong></td><td>Once sellers are verified, split each payment.</td><td><a href="split-payments.md">split-payments.md</a></td></tr><tr><td><h3><i class="fa-briefcase" style="color:$primary;">:briefcase:</i></h3></td><td><strong>Verify a business (KYB)</strong></td><td>For company sellers, the same custom-onboarding logic plus KYB.</td><td><a href="../verification/kyb.md">kyb.md</a></td></tr></tbody></table>
