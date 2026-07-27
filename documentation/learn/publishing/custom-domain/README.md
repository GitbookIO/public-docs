---
description: Serve your docs site on your own domain.
---

# Set a custom domain

{% hint style="info" %}
Custom domains are available on Premium and Ultimate plans.
{% endhint %}

By default, your sites are accessible on a `[subdomain].gitbook.io` domain. Set a custom domain so your audience can reach your documentation on a domain you choose instead.

{% hint style="info" %}
This page covers a custom domain or subdomain. For a custom subdirectory (like `example.com/docs`), see [Custom subdirectories](custom-subdirectories.md).
{% endhint %}

{% stepper %}
{% step %}
#### Choose a subdomain

Use `www`, or a custom one — commonly `docs.example.com`, `help.example.com`, or `developers.example.com`.
{% endstep %}

{% step %}
#### Initiate the custom domain setup

Open the site's **Settings**, then **Set up a custom domain**. Enter the domain you chose, and click **Next**.
{% endstep %}

{% step %}
#### Configure the DNS

You'll see three fields: **Type**, **Name**, **Target**. Copy the **Name** and **Target** values into your DNS provider — outside GitBook — picking the **Type** of record from your provider's list. Each provider differs, so check with them directly if you're unsure.

After adding the record, wait at least 1 hour for it to propagate before continuing.
{% endstep %}

{% step %}
#### Finalize your setup

Once the record has propagated, GitBook verifies the domain and record, and automatically configures an SSL certificate. You'll get a notification when it's done — or close the window and we'll notify you once it's finished on our end.
{% endstep %}
{% endstepper %}

Running into problems? See [Troubleshoot custom domains](troubleshoot-custom-domains.md).
