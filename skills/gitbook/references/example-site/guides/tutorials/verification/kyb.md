---
icon: briefcase
description: Verify a business and its beneficial owners — the KYB flow end to end.
---

# Verify a business (KYB)

By the end of this tutorial you'll have a KYB flow that collects business info, identifies beneficial owners, runs identity verification on each owner, screens the business and owners against sanctions lists, and lands a single clean **Verified** status on your platform. The build takes about 2 hours.

This is for marketplaces onboarding business sellers, B2B platforms paying out to vendors, and any team that needs to verify a corporate entity before processing payments on its behalf.

{% hint style="info" %}
**Prerequisites.** An Evolve Enterprise account (KYB is Enterprise-only). Test API keys. Familiarity with the [Business verification](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/verification-flows/business) concept.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Create a KYB session

When the business operator starts onboarding, your server creates a KYB verification session and gets back a hosted URL:

{% tabs %}
{% tab title="Node" %}
```js
const session = await evolve.identity.verificationSessions.create({
  type: "business",
  return_url: "https://yourapp.com/verified",
  metadata: {
    internal_org_id: "org_42",
  },
});

res.json({ verifyUrl: session.url });
```
{% endtab %}

{% tab title="Python" %}
```python
session = evolve.VerificationSession.create(
    type="business",
    return_url="https://yourapp.com/verified",
    metadata={"internal_org_id": "org_42"},
)
return jsonify(verifyUrl=session.url)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Send the operator to the hosted form

The hosted form walks the operator through:

1. Legal name, registration country, EIN/equivalent.
2. Business address.
3. Officers and beneficial owners (anyone ≥25% ownership, plus controllers).
4. For each owner: name, DOB, address, ID.

This part takes the operator 5–10 minutes for a simple LLC. Complex ownership structures (holding companies, trusts) take longer.

{% hint style="info" %}
You can pre-fill any field your platform already knows. Pass values via `prefill: { ... }` on the session create — the operator can still edit, but they don't re-enter what you have.
{% endhint %}

{% endstep %}

{% step %}

### Verify each beneficial owner

The hosted form collects names; identity verification on each owner is automatic. Each owner gets an email with a verification link they complete on their own device — no need to be in the same place as the operator.

While owners are verifying, the session sits in `processing` state. You'll get one webhook per owner verification, and a final `verification_session.verified` (or `failed` / `manual_review`) when all owners are done.

{% endstep %}

{% step %}

### Run sanctions screening

Sanctions screening runs automatically as part of the KYB flow — both on the business entity and each beneficial owner. You don't trigger it separately.

If anything matches, the session goes to `manual_review`. Your compliance team reviews the match in the dashboard's **Identity → Disputes / Manual review** queue and either approves (false positive) or rejects.

{% endstep %}

{% step %}

### Listen for the final webhook

When the overall KYB completes, you get one event with the consolidated decision:

{% tabs %}
{% tab title="Node" %}
```js
if (event.type === "verification_session.verified" && event.data.object.type === "business") {
  await db.organizations.update(
    { kyb_session_id: event.data.object.id },
    { kyb_status: "verified", verified_at: new Date() }
  );
  enableHighValueFeatures(event.data.object.metadata.internal_org_id);
}
```
{% endtab %}

{% tab title="Python" %}
```python
if event.type == "verification_session.verified" and event.data.object.type == "business":
    db.organizations.update_where(
        kyb_session_id=event.data.object.id,
        values={"kyb_status": "verified", "verified_at": datetime.utcnow()},
    )
    enable_high_value_features(event.data.object.metadata["internal_org_id"])
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Set up ongoing monitoring

KYB isn't a one-shot check. Sanctions lists update daily and ownership changes. Subscribe to `screening.match_added` and surface a banner in the operator's dashboard when it fires:

> A new sanctions match was added for one of your verified owners. Compliance review in progress.

While the match is reviewed, hold any pending payouts to the business. This is automatic if you've set the right policy in **Settings → Connect → On sanctions match**.

{% endstep %}

{% step %}

### Test with the sanctions fixture

Test mode includes a fixture business named "Test Sanctioned Inc." that triggers a sanctions match. Run a KYB against it to confirm your manual-review queue catches it and your downstream policy (payout hold, alert email, etc.) fires correctly.

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"KYB takes 5+ business days for one of our customers"</summary>

Usually means an owner hasn't completed their identity verification. Check the session — it shows per-owner status. The bottleneck is almost always one owner who hasn't clicked their email link. Have your operator follow up directly.

</details>

<details>

<summary>"Sanctions screening flagged someone with a common name"</summary>

False-positive rate on sanctions matches at the medium-confidence threshold is real (think: any John Smith). The dashboard's manual-review tool shows the matched-list entry and the verified person side by side; your compliance reviewer marks false positive with a reason and the verification proceeds. Every override is logged in the audit trail.

</details>

<details>

<summary>"We onboard businesses from countries Evolve hasn't mentioned"</summary>

Coverage is broader than the listed countries — most non-US registries are supported on a case-by-case basis. Talk to your account team before launching in a new country; they'll confirm coverage and pre-emptively flag any region-specific rules.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-id-card" style="color:$primary;">:id-card:</i></h3></td><td><strong>Identity verification on sign-up</strong></td><td>The same flow for individual customers.</td><td><a href="identity-on-signup.md">identity-on-signup.md</a></td></tr><tr><td><h3><i class="fa-user-plus" style="color:$primary;">:user-plus:</i></h3></td><td><strong>Onboard your first sellers</strong></td><td>KYB plus the rest of Connect onboarding.</td><td><a href="../marketplace/onboard-sellers.md">onboard-sellers.md</a></td></tr><tr><td><h3><i class="fa-rotate-right" style="color:$primary;">:rotate-right:</i></h3></td><td><strong>Re-verification trigger</strong></td><td>Re-run KYB when ownership changes.</td><td><a href="re-verification-trigger.md">re-verification-trigger.md</a></td></tr></tbody></table>
