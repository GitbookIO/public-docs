# Organization-level custom domain

{% hint style="info" %}
Please follow the steps to set a custom domain in this order:

1. [Choosing a subdomain](../choose.md)
2. [Deciding where to set the custom domain](../location.md)
3. [**Initiating the custom domain setup**](./) **(at the** [**organization**](organization-level-custom-domain.md)**,** [**collection**](collection-level-custom-domain.md)**, or** [**space**](space-level-custom-domain.md) **level) (you are here)**
4. [Configuring DNS](../configure-dns.md)
5. [Confirming the custom domain setup](../finalize.md)
{% endhint %}

{% hint style="warning" %}
Before you'll be able to set a custom domain for your organization, **at least one space owned by the organization will need to be published**. If all of the spaces are unpublished, you won't see the publishing section on the organization settings page.
{% endhint %}

You'll find the options for setting a custom domain for an organization within the organization settings page. To get there, open the settings menu. This is located at the bottom of the sidebar — click on the cog ![](../../../.gitbook/assets/settings.png) icon to open the menu. Then, click on the **\[Org Name] Settings** link. It will look something like this:

<figure><img src="../../../.gitbook/assets/org-settings.png" alt=""><figcaption><p>Accessing the organization settings</p></figcaption></figure>

On the next page, in the **Publishing** section, next to **Custom Domain**, click the **Connect a domain** button.

<figure><img src="../../../.gitbook/assets/org-set-custom-domain.png" alt=""><figcaption><p>An organization's settings page with the custom domain section highlighted</p></figcaption></figure>

This will open up a window where you can enter the custom domain, and then click the **Next: Configure DNS** button:

<figure><img src="../../../.gitbook/assets/org-enter-subdomain.png" alt=""><figcaption><p>Connect a custom domain</p></figcaption></figure>

We'll then provide the name and value to use in the next step when you create your CNAME DNS record. You can copy the name or value to your clipboard by clicking on the icon on the right-hand side of each field.

<figure><img src="../../../.gitbook/assets/configure-dns.png" alt=""><figcaption><p>The name and value for the CNAME record</p></figcaption></figure>

The value for the CNAME record will be in the format `[something]-hosting.gitbook.io`, where that `[something]` will be **unique to you**. Make sure to use the value displayed to you in the GitBook app, and _not_ the value in the screenshot above! 🙂

Now, you're ready to move onto the next step: [configuring DNS](../configure-dns.md).
