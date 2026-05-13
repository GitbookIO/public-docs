---
icon: shield-halved
description: HMAC-SHA256 signature verification — in every supported language.
---

# Verifying signatures

Every webhook delivery includes an `Evolve-Signature` header. The signature is HMAC-SHA256 over the timestamp + the raw request body, signed with the endpoint's signing secret. Verify it before doing anything else with the request.

## The header format

```
Evolve-Signature: t=1714477200,v1=5257a869e7ecebeda32affa62cdca3fa51cad7e77a0e56ff536d0ce8e108d8bd
```

* `t` — Unix timestamp (seconds) when Evolve generated the signature.
* `v1` — the HMAC-SHA256 signature.

## The verification algorithm

```
signed_payload = "{t}.{raw_body}"
expected = HMAC_SHA256(signing_secret, signed_payload)
valid = constant_time_compare(expected, v1)
```

Three things to enforce:

1. **The signature matches.** Use a constant-time comparison.
2. **The timestamp is recent.** Reject anything older than 5 minutes (default tolerance).
3. **You're using the raw body.** Re-serializing JSON before verification breaks the signature.

## Verifying in code

The official SDKs ship a one-call helper. Use it.

{% tabs %}
{% tab title="Node" %}
```js
import express from "express";
import Evolve from "@evolve/node";

const evolve = new Evolve(process.env.EVOLVE_SECRET_KEY);
const app = express();

// IMPORTANT: get the raw body, not parsed JSON.
app.post("/webhook", express.raw({ type: "application/json" }), (req, res) => {
  const sig = req.headers["evolve-signature"];

  let event;
  try {
    event = evolve.webhooks.constructEvent(
      req.body,
      sig,
      process.env.EVOLVE_WEBHOOK_SECRET
    );
  } catch (err) {
    console.warn("Bad signature:", err.message);
    return res.status(400).send("Invalid signature");
  }

  // Handle the event.
  switch (event.type) {
    case "charge.succeeded": handleCharge(event.data.object); break;
    case "charge.failed":    handleFailure(event.data.object); break;
  }

  res.json({ received: true });
});
```
{% endtab %}

{% tab title="Python" %}
```python
from flask import Flask, request, jsonify
import evolve, os

evolve.api_key = os.environ["EVOLVE_SECRET_KEY"]
app = Flask(__name__)

@app.route("/webhook", methods=["POST"])
def webhook():
    payload = request.get_data(as_text=False)  # raw bytes, not parsed JSON
    sig = request.headers.get("Evolve-Signature")

    try:
        event = evolve.Webhook.construct_event(
            payload, sig, os.environ["EVOLVE_WEBHOOK_SECRET"]
        )
    except evolve.error.SignatureVerificationError:
        return "Invalid signature", 400

    if event.type == "charge.succeeded":
        handle_charge(event.data.object)

    return jsonify(received=True)
```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
    "io"
    "net/http"
    "os"

    "github.com/evolve-pay/evolve-go/webhook"
)

func handler(w http.ResponseWriter, r *http.Request) {
    body, err := io.ReadAll(r.Body)
    if err != nil {
        http.Error(w, "read failed", 400)
        return
    }

    event, err := webhook.ConstructEvent(
        body,
        r.Header.Get("Evolve-Signature"),
        os.Getenv("EVOLVE_WEBHOOK_SECRET"),
    )
    if err != nil {
        http.Error(w, "invalid signature", 400)
        return
    }

    switch event.Type {
    case "charge.succeeded":
        // ...
    }

    w.Write([]byte(`{"received":true}`))
}
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "sinatra"
require "evolve"

post "/webhook" do
  payload = request.body.read
  sig = request.env["HTTP_EVOLVE_SIGNATURE"]

  begin
    event = Evolve::Webhook.construct_event(
      payload, sig, ENV["EVOLVE_WEBHOOK_SECRET"]
    )
  rescue Evolve::SignatureVerificationError
    halt 400, "Invalid signature"
  end

  case event.type
  when "charge.succeeded"
    handle_charge(event.data.object)
  end

  status 200
  { received: true }.to_json
end
```
{% endtab %}

{% tab title="Manual (any language)" %}
```python
import hmac, hashlib, time

def verify(payload: bytes, sig_header: str, secret: str, tolerance: int = 300):
    parts = dict(p.split("=", 1) for p in sig_header.split(","))
    timestamp = int(parts["t"])

    # Reject stale signatures.
    if abs(time.time() - timestamp) > tolerance:
        raise ValueError("timestamp too old")

    signed = f"{timestamp}.".encode() + payload
    expected = hmac.new(secret.encode(), signed, hashlib.sha256).hexdigest()

    if not hmac.compare_digest(expected, parts["v1"]):
        raise ValueError("invalid signature")
```
{% endtab %}
{% endtabs %}

## Common pitfalls

<details>

<summary>"My signature verification fails on every request"</summary>

Almost always one of:

* **Body is parsed before verification.** Frameworks like Express, Flask, Rails default to parsing JSON. You need the raw bytes that arrived on the wire.
* **Wrong signing secret.** Each endpoint has its own. Test-mode and live-mode endpoints have different secrets too.
* **Wrong endpoint.** The dashboard shows what URL Evolve is sending to.

</details>

<details>

<summary>"Signature works locally but fails in production"</summary>

Check whether something in front of your server (nginx, a load balancer, a CDN) is rewriting the body — even adding a trailing newline breaks HMAC verification.

</details>

<details>

<summary>"I'm getting 'timestamp too old' errors"</summary>

Either your server's clock is way off NTP, or you're processing events that were buffered for more than 5 minutes (e.g. a backlog after an outage). Bump the tolerance for backlog processing, or reject and let Evolve retry — Evolve's retry will have a fresh timestamp.

</details>

## Rolling the signing secret

If you suspect the signing secret has leaked, roll it from **Developers → Webhooks → [endpoint] → Roll secret**. The new secret is active immediately; the old one keeps working for 24 hours so you have time to deploy.

## Related

* [Authentication](../getting-started/authentication.md) — for the outbound side (your requests to Evolve).
* [Retries and replay](retries-and-replay.md) — what happens when verification fails on your side.
* [Event catalog](event-catalog.md) — every event type Evolve sends.
