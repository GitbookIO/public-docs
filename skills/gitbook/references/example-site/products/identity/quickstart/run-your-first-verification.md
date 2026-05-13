---
icon: rocket
description: Run your first identity verification from the dashboard — no integration required.
---

# Run your first verification

The fastest way to see Identity work is to send a verification link, complete it yourself with test fixture data, and watch the result land in your dashboard. You don't need to write any code.

{% hint style="info" %}
This walkthrough uses test mode. Test verifications are real, but no documents are stored long-term and nothing leaves the test environment.
{% endhint %}

{% stepper %}
{% step %}

### Open the test dashboard

Sign in to <a href="https://gitbook.com"><code class="expression">space.vars.dashboard_test</code></a> and click into **Identity** in the left sidebar.

{% endstep %}

{% step %}

### Create a verification session

Go to **Identity → Verification sessions** and click **New session**. Set:

* **Type** — `identity` (the default)
* **Required checks** — leave defaults (document + selfie)
* **Subject** — your test email address

Click **Create**. Evolve generates a hosted verification URL — copy it.

{% endstep %}

{% step %}

### Complete the verification

Open the link in a new tab on a phone (the camera capture flow is mobile-first). On the hosted flow:

1. Pick a country and document type — choose **United States → Driver's license**.
2. Use the test image **`test-dl-front.jpg`** when asked to capture the front. Test images are linked at the bottom of the test-mode capture screen.
3. Use **`test-dl-back.jpg`** for the back.
4. For the selfie, point the camera at any face — test mode accepts any image.

{% endstep %}

{% step %}

### See it in the dashboard

Back in the dashboard, the new verification appears in **Identity → All sessions** with a status of **Verified**. Click it to see the full timeline — when each check started, what passed, what flagged, and the final decision.

{% endstep %}

{% step %}

### See a failure

The default test fixture passes everything. To see a failure, repeat the flow and use **`test-dl-expired.jpg`** instead of `test-dl-front.jpg`. The verification now ends with status **Failed** and reason `document_expired`.

{% endstep %}
{% endstepper %}

## What's next?

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-toggle-on" style="color:$primary;">:toggle-on:</i></h3></td><td><strong>Switch to live mode</strong></td><td>What changes when you flip the switch.</td><td><a href="test-and-live-mode.md">test-and-live-mode.md</a></td></tr><tr><td><h3><i class="fa-list-check" style="color:$primary;">:list-check:</i></h3></td><td><strong>Pick a flow</strong></td><td>Identity, bank, business — when to use which.</td><td><a href="../verification-flows/README.md">README.md</a></td></tr><tr><td><h3><i class="fa-bolt" style="color:$primary;">:bolt:</i></h3></td><td><strong>Set up a webhook</strong></td><td>React to verification results automatically.</td><td><a href="https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks">README.md</a></td></tr></tbody></table>

{% hint style="info" %}
**Building an integration?** Developers / [Identity API quickstart](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/identity-api) covers the same flow with code samples in cURL, Node, Python, Go, and Ruby.

<p><button type="button" class="button primary" data-action="ask" data-query="How do I integrate Evolve Identity with my own onboarding flow?" data-icon="code">Ask the docs</button></p>
{% endhint %}
