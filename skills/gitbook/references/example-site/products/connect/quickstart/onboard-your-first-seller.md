---
icon: rocket
description: Onboard a test seller, take a payment, and watch the split land in two accounts.
---

# Onboard your first seller

The fastest way to see Connect work is to onboard a test seller, take a single payment, and watch the application fee and seller payout land in the dashboard. The whole walkthrough takes about ten minutes.

{% hint style="info" %}
This walkthrough uses test mode. Test sellers, test payments, and test payouts are all real API objects — but no money moves and nothing leaves the test environment.
{% endhint %}

{% stepper %}
{% step %}

### Open the test dashboard

Sign in to <a href="https://gitbook.com"><code class="expression">space.vars.dashboard_test</code></a> and click into **Connect** in the left sidebar.

{% endstep %}

{% step %}

### Create a connected account

Go to **Connect → Connected accounts** and click **New account**. Set:

* **Account type** — `individual` (the default for the demo)
* **Country** — `United States`
* **Email** — your test email

Click **Send onboarding link**. Evolve generates a hosted onboarding URL and emails it to the address you entered.

{% endstep %}

{% step %}

### Complete onboarding as the seller

Open the onboarding email and click the link. The hosted flow walks the seller through:

1. Personal info (name, address, DOB).
2. Identity verification (test fixture passes by default).
3. A test bank account for payouts (use routing `110000000` and account `000123456789`).

Submit. The account moves to **Verified** in your dashboard within seconds.

{% endstep %}

{% step %}

### Take a payment

Back in your dashboard, find the new connected account and click **Take a test payment**. Set:

* **Amount** — `$100.00`
* **Application fee** — `$2.00` (the default 2%)
* **Card** — use the test card `4242 4242 4242 4242`

Click **Charge**. The payment succeeds. The dashboard shows two related entries:

* **Charge** of $100.00 against the buyer's card.
* **Transfer** of $98.00 to the seller's connected account.

The remaining $2.00 is your application fee.

{% endstep %}

{% step %}

### Trigger a payout

Sellers receive payouts on a schedule (daily, weekly, monthly), but you can trigger one on demand for testing. From the seller's account page, click **Pay out now**. The $98.00 lands in the test bank account immediately.

In live mode, the payout would appear in the seller's bank within 1–3 business days depending on your plan and the seller's country.

{% endstep %}
{% endstepper %}

## What happened in the dashboard

Two pages worth knowing about:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-store" style="color:$primary;">:store:</i></h3></td><td><strong>Connected accounts</strong></td><td>Every seller, with their onboarding status, payout schedule, and balance.</td><td></td></tr><tr><td><h3><i class="fa-list" style="color:$primary;">:list:</i></h3></td><td><strong>Platform feed</strong></td><td>Every charge, transfer, application fee, and payout across all sellers.</td><td></td></tr></tbody></table>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-toggle-on" style="color:$primary;">:toggle-on:</i></h3></td><td><strong>Switch to live mode</strong></td><td>What changes when you flip the switch.</td><td><a href="test-and-live-mode.md">test-and-live-mode.md</a></td></tr><tr><td><h3><i class="fa-window-maximize" style="color:$primary;">:window-maximize:</i></h3></td><td><strong>Add a checkout</strong></td><td>Hosted, embedded, or fully custom buyer experience.</td><td><a href="../embedded-checkout/README.md">README.md</a></td></tr><tr><td><h3><i class="fa-percent" style="color:$primary;">:percent:</i></h3></td><td><strong>Configure splits</strong></td><td>Application fees, flat fees, and conditional rules.</td><td><a href="../platform-setup/splitting-payments.md">splitting-payments.md</a></td></tr></tbody></table>
