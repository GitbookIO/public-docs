# Configure DNS

{% hint style="info" %}
This is **step 2** of a 3-step process for setting up a custom domain. Make sure to follow the steps in the correct order!

1. [Choose a subdomain](choose-a-subdomain.md)
2. Configure DNS (you are here)
3. [Set the custom domain in GitBook](custom-domain-setup-on-gitbook.md)
{% endhint %}

Configuring DNS happens _outside_ of GitBook, at the DNS provider you are using for your domain.

**This step is super important** because the correct DNS configurations are what allow us to connect the subdomain to your space, collection, or organization in step 3.

There are three parts to this step:

1. [Configure a CNAME record](dns-configuration.md#configure-a-cname-record)
2. [Check for a CAA record](dns-configuration.md#check-for-a-caa-record)
3. [Wait for the changes to take effect](dns-configuration.md#wait-for-the-changes-to-take-effect)

## Configure a CNAME record

{% hint style="info" %}
The short answer: point your subdomain to GitBook via a CNAME record.
{% endhint %}

The names of the fields and what to actually enter to configure the record may differ between DNS control panels, but we've covered the most common options here. If you're in any doubt, check with your DNS provider.

* The **type** is the kind of DNS record that you want to create. Here, you need to choose **CNAME**.
* The **name** or **DNS entry** is where you enter your subdomain. You might need to enter it in full (e.g. **docs.example.com**) or you might just need to enter the part before your apex domain (e.g. **docs**). If you're not sure which to use, check with your DNS provider.
* The **target** or **value** or **destination** is where the subdomain should be pointed.

You might also see a field named **TTL**, which stands for Time To Live. It's the number of seconds that the DNS record can be cached for. If you're not sure what to set, look at the TTL for your existing DNS records. You could set the same number. If you're still not sure, we suggest setting 43200 seconds (12 hours) or 86400 seconds (24 hours).

Here's an example of how a correct configuration looks in Cloudflare's control panel:

![A properly configured custom domain in Cloudflare's control panel](<../.gitbook/assets/Screenshot 2022-04-11 at 16.53.56.png>)

{% hint style="warning" %}
**Note:** a CNAME record cannot co-exist with another record for the same name. If you already have an A record, AAAA record, TXT record, or any other type of record for your chosen subdomain, you would need to remove those first, before adding the CNAME record.
{% endhint %}

### Are you using Cloudflare?

If you are configuring DNS in Cloudflare's control panel, you may be tempted to activate Cloudflare's proxying (the orange cloud, also called "Proxy status" in your domain settings).

While this configuration _might_ work in most cases, we strongly recommend against activating it. Firstly, because your custom domain will already benefit from Cloudflare's CDN and a DigiCert SSL certificate. Secondly, this option obfuscates the DNS target for your domain to the public, preventing GitBook to properly run routine checks on your custom domain.

Whenever possible, please **turn off Cloudflare proxying** to ensure that your documentation is served without issues and can be monitored by GitBook.

## Check for a CAA record

{% hint style="info" %}
The short answer: either don't have a CAA record, or have one that explicitly allows DigiCert.
{% endhint %}

CAA records enable you to specify who can issue an SSL certificate for the domains that you own. We use DigiCert to issue an SSL certificate for your custom domain, so this needs to be allowed. There are two ways to do this.

1. Have no CAA record. Without a CAA record, there are no limitations on which SSL providers are allowed to issue an SSL certificate for your domain.
2. Have a CAA record that explicitly allows DigiCert. Any providers that are not explicitly allowed will be blocked. The following is the value that would need to be included in a CAA record to explicitly allow DigiCert:

```
0 issue "digicert.com"
```

## Wait for the changes to take effect

{% hint style="info" %}
The short answer: you might need to wait 1-48 hours for the DNS changes to take effect before moving onto step 3.
{% endhint %}

Remember the TTL (Time To Live) field we mentioned earlier? DNS records are cached for a period of time — which is usually a very good thing for performance reasons, because they typically don't change very often. When they _do_ change, there is a period of time (the TTL value) where DNS cache servers need their cache to expire before they will check for any changes and behave accordingly.

In most cases, it's best to allow at least an hour before moving onto step 3. Sometimes it could all update a bit more quickly, or it could take longer. It's rare for this to take longer than 48 hours.

Want to check how this process, known as _propagation_, is progressing? You could use a DNS lookup tool, such as [WhatsMyDNS](https://www.whatsmydns.net/). Enter your full subdomain, select CNAME from the dropdown list, and press the Search button. DNS cache servers around the world will respond to let you know what their cached result is. You'll want to periodically check these results until the vast majority respond with your assigned CNAME.

Once DNS propagation has completed, you can move onto [step 3: setting the custom domain in GitBook](custom-domain-setup-on-gitbook.md).
