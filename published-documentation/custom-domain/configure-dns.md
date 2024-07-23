# 3. Configure the DNS

Configuring DNS happens _outside_ of GitBook, at the DNS provider you are using for your domain.

There are three parts to this step:

1. [Configure a CNAME record](configure-dns.md#configure-a-cname-record)
2. [Check for a CAA record](configure-dns.md#check-for-a-caa-record)
3. [Wait for the changes to take effect](configure-dns.md#wait-for-the-changes-to-take-effect)

## Configure a CNAME record

The names of the fields and what to enter to configure the record may differ between DNS control panels, but we’ve covered the most common options here. If you’re in any doubt, check with your DNS provider.

* The **type** is the kind of DNS record that you want to create. Here, you need to choose **CNAME**.
* The **name** or **DNS entry** is where you enter your subdomain. You might need to enter it in full (e.g. **docs.example.com**) or you might need to enter the part before your apex domain (e.g. **docs**). If you’re unsure which to use, check with your DNS provider.
* The **target, value** or **destination** is where the subdomain should be pointed.

{% hint style="info" %}
You might also see a field named **TTL**, which stands for Time To Live. It’s the number of seconds that the DNS record can be cached for.&#x20;

To determine an appropriate TTL (Time to Live) for your new DNS records, you can reference the TTL values of your existing records. Matching these values is a safe practice if you're unsure of what to set for the new ones.\
\
Alternatively, we suggest setting 43200 seconds (12 hours) or 86400 seconds (24 hours).
{% endhint %}

Here’s an example of how a correct configuration looks in Cloudflare’s control panel:

![A properly configured custom domain in Cloudflare’s control panel](<../../.gitbook/assets/Screenshot 2022-04-11 at 16.53.56.png>)

{% hint style="danger" %}
**Note:** a CNAME record cannot co-exist with another record for the same name. If you already have an A record, AAAA record, TXT record, or any other type of record for your chosen subdomain, you would need to remove those, before adding the CNAME record.
{% endhint %}

### Are you using Cloudflare?

If you are configuring DNS in Cloudflare’s control panel, please ensure that Cloudflare’s proxying (the orange cloud, also called "Proxy status" in your domain settings) is **disabled**.&#x20;

This is for two reasons:

1. This option obfuscates the DNS target for your domain to the public, preventing GitBook from properly running routine checks on your custom domain.
2. Your custom domain will already benefit from Cloudflare’s CDN and a Google Trust Services SSL certificate on our end.

Again, please **turn off Cloudflare proxying** to ensure that your documentation is served without issues and can be monitored by GitBook.

{% hint style="warning" %}
**GitBook does not officially support proxy setups**&#x20;

If you decide to set it up anyway, please ensure your setup respects the following:

* You need to proxy all `GET`, `OPTIONS`, `HEAD`, `POST` methods.
* You should respect the `Cache-Control` header and use the entire request (URL + headers, by respecting the `Vary` header) as a cache key.
* You should not modify the HTML to load external resources, or you should consider the CSP and ensure a [`nonce`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global\_attributes/nonce) is set on every resource.
{% endhint %}

## Check for a CAA record

CAA records enable you to specify who can issue an SSL certificate for the domains you own. We use Google Trust Services to issue an SSL certificate for your custom domain, so this needs to be allowed. There are two ways to do this:

1. Have no CAA record. Without a CAA record, there are no limitations on which SSL providers can issue an SSL certificate for your domain.
2. Have a CAA record that explicitly allows Google Trust Services. If a CAA record exists, any providers not explicitly allowed will be blocked. The following is the value that would need to be included in a CAA record to allow Google Trust Services:

```
0 issue "pki.goog"
```

## Wait for the changes to take effect

DNS records are cached for a defined period, known as the Time to Live (TTL). This caching is beneficial for performance since DNS records rarely change.

The Time to Live (TTL) value specifies when DNS cache servers must refresh their cache by checking for updates, ensuring they respond with the most current information.&#x20;

In most cases, it’s best to allow _**at least an hour**_ before moving to the final step of custom domain set-up.&#x20;

{% hint style="info" %}
**You might need to wait 1-48 hours for the DNS changes to take effect.**&#x20;
{% endhint %}

#### Want to check how this process, known as _propagation_, is progressing?&#x20;

You could use a DNS lookup tool, such as [WhatsMyDNS](https://www.whatsmydns.net/).&#x20;

Enter your full subdomain, select CNAME from the dropdown list, and press the Search button. DNS cache servers around the world will respond to let you know what their cached result is. You’ll want to periodically check these results until the majority respond with your assigned CNAME value.

Once DNS propagation has been completed, you can move on to the last step: [confirming the custom domain setup](finalize.md).
