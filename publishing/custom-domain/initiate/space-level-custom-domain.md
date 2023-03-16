# Space-level custom domain

{% hint style="info" %}
Please follow the steps to set a custom domain in this order:

1. [Choosing a subdomain](../choose.md)
2. [Deciding where to set the custom domain](../location.md)
3. [**Initiating the custom domain setup**](./) **(at the** [**organization**](organization-level-custom-domain.md)**,** [**collection**](collection-level-custom-domain.md)**, or** [**space**](space-level-custom-domain.md) **level) (you are here)**
4. [Configuring DNS](../configure-dns.md)
5. [Finalizing the custom domain setup](../finalize.md)
{% endhint %}

You'll find the options for setting a custom domain for a space within the space's **visibility menu**. To get there, click on the name of the space in the sidebar, and then click on the button to open the visibility menu near the top-right corner. It will look something like this:

<figure><img src="../../../.gitbook/assets/visibility-menu-space.png" alt=""><figcaption><p>Click the button to open the visibility menu</p></figcaption></figure>

First, your space needs to be published. Any setting other than unpublished will work — **public**, **unlisted**, **share link**, or **visitor authentication**. (Depending on the plan you have chosen, it might be that only _some_ of these publishing options are available to you.)

Once you have published your space using one of those options, the button will no longer say publish, but will instead state the current publish setting. In this example, the space is published as **unlisted.** Next, click on **link and domain settings**:

<figure><img src="../../../.gitbook/assets/space-link-and-domain-settings.png" alt=""><figcaption><p>Link and domain settings</p></figcaption></figure>

From **link and domain settings**, click the **connect a domain** button:

<figure><img src="../../../.gitbook/assets/space-connect-a-domain.png" alt=""><figcaption><p>Connect a domain</p></figcaption></figure>

This will open up a window where you can enter the custom domain, and then click the **continue** button:

<figure><img src="../../../.gitbook/assets/connect-a-domain.png" alt=""><figcaption><p>Connect a domain</p></figcaption></figure>

Behind the scenes, we'll check the DNS settings for the custom domain and we'll provide the value to use in the next step when you create your CNAME DNS record. Copy that value to your clipboard by clicking on the icon on the right-hand side of the value field.

<figure><img src="../../../.gitbook/assets/cname-value.png" alt=""><figcaption><p>The CNAME value for your custom domain</p></figcaption></figure>

The value for the CNAME record will be in the format `[something]-hosting.gitbook.io`, where that `[something]` will be **unique to you**. Make sure to use the value displayed to you in the GitBook app, and _not_ the value in the screenshot above! 🙂

Once you have copied the unique CNAME value to your clipboard, you're ready to move onto the next step: [configuring DNS](../configure-dns.md).
