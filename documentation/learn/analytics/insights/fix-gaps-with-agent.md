---
description: Send content gaps to GitBook Agent to draft fixes.
---

# Fix gaps with GitBook Agent

{% hint style="warning" %}
This feature is in early access — access is rolling out gradually.
{% endhint %}

Once you've [identified a content gap](identify-content-gaps.md), GitBook Agent can help you close it directly from the Insights dashboard. This is the same underlying finding-and-fix mechanism described in [Run an Agent audit](../../gitbook-ai/agent/run-an-audit.md) — the difference here is the entry point: you're acting on one specific gap Insights has already surfaced, rather than starting a broader scan.

When a gap supports an automatic fix, GitBook shows a **Create change request** action, so Agent can generate a proposed fix for your team to review. If you don't want to act on a gap, archive it instead — GitBook won't resurface an archived finding.
