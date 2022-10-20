# Finalizing the custom domain setup

{% hint style="info" %}
Please follow the steps to set a custom domain in this order:

1. ****[Choosing a subdomain](choose.md)
2. ****[Deciding where to set the custom domain](location.md)
3. [Initiating the custom domain setup](initiate/) (at the [organization](initiate/organization-level-custom-domain.md), [collection](initiate/collection-level-custom-domain.md), or [space](initiate/space-level-custom-domain.md) level)
4. [Configuring DNS](configure-dns.md)
5. ****[**Finalizing the custom domain setup**](finalize.md) **(you are here)**
{% endhint %}

Once your CNAME record has taken effect, or has _propagated_, you're ready to finalize the setup in GitBook.

If you're setting an organization-level custom domain, go back into the organization settings page, and click the **edit domain** button in the Publishing section.

If you're setting a collection- or space-level custom domain, go back into the **link and domain settings** for that collection or space. From there, click the **edit domain** button.

You'll see the same Connect a domain screen that you saw in step 3, with the custom domain you entered previously pre-filled. Click the **continue** button, and GitBook will again check the DNS settings behind the scenes. If we are able to confirm that the subdomain is correctly pointed to the value provided to you, you'll see the following success message:

<figure><img src="../../.gitbook/assets/connect-a-domain-success.png" alt=""><figcaption><p>Success!</p></figcaption></figure>

Congratulations! Visitors to your documentation can now use your custom domain to access it. 🎉

If you ever change your mind, you can always go back to the organization settings page or to the link and domain settings for a collection or space to edit or remove the custom domain.

If you follow the steps on this page and you don't see the success message, some more time might still be needed for the CNAME record to propagate. Try allowing about another hour before coming back to try it again, or review our [troubleshooting](troubleshooting.md) information if you still have trouble. Remember that it _can_ in some cases take up to 48 hours for the change to fully take effect.
