---
description: Follow these steps to allow GitBook to serve your documentation on your custom domain.
---
# DNS configuration

## Supported domains

**Only subdomains** can be used to serve your documentation. Apex domains cannot be used.

See the table below:

|                        |                    |             |
| ---------------------- | ------------------ | ----------- |
| **Custom domain type** | **Example domain** | **Support** |
| `www` subdomain        | `www.example.com`  | ✅           |
| custom subdomain       | `blog.example.com` | ✅           |
| apex domain            | `example.com`      | ❌           |

## DNS Settings

### CNAME record

In short, **CNAME** your subdomain to `hosting.gitbook.io`.

Given the number of existing managed DNS providers, we cannot provide an actual setup process for all of them. Usually, you simply have to enter the subdomain without the root domain, and choose a CNAME type with `hosting.gitbook.io` as its value or target.

For example, if your root domain is `mycompany.com`, here is the proper configuration on Cloudflare if you wanted your documentation to be served at `docs.mycompany.com`:

![Properly configured custom domain on Cloudflare](<../../.gitbook/assets/image (42).png>)

{% hint style="warning" %}
If you already have a custom domain registered on GitBook with a CNAME set to `hosting.gitbook.com`, please contact our support team before updating its CNAME to `hosting.gitbook.io` to ensure a flawless migration.
{% endhint %}

### CAA record

In order for DigiCert to issue an SSL certificate for your custom domain, it must be allowed to do so. CAA records allow you to specify who can issue an SSL certificate for the custom domains that you own.

**When no CAA record** is registered for a domain, it means that anyone can issue an SSL certificate for it. If this is your case, your domain is **already properly configured** to be used with GitBook.

If **you already have a CAA record** for your custom domain, you must **explicitly allow DigiCert** to issue an SSL certificate for it by adding the following record:

```
0 issue "digicert.com"
```

## Cloudflare proxying

If you domain is hosted on Cloudflare, you may be tempted to activate Cloudflare's proxying (the orange cloud, also called "Proxy status" in your domain settings).

While this configuration **might work** on most cases, we strongly recommend against activating it. First, because your custom domain will already benefit from Cloudflare's CDN and a DigiCert SSL certificate. This option also obfuscates the DNS target for your domain to the public, preventing GitBook to properly run routine checks on your custom domain.

Whenever possible, **turn off Cloudflare proxying** to ensure that your documentation is served without issues and can be monitored by GitBook.
