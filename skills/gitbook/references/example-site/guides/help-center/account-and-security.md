---
icon: user-shield
description: Team access, SSO, audit logs, key management, and account-level security questions.
---

# Account and security

## How do I invite a team member?

Open **Settings → Team → Invite member** in the dashboard. Enter their email and pick a role (Admin, Developer, Operator, Finance, or Viewer). They'll receive an email and join your account once they accept.

You can change a member's role any time, and the change takes effect immediately.

## What roles are available, and what can each one do?

Five roles, each progressively more restricted:

| Role | Can do |
| --- | --- |
| **Admin** | Everything, including managing other members and billing. |
| **Developer** | API keys, webhook endpoints, integration testing. No billing. |
| **Operator** | Issue refunds, respond to disputes, manage payouts. No billing or API keys. |
| **Finance** | Read-only on payments, full access to settlements and reports. |
| **Viewer** | Read-only across the dashboard. |

You can also create custom roles with specific permissions in **Settings → Team → Custom roles** on Enterprise.

## How do I set up SSO?

SSO is available on Growth and Enterprise. In **Settings → Security → SSO**, pick your provider (Okta, Google Workspace, Microsoft Entra ID, or generic SAML/OIDC) and follow the per-provider setup. Most teams have it working in 30 minutes.

After SSO is enabled, password-based logins are disabled for everyone except break-glass admins (you can configure this).

For SCIM (auto-provisioning team members from your IdP), see the [community forum](https://gitbookio.github.io/evolve-demo/connections/community/).

## How do I rotate an API key?

In **Developers → API keys**, click **Roll** next to the key. The new key is active immediately; the old one keeps working for 24 hours so you can deploy without downtime. Revoke the old one once you've confirmed the new one is in place.

For incident response (suspected leakage), revoke immediately rather than rolling — anyone with the old key loses access at once. See the [webhook deep-dive on YouTube](https://gitbookio.github.io/evolve-demo/connections/youtube/webhooks-deep-dive.html) for the full incident-response flow.

## What does Evolve do if a key leaks publicly?

Evolve runs leaked-key detection across public GitHub commits, public Gitlab, common paste sites, and a few cloud-provider misconfigurations. If we detect your key in any of those, we auto-revoke it and email you within minutes — usually before any unauthorized requests can land.

Auto-revocation can't be turned off. If you'd rather receive a warning without immediate revocation, contact support.

## How do I export my audit log?

The audit log is exportable from **Compliance → Audit log → Export**. Choose a date range, columns, and format (CSV or JSON). Exports under 10,000 rows generate immediately; larger exports email you when ready.

For continuous export to your SIEM (Splunk, Datadog, etc.), the [reporting webhooks doc](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/webhooks/event-catalog) covers the per-event push pattern.

## Can I require 2FA for all team members?

Yes. **Settings → Security → Two-factor authentication → Require for all members**. Existing members get a 7-day grace period to enroll; new members must enroll on first login.

If you also have SSO enabled, your IdP's MFA controls take precedence — Evolve's 2FA only applies to non-SSO admins (typically break-glass accounts).

## What's Evolve's security posture?

We're SOC 2 Type II audited annually, ISO 27001 certified, and PCI-DSS Level 1 compliant. Reports are available under NDA from your account team.

Encryption at rest uses per-tenant keys (KMS-managed); Enterprise customers can BYOK. Data residency in EU and US regions is configurable in **Settings → Security → Data residency**.

## What happens if I close my account?

Closing an account is a multi-step process to make sure there's no money left to move. Contact your account team to start it; they walk you through:

1. Disabling new charges.
2. Settling any outstanding balance.
3. Issuing any pending payouts.
4. Final settlement file.
5. Closing the account.

Account data is retained per your retention policy (default 7 years for compliance records, 30 days for verification PII). Closed accounts cannot be reopened with the same name; sign up fresh if you change your mind.

## Where can I find more answers?

* [Community forum](https://gitbookio.github.io/evolve-demo/connections/community/)
* [YouTube: Webhooks deep-dive](https://gitbookio.github.io/evolve-demo/connections/youtube/webhooks-deep-dive.html)
* [Developer docs: Authentication](https://app.gitbook.com/s/Si95BtOt1VRLWjT7A67V/getting-started/authentication)
* [Identity compliance: Audit logs](https://app.gitbook.com/s/w7NRnYZuokE4h1mm2pJB/compliance/audit-logs)
