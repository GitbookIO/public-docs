---
description: Learn how to receive webhook notifications through GitBook's Webhook integration
---

# Receive webhook notifications

The [Webhook integration](https://www.gitbook.com/integrations/webhook) sends real-time notifications when events occur in your GitBook spaces or sites. It supports a configurable webhook URL, HMAC signature verification, and automatic retry with exponential backoff.

Before following this guide, install the [Webhook integration](https://www.gitbook.com/integrations/webhook) into your organization.

### Supported events

Which events are available depends on whether the integration is installed on a space or a site.

**Spaces:**

* **Content updates** (`space_content_updated`) — content in the space was modified.

**Sites:**

* **Site views** (`site_view`) — a user visited a page on your site.
* **Page feedback** (`page_feedback`) — a user submitted feedback on a page.

#### `space_content_updated`

```json
{
  "eventId": "evt_2345678901bcdefg",
  "type": "space_content_updated",
  "spaceId": "space_xyz789",
  "installationId": "inst_def456",
  "revisionId": "rev_abc123def456"
}
```

#### `site_view`

```json
{
  "eventId": "evt_1234567890abcdef",
  "type": "site_view",
  "siteId": "site_abc123",
  "installationId": "inst_def456",
  "visitor": {
    "anonymousId": "anon_789ghi",
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36",
    "ip": "192.168.1.100",
    "cookies": {
      "session_id": "sess_xyz789"
    }
  },
  "url": "https://docs.example.com/getting-started",
  "referrer": "https://www.google.com/search?q=example+docs"
}
```

#### `page_feedback`

```json
{
  "eventId": "evt_3456789012cdefgh",
  "type": "page_feedback",
  "siteId": "site_abc123",
  "spaceId": "space_xyz789",
  "installationId": "inst_def456",
  "pageId": "page_feedback123",
  "feedback": {
    "rating": "good",
    "comment": "This page was very helpful!"
  },
  "visitor": {
    "anonymousId": "anon_789ghi",
    "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36",
    "ip": "192.168.1.101",
    "cookies": {}
  },
  "url": "https://docs.example.com/api-reference",
  "referrer": "https://docs.example.com/getting-started"
}
```

### Configuration

At minimum, set a **Webhook URL** (the endpoint events are sent to) and choose which **event types** to receive.

### Webhook security

Every request carries an HMAC-SHA256 signature in the `X-GitBook-Signature` header:

```
X-GitBook-Signature: t=1640995200,v1=abc123def456...
```

* `t` — Unix timestamp of the request.
* `v1` — HMAC-SHA256 signature of the payload.

Verify it like this:

```javascript
const crypto = require('crypto');

function verifyGitBookSignature(payload, signature, secret) {
  if (!signature) return false;

  try {
    // Parse signature format: t=timestamp,v1=hash
    const parts = signature.split(',');
    let timestamp, hash;

    for (const part of parts) {
      if (part.startsWith('t=')) {
        timestamp = part.substring(2);
      } else if (part.startsWith('v1=')) {
        hash = part.substring(3);
      }
    }

    if (!timestamp || !hash) return false;

    // Generate expected signature (our implementation uses timestamp.payload format)
    const expectedSignature = crypto
      .createHmac('sha256', secret)
      .update(`${timestamp}.${payload}`)
      .digest('hex');

    // Constant-time comparison to prevent timing attacks
    return crypto.timingSafeEqual(
      Buffer.from(hash, 'hex'),
      Buffer.from(expectedSignature, 'hex')
    );
  } catch (error) {
    return false;
  }
}

// Usage
const isValid = verifyGitBookSignature(
  requestBody,
  request.headers['x-gitbook-signature'],
  'your-secret-key'
);
```

### Retry logic

Failed deliveries retry automatically:

* **Max retries**: 3 attempts
* **Backoff strategy**: exponential, with jitter
* **Base delay**: 1 second, ±10% jitter
* **Retries on**: network errors, `5xx` responses, `429` rate limiting
* **No retry on**: other `4xx` client errors

| Attempt | Base delay | Jitter range | Total delay range |
|---|---|---|---|
| 1 | 1s | ±0.1s | 1.0–1.1s |
| 2 | 2s | ±0.2s | 2.0–2.2s |
| 3 | 4s | ±0.4s | 4.0–4.4s |

### Best practices

**Design your endpoint to verify signatures first, respond fast, and process asynchronously:**

```javascript
const express = require('express');
const app = express();

app.post('/webhooks/gitbook', express.raw({ type: 'application/json' }), (req, res) => {
  const requestBody = req.body.toString();

  const signature = req.headers['x-gitbook-signature'];
  const isValid = verifyGitBookSignature(requestBody, signature, process.env.GITBOOK_SECRET);

  if (!isValid) {
    return res.status(401).json({ error: 'Invalid signature' });
  }

  // Respond immediately, then process asynchronously
  res.status(200).json({ received: true });

  setImmediate(() => {
    const event = JSON.parse(requestBody);
    processEvent(event);
  });
});
```

**Handle duplicate deliveries idempotently** — webhooks can be delivered more than once for the same event:

```javascript
const processedEvents = new Map();
const EVENT_RETENTION_MS = 2 * 60 * 1000; // 2 minutes

function remember(eventId) {
  if (processedEvents.has(eventId)) return false;

  const timer = setTimeout(() => {
    processedEvents.delete(eventId);
  }, EVENT_RETENTION_MS);

  processedEvents.set(eventId, timer);
  return true;
}

function handleEvent(event) {
  // Guard goes first so concurrent deliveries don't double-process
  if (!remember(event.eventId)) {
    console.log('Duplicate event ignored:', event.eventId);
    return;
  }

  // doWork(event);
}
```
