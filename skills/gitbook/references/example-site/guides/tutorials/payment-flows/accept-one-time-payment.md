---
icon: cart-shopping
description: Build a working checkout that takes a real test payment in under an hour.
---

# Accept a one-time payment with Checkout

By the end of this tutorial you'll have a working checkout flow — a buyer clicks **Pay**, a hosted Evolve page collects card details, a real test payment lands in your dashboard, and your server gets a webhook event. The whole build takes about 45 minutes.

This is the right starting point if you've never integrated payments before, or if you're prototyping a new flow.

{% hint style="info" %}
**Prerequisites.** A test API key from [dashboard.test.evolve.com](https://gitbook.com), a server that can accept HTTPS requests, and either Node or Python on your machine. If you don't have a server yet, [ngrok](https://ngrok.com) plus a tiny Express app is fine.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=55oOB-lsQKY" %}

## Build it

{% stepper %}
{% step %}

### Install the SDK

Pick your language:

{% tabs %}
{% tab title="Node" %}
```bash
npm install @evolve/node express
```
{% endtab %}

{% tab title="Python" %}
```bash
pip install evolve flask
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Create a Checkout session on your server

When the buyer clicks **Pay** on your site, your server creates a Checkout session and returns the URL.

{% tabs %}
{% tab title="Node" %}
```js
import Evolve from "@evolve/node";
import express from "express";

const evolve = new Evolve(process.env.EVOLVE_SECRET_KEY);
const app = express();

app.post("/checkout", async (req, res) => {
  const session = await evolve.checkoutSessions.create({
    amount: 4200,
    currency: "usd",
    description: "Order #1042",
    success_url: "https://yourapp.com/thanks?session={CHECKOUT_SESSION_ID}",
    cancel_url: "https://yourapp.com/cart",
  });
  res.json({ url: session.url });
});
```
{% endtab %}

{% tab title="Python" %}
```python
import os
import evolve
from flask import Flask, jsonify

evolve.api_key = os.environ["EVOLVE_SECRET_KEY"]
app = Flask(__name__)

@app.post("/checkout")
def checkout():
    session = evolve.CheckoutSession.create(
        amount=4200,
        currency="usd",
        description="Order #1042",
        success_url="https://yourapp.com/thanks?session={CHECKOUT_SESSION_ID}",
        cancel_url="https://yourapp.com/cart",
    )
    return jsonify(url=session.url)
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Redirect the buyer

In your front-end, send the buyer to `session.url`:

```html
<button id="pay">Pay $42.00</button>
<script>
document.getElementById("pay").addEventListener("click", async () => {
  const res = await fetch("/checkout", { method: "POST" });
  const { url } = await res.json();
  window.location.href = url;
});
</script>
```

The buyer lands on Evolve's hosted checkout, enters card details, and pays. Use test card `4242 4242 4242 4242` with any future expiry and any CVC.

{% endstep %}

{% step %}

### Add a webhook endpoint

Most production flows react to a webhook rather than relying on the redirect alone (buyers close tabs). Add an endpoint at **Developers → Webhooks → Add endpoint**, subscribe to `charge.succeeded`, and have your server handle it:

{% tabs %}
{% tab title="Node" %}
```js
app.post("/webhook", express.raw({ type: "application/json" }), (req, res) => {
  let event;
  try {
    event = evolve.webhooks.constructEvent(
      req.body,
      req.headers["evolve-signature"],
      process.env.EVOLVE_WEBHOOK_SECRET
    );
  } catch (err) {
    return res.status(400).send("Bad signature");
  }

  if (event.type === "charge.succeeded") {
    fulfillOrder(event.data.object);
  }
  res.json({ received: true });
});
```
{% endtab %}

{% tab title="Python" %}
```python
from flask import request

@app.post("/webhook")
def webhook():
    try:
        event = evolve.Webhook.construct_event(
            request.get_data(),
            request.headers.get("Evolve-Signature"),
            os.environ["EVOLVE_WEBHOOK_SECRET"],
        )
    except evolve.error.SignatureVerificationError:
        return "Bad signature", 400

    if event.type == "charge.succeeded":
        fulfill_order(event.data.object)
    return ""
```
{% endtab %}
{% endtabs %}

{% endstep %}

{% step %}

### Verify it end-to-end

Run your server, click **Pay**, complete the test checkout, and confirm:

1. The charge appears in **Payments → All payments** within a few seconds.
2. Your `success_url` fires with the session ID appended.
3. Your webhook handler logs the `charge.succeeded` event.
4. `fulfillOrder` runs once and only once (idempotency check on the event ID — see [Webhooks → Retries and replay](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/retries-and-replay)).

{% endstep %}
{% endstepper %}

## Common pitfalls

<details>

<summary>"My webhook signature verification keeps failing"</summary>

Almost always one of: body parsed before verification (use `express.raw` or equivalent), wrong signing secret (test vs live have different ones), or a proxy that's altering the body. See [Webhooks → Verifying signatures](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/verifying-signatures).

</details>

<details>

<summary>"Buyers see a generic descriptor on their statement"</summary>

Set your statement descriptor in **Settings → Billing → Statement descriptor**. The default is your registered business name truncated to 22 characters; that's often unrecognizable to customers. Use a brand name they'll recognize.

</details>

<details>

<summary>"The redirect works but I want a custom thank-you page"</summary>

Pass a `success_url` that points at your own page; you can include `{CHECKOUT_SESSION_ID}` as a placeholder and Evolve fills it in. On that page, retrieve the session server-side to confirm the charge succeeded — never trust the redirect alone for fulfillment.

</details>

## What's next

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-bookmark" style="color:$primary;">:bookmark:</i></h3></td><td><strong>Save cards for repeat customers</strong></td><td>Charge the same buyer again later.</td><td><a href="save-cards.md">save-cards.md</a></td></tr><tr><td><h3><i class="fa-shield-halved" style="color:$primary;">:shield-halved:</i></h3></td><td><strong>Set up 3-D Secure</strong></td><td>Liability shift on high-value charges.</td><td><a href="3d-secure.md">3d-secure.md</a></td></tr><tr><td><h3><i class="fa-shield-check" style="color:$primary;">:shield-check:</i></h3></td><td><strong>Prevent chargebacks</strong></td><td>Habits that cut dispute rates.</td><td><a href="chargeback-prevention.md">chargeback-prevention.md</a></td></tr></tbody></table>
