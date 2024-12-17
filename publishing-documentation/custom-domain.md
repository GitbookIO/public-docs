---
icon: globe-pointer
description: Set a custom domain for your GitBook organization or docs sites
---

# Set a custom domain

{% hint style="info" %}
This feature is available on [Premium and Ultimate site plans](https://www.gitbook.com/pricing).
{% endhint %}

By default, your sites are accessible on a `[subdomain].gitbook.io` domain.&#x20;

You can customize this by setting a custom domain, meaning your audience can access your documentation on a chosen domain.

{% stepper %}
{% step %}
### Choose a subdomain

When choosing a subdomain, you can either use `www` or a custom one. Some commonly used subdomains are:

* `docs.example.com`
* `help.example.com`
* `developers.example.com`
{% endstep %}

{% step %}
### Initiate the custom domain setup

Navigate to the site for which you want to set the custom domain. Click **Settings,** then choose **Set up a custom domain.**

From here, you'll see a window where you can enter the custom domain you chose in the first step. Type it out and click **Next.**
{% endstep %}

{% step %}
### Configure the DNS

At this stage, you'll see a window with three fields: **Type, Name, Target.**

Those are the details you'll use to set your custom domain in your DNS provider. This is done _outside_ GitBook, in the provider you are using for your domain.

Copy the contents of the **Name** and **Target** fields to use in your DNS provider. Each provider is different, so when in doubt, check directly with them how to add this record. You should be able to pick the **Type** of record from a list in your provider.

After adding the record, it might take some time for the changes to propagate. We recommend **waiting at least 1 hour** before moving to the next step. Click **Next** when you are ready.
{% endstep %}

{% step %}
### Finalize your setup

After adding the record and it being propagated, it's time to go live! GitBook will verify the domain, the record you added and will automatically configure the SSL certificate for your domain.

Once done, you'll receive a notification and can click **Finish**. You can also close the window if you need, and we'll send you a notification once the process is done on our side.
{% endstep %}
{% endstepper %}

### Troubleshooting

Setting up a custom domain can occasionally run into obstacles. Below, we outline frequent problems encountered during this process and provide detailed solutions to each of them.

<details>

<summary>SSL error: an error occurred when provisioning your SSL certificate.</summary>

When a custom domain is set for your organization, collection, or space, we set up an SSL certificate on our end so that your documentation will load securely, over HTTPS. \
\
This happens automatically when you set your custom domain — you do not need to purchase or configure an SSL certificate.

Occasionally errors occur at this stage, usually when the CNAME record for the custom domain hasn't propagated.

In these cases, we can recommend the following:

1. Check that your CNAME record is set up correctly. \
   Please review our page about configuring DNS to help you with this. \
   If the CNAME record is incorrect, we won't be able to configure the SSL certificate and complete the custom domain set-up.&#x20;
2. Allow _**at least one hour**_ between configuring the CNAME record and finalizing the custom domain setup.&#x20;
3. Verify if the CNAME has propagated. You can try using a third-party DNS lookup tool, such as [WhatsMyDNS](https://www.whatsmydns.net/), to find out what the servers believe to be correct for your correct CNAME record.&#x20;
4. If you are using Cloudflare, please confirm that you don’t have the record proxied [as explained here](broken-reference).

</details>

<details>

<summary>Domain already connected error: your subdomain is already configured for different content.</summary>

A custom domain assigned to an organization or site must be unique. Attempting to use the same custom domain in more than one location will result in an error.

If this happens, you can click the link within the error message to look at the content the custom domain is already connected to. This may help you to decide what to do next.

It’s also possible that you might not have access to the content — if that’s the case, contact the support team and they can help you with your next steps.

The solution to this error will always be one of two things, however:

1. Choose a different custom domain; or
2. Disconnect the custom domain from the content it is already connected to, then reconnect it to the new content.

</details>

<details>

<summary>The custom domain is set correctly, but is redirecting to a different custom domain.</summary>

This is an expected behaviour, that usually can be changed.&#x20;

The common issue is that custom domains have been set in multiple locations for example organization and the site. When someone accesses the URL for an organization, they are taken straight to the organization’s default content. Likewise, when someone accesses the URL for a multi-variant site, they are taken straight to the multi-variant default site.&#x20;

**Example**&#x20;

* `docs.example.com` is set as the custom domain for an organization
* `team.example.com` is set as the custom domain for that organization’s default content.

In this case, the expected behaviour  would be `docs.example.com` redirecting you to `team.example.com`.

This issue can be solved by changing the default content or by removing the organization domain and adding the domains at a space level or the other way around (removing the space domain, and maintaining the org domain)&#x20;

This issue frequently occurs due to the confusion over the location of the domain. \
Please ensure you checked where your domains are set up, and adjusted this to your requirement.&#x20;

</details>
