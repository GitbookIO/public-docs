---
description: Control who can see your docs and personalize content for them.
---

# Site access and personalization

GitBook gives you two related but distinct tools for controlling what readers see:

* **[Authenticated access](authenticated-access/README.md)** protects your docs behind a login, so only signed-in visitors can view them at all.
* **[Adaptive content](adaptive-content-concepts.md)** customizes what a signed-in (or otherwise identified) visitor sees, based on data about who they are.

They can work together, or independently — adaptive content can also run on a publicly published site, using data from cookies, URL parameters, or feature flags instead of a login.

* [Adaptive content: how claims flow](adaptive-content-concepts.md) — the concept.
* [Configure adaptive content](configure-adaptive-content.md) — enable it and choose how visitor data reaches GitBook.
* [Write content conditions](write-content-conditions.md) — show or hide pages, sections, variants, and blocks.
* [Test with segments](test-with-segments.md) — preview your site as different visitors.
* [Troubleshoot adaptive content](troubleshoot-adaptive-content.md) — when claims or conditions aren't behaving.
* [Authenticated access](authenticated-access/README.md) — require sign-in, with Auth0, Azure AD, Okta, AWS Cognito, generic OIDC, or your own backend.
