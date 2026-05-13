---
icon: rocket
description: Take your first test payment from the dashboard — no integration required.
---

# Accept your first payment

The fastest way to see Evolve work is to send a payment link, pay it yourself with a test card, and watch it land in your dashboard. You don't need to write any code.

{% hint style="info" %}
This walkthrough uses test mode. Test charges are real, but no money moves and nothing leaves the test environment.
{% endhint %}

{% stepper %}
{% step %}

### Open the test dashboard

Sign in to <a href="https://gitbook.com"><code class="expression">space.vars.dashboard_test</code></a>. If you've just created your account, you'll land in test mode by default — you can tell by the **Test** badge in the top bar.

<figure><img src="../.gitbook/assets/dashboard-test-badge.png" alt="The Evolve dashboard showing a Test mode badge in the header"><figcaption><p>Look for the Test badge in the top bar.</p></figcaption></figure>

{% endstep %}

{% step %}

### Create a payment link

Go to **Payments → Payment links** and click **New link**. Set:

* **Amount** — `$42.00`
* **Description** — `First test payment`
* **Methods** — leave the defaults

Click **Create**. Evolve generates a hosted checkout URL you can share with anyone — no integration on your side.

{% endstep %}

<figure><img src="../.gitbook/assets/payment-link-created.png" alt="A created payment link with a Copy button"><figcaption></figcaption></figure>

{% step %}

### Pay it with a test card

Open the payment link in a new tab. On the hosted checkout, use one of these test cards:

| Card | Number | Result |
| --- | --- | --- |
| Visa | `4242 4242 4242 4242` | Approved |
| Visa | `4000 0000 0000 0002` | Declined (`card_declined`) |
| Mastercard | `5555 5555 5555 4444` | Approved |
| Visa (3-D Secure required) | `4000 0027 6000 3184` | Approved after authentication |

Use any future expiry date and any 3-digit CVC.

{% endstep %}

{% step %}

### See it land in the dashboard

Back in the dashboard, the new charge appears at the top of **Payments → All payments**. Click it to see the full timeline — when the link was opened, when the card was approved, and when the funds were captured.

{% endstep %}

{% step %}

### Refund it

From the charge page, click **Refund**. You can refund the full amount or a partial amount. The refund appears as a separate row in the timeline and as a deduction on the next [settlement file](../reconciliation/settlement-files.md).

{% endstep %}
{% endstepper %}

## What's next?

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-toggle-on" style="color:$primary;">:toggle-on:</i></h3></td><td><strong>Switch to live mode</strong></td><td>What changes when you flip the switch.</td><td><a href="test-and-live-mode.md">test-and-live-mode.md</a></td></tr><tr><td><h3><i class="fa-circle-dollar-to-slot" style="color:$primary;">:circle-dollar-to-slot:</i></h3></td><td><strong>Take payments at scale</strong></td><td>Beyond payment links: Checkout, Elements, the API.</td><td><a href="../accept-payments/take-a-payment.md">take-a-payment.md</a></td></tr><tr><td><h3><i class="fa-bolt" style="color:$primary;">:bolt:</i></h3></td><td><strong>Set up a webhook</strong></td><td>React to payment events automatically.</td><td><a href="https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks">README.md</a></td></tr></tbody></table>

{% hint style="info" %}
**Building an integration?** Developers / [Payments API quickstart](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/payments-api) covers the same flow with code samples in cURL, Node, Python, Go, and Ruby.

<p><button type="button" class="button primary" data-action="ask" data-query="How do I integrate Evolve Payments with my own checkout?" data-icon="code">Ask the docs</button></p>
{% endhint %}
