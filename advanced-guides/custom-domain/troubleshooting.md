---
description: >-
  Helping you to solve some of the most common issues when setting up a custom
  domain.
---

# Troubleshooting

On this page we'll walk through some of the most common issues that folks run into when setting a custom domain, and explain how to solve them.

<details>

<summary>SSL error: an error occurred when provisioning your SSL certificate.</summary>

When a custom domain is set for your organization, collection, or space, we set up an SSL certificate on our end so that your documentation will load securely, over HTTPS. This happens automatically when you set your custom domain — you do not need to purchase or configure an SSL certificate yourself.

Sometimes, though, there can be a problem at the stage where we set up the SSL certificate. Most often when this happens the issue is that the CNAME record for the custom domain has not fully taken effect, or _propagated_, yet.

In these cases, we can recommend the following:

1. Check that your CNAME record is set up correctly. Please review our page about [configuring DNS](configure-dns.md) to help you with this. If the CNAME record is incorrect, we will never be able to configure the SSL certificate and complete the setup of your custom domain. The value for the CNAME record will be displayed to you in the GitBook app, and will be in the format `[something]-hosting.gitbook.io` (where that `[something]` will be unique to you).
2. Allow at least one hour between [configuring the CNAME record](configure-dns.md) and [finalizing the custom domain setup](finalize.md). This is because in _most_ cases, propagation will complete within one hour.
3. Try using a third-party DNS lookup tool, such as [WhatsMyDNS](https://www.whatsmydns.net/), to find out what value servers located all around the world believe to be correct for your CNAME record. Type or paste your subdomain into the field, choose CNAME from the dropdown, and click on the search button. As propagation progresses, more and more servers will return the result that you expect. When the vast majority of these servers are reporting back the result that you expect, you can try moving onto the step of [finalizing the custom domain setup](finalize.md).

If after trying those steps you are still having any trouble, please [contact the support team](../../troubleshooting/support.md). In your message, please make sure to share:

1. The subdomain that you would like to set as a custom domain; and
2. The name of the organization, collection, or space for which you would like to set it.

</details>

<details>

<summary>Domain already connected error: your subdomain is already configured for different content.</summary>

The custom domain that you set for an organization, collection, or space needs to be unique. It is not possible to set the same custom domain in multiple places and, if you try to do so, you'll run into this error.

If this happens, you can click on the link within the error message to take a look at the content that the custom domain is already connected to. This may help you to decide what to do next. It's also possible that you might not have access to the connected content — if that's the case, [contact the support team](../../troubleshooting/support.md) and they can help you with your next steps.

The solution to this error will always be one of two things, however:

1. Choose a different custom domain; or
2. Disconnect the custom domain from the content it is already connected to, and then reconnect it to the new content.

</details>

<details>

<summary>The custom domain is set correctly, but is redirecting to a different custom domain.</summary>

This is _probably_ expected behaviour, but is something that you can change!

The issue here is typically that custom domains have been set in more than one place. Keep in mind that when someone accesses the URL for an organization, they are taken straight to the organization's default content. And likewise, when someone accesses the URL for a collection, they are taken straight to the collection's default space. So, consider these examples:

#### Example 1

`docs.example.com` is set as the custom domain for an organization, and `team.example.com` is set as the custom domain for that organization's default content. In this case, it would be expected that visiting `docs.example.com` would take you straight to `team.example.com`.

One solution here could be to remove both docs.example.com and team.example.com and then re-add docs.example.com at the space-level.

#### Example 2

`products.example.com` is set as the custom domain for a collection, and `product1.example.com` is set as the custom domain for that collection's default space. In this case, it would be expected that visiting `products.example.com` would take you straight to `product1.example.com`.

So, whenever you set custom domains, make sure to consider this cascading effect when [deciding where to set each custom domain](location.md). If you see one custom domain redirecting to another, check what's happening with custom domains at the organization-, collection-, and space-level. If, after checking, you still have questions, feel free to [contact the support team](../../troubleshooting/support.md).

</details>
