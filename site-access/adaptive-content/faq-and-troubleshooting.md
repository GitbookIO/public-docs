---
description: Common questions and troubleshooting steps for adaptive content
---

# FAQ and troubleshooting

### Which authentication method should I use for adaptive content?

It depends on how you want to control access:

* Public and private content on one site — use [signed cookies](enabling-adaptive-content/cookies.md)
* Simple personalization without authentication — use [URL parameters](enabling-adaptive-content/url.md)
* An entirely private site — use an [authenticated access integration](enabling-adaptive-content/authenticated-access.md)
* Already using feature flags — use a [feature flag provider](enabling-adaptive-content/feature-flags.md)

### Can I publish a partially public site with some authenticated content?

Yes. You can keep a public site with some authenticated sections, without requiring login for the entire site:

1. Keep your site audience as Public, Unlisted, or Share link.
2. Enable adaptive content in your site’s settings.
3. Use [signed cookies](enabling-adaptive-content/cookies.md#signed-cookie) to pass visitor claims after they log in to your main application.
4. Set conditions on the specific pages or sections that should only show for authenticated visitors.

### How do I set up adaptive content with a custom OIDC provider?

Adaptive content works with any identity provider:

1. Set up the generic OIDC integration in GitBook.
2. Configure your OIDC provider to include custom claims in tokens.
3. Map those claims in your GitBook visitor schema.

Common issues: make sure your provider includes the custom claims in the token (not just standard OIDC claims), check whether claims are nested under provider-specific properties, and verify the token format. Different providers structure custom claims differently — check your provider’s documentation.

### Why aren’t my segments working or showing in preview?

* Confirm your visitor schema is correctly defined.
* Verify that your segment JSON matches the schema structure.
* Ensure the condition applies to the section, page, or block you’re testing.
* Use the preview feature from the correct page, and refresh the preview after schema changes.

See [Testing with segments](testing-with-segments.md) for the full testing flow.

### Does restricted content appear in search results?

No. Search results only reflect the content a visitor has access to. Any section, page, or block behind adaptive content is only indexed and visible in search for visitors who meet the conditions to view it.

### Do JWT claim schemas support free-form strings?

Not yet. Claim schemas currently only support enums for string values, so define all required string values within an enum.

### Can adaptive content work with arrays in JWT claims?

No. A claim provides a single value — a string (enum) or a boolean. If you need multiple values, transform them on the claims-provider side (for example, in Azure or Okta).

### How do I debug adaptive content conditions?

* Property names are case-sensitive (`role` ≠ `Role`).
* Check data types — boolean `true` is not the string `"true"`.
* Check the property path in nested conditions.
* Inspect the claims attached to a token at [jwt.io](https://www.jwt.io/) to confirm your expected claims are being passed.
