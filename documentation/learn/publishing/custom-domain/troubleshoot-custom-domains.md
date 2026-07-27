---
description: Fixes for DNS, SSL, and domain connection problems.
---

# Troubleshoot custom domains

<details>

<summary>SSL error: an error occurred when provisioning your SSL certificate</summary>

When you set a custom domain for your organization, group, or section, GitBook automatically provisions an SSL certificate so your documentation loads securely over HTTPS — you don't need to purchase or configure one yourself.

Errors here usually happen when the CNAME record for the custom domain hasn't propagated yet:

1. Check that your CNAME record is set up correctly — see [Set a custom domain](README.md). An incorrect record means GitBook can't configure the SSL certificate or finish setup.
2. Allow at least one hour between configuring the CNAME record and finalizing the custom domain setup.
3. Verify the CNAME has propagated, using a third-party DNS lookup tool like [WhatsMyDNS](https://www.whatsmydns.net/).
4. If you're using Cloudflare, confirm the record isn't proxied — [see Cloudflare's docs](https://developers.cloudflare.com/fundamentals/setup/manage-domains/pause-cloudflare/#disable-proxy-on-dns-records).

</details>

<details>

<summary>Domain already connected error: your subdomain is already configured for different content</summary>

A custom domain assigned to a site must be unique — using the same domain in more than one place produces this error.

Click the link in the error message to see what content the domain is already connected to. If you don't have access to that content, [contact support](../../../resources/get-support.md) for help deciding next steps.

The fix is always one of two things:

1. Choose a different custom domain, or
2. Disconnect the domain from its current content, then reconnect it to the new content.

</details>
