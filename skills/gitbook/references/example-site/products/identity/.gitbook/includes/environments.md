---
title: Test and live environments
---

Evolve has two fully separate environments. They share no data — keys, customers, charges, and webhooks all exist independently in each.

| Environment | API base URL | Dashboard | Key prefix |
| --- | --- | --- | --- |
| Test | <code class="expression">space.vars.api_test</code> | <code class="expression">space.vars.dashboard_test</code> | `sk_test_` / `pk_test_` |
| Live | <code class="expression">space.vars.api_live</code> | <code class="expression">space.vars.dashboard_live</code> | `sk_live_` / `pk_live_` |

Test mode accepts only test fixture data — no real cards, real documents, or real bank accounts. Nothing leaves the test environment.
