---
description: Fixes for claims not arriving and conditions not matching.
---

# Troubleshoot adaptive content

If a condition isn't showing or hiding content the way you expect, work through these checks.

### Claims aren't showing up in the condition editor's autocomplete

The condition editor suggests claims and attributes it's seen from previous visitors. If a claim you expect isn't suggested, no visitor carrying it has reached your site yet — [test with a segment](test-with-segments.md) instead of waiting for real traffic, or check that your [visitor schema](configure-adaptive-content.md#set-your-visitor-schema) actually declares the claim.

### A condition matches in a segment, but not for real visitors

Confirm the claim is declared correctly in your [visitor schema](configure-adaptive-content.md#set-your-visitor-schema) — in particular, that anything arriving via cookies, URL parameters, or feature flags is declared under the schema's `unsigned` object. Claims missing from `unsigned` won't be readable, even if your application is sending them correctly.

### Cookie-based claims aren't arriving

* Confirm your site is served under a [custom domain](../publishing/custom-domain/README.md) — the cookie methods for adaptive content don't work on a `.gitbook.io` subdomain.
* For a signed cookie, confirm the JWT is signed with the site's current visitor signing key, found in your site's audience settings, and that the cookie is scoped to a wildcard covering your domain (e.g. `.acme.org` for `app.acme.org`).
* For a public cookie, remember it's unsigned — its properties must be declared under `unsigned` in your schema.

### URL parameter claims aren't arriving

Confirm the parameter is in the exact format `visitor.<prop>` and that `<prop>` is declared under your schema's `unsigned` object. URL-based claims are also visitor-editable — don't rely on them for anything sensitive.

### Feature-flag claims aren't arriving

Confirm the GitBook adaptive-content helper (`@gitbook/adaptive`) is actually wired into your feature flag provider's React SDK, and that your visitor schema has been set — installing the LaunchDarkly or Reflag integration should set this automatically. See [Configure adaptive content](configure-adaptive-content.md#feature-flags).

### A condition doesn't evaluate the way you expect

Check the expression itself in the condition editor — conditions are plain JavaScript, so a missing `!`, a `&&` where you meant `||`, or a typo'd claim name will silently produce the wrong result rather than an error. [Test with a segment](test-with-segments.md) that matches (and one that doesn't) to confirm the logic before publishing.

### Still stuck?

[Contact support](../../resources/get-support.md) with the claim(s) you're passing, the condition you've written, and whether the issue reproduces in a test segment or only with real visitor traffic.
