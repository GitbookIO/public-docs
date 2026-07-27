---
description: Learn how to use HTTP requests in your integration
---

# Work with HTTP requests

Integrations often need to talk to the outside world — receiving webhooks, handling OAuth callbacks, or reacting to events GitBook itself emits. GitBook's runtime exposes a simple HTTP interface for this: once your integration is deployed, GitBook provisions an HTTPS endpoint that external callers can POST to, and your integration inspects the incoming event and responds.

{% hint style="info" %}
#### You rarely need to handle this manually

GitBook's SDK abstracts nearly all of this away — for most use cases, you'll work entirely through the higher-level [runtime reference](../integration-runtime-reference.md), defining actions, reacting to events, and rendering components. This page is useful if your integration needs to accept external events or callback payloads directly.
{% endhint %}

### The HTTP interface

Every integration exposes a single POST endpoint:

```
POST /{version}
Content-Type: multipart/form-data
```

`{version}` is the integration API version. If you're using the GitBook CLI, versioning and backwards compatibility are handled for you.

The request body is `FormData` with three fields:

* **event** — a serialized event describing what triggered the call (typed as `Event` from `@gitbook/api-client`). It may represent an external webhook, a GitBook-originated event, or another trigger.
* **environment** — information about the execution environment, such as installation details.
* **fetch-body** — the raw binary buffer of the exact body sent to your integration. Useful for verifying webhook signatures or handling non-JSON payloads.

### Handling an incoming event

GitBook parses the FormData, converts the event into a structured object, and passes it into your integration's logic. If you're using the SDK, you implement the relevant action or handler — you don't read FormData streams or parse multipart payloads yourself.

A typical webhook workflow:

1. An external service POSTs to your integration's endpoint.
2. GitBook reads the FormData and extracts `event`, `environment`, and `fetch-body`.
3. Your handler receives the normalized data.
4. You run your logic — verifying signatures, syncing data, updating blocks, or triggering ContentKit components.

### Shape of the request

```typescript
interface IncomingIntegrationRequest {
    event: Event;               // From @gitbook/api-client
    environment: IntegrationEnvironment;
    'fetch-body'?: Buffer;      // Raw request body, if present
}
```

GitBook delivers the payload in this structured form regardless of how the external service originally formatted its request — which unlocks patterns like accepting third-party webhooks, processing OAuth redirects, ingesting custom events from your own backend, or triggering content updates based on external state. Most integrations never touch this low-level interface directly; the runtime handles routing and parsing so you can focus on your logic.
