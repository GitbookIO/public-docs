# Deciding where to set the custom domain

{% hint style="info" %}
Please follow the steps to set a custom domain in this order:

1. ****[Choosing a subdomain](choose.md)
2. ****[**Deciding where to set the custom domain**](location.md) **(you are here)**
3. [Initiating the custom domain setup](initiate/) (at the [organization](initiate/organization-level-custom-domain.md), [collection](initiate/collection-level-custom-domain.md), or [space](initiate/space-level-custom-domain.md) level)
4. [Configuring DNS](configure-dns.md)
5. [Finalizing the custom domain setup](finalize.md)
{% endhint %}

There are three levels at which a custom domain can be set:

1. [At the organization level](location.md#organization-level-custom-domains)
2. [At the collection level](location.md#collection-level-custom-domains)
3. [At the space level](location.md#space-level-custom-domains)

This page provides more information about each of the options to help you decide where you want to set your custom domain.

## Organization-level custom domains

Because organizations contain collections and/or spaces, any custom domain set for the organization will have an effect on the domain for all collections and spaces within it, unless overridden by a custom domain set for a specific collection or space owned by the same organization.

It's important to note that **the custom domain you set will **_**not**_** be used as-is for any space within the organization**. Instead, each space will use the domain in this format: `[customdomain]/[spaceURL]`. The spaceURL part cannot be empty, and is set in the link and domain settings for each space.

If you've decided that you want to set a custom domain at the organization level, you can [go to the next step](initiate/) for the details on how to set it. If you're not sure, keep reading to review your other options.

## Collection-level custom domains

Because collections contain spaces, any custom domain set for the collection will have an effect on the domain for all spaces within it, unless overridden by a custom domain for a specific space within that collection.

It's important to note that **the custom domain you set will be used as-is for the **_**default**_** space in the collection**. Other spaces in the collection will have a URL in this format: `[yourcustomdomain]/v/[spaceURL]`. The spaceURL part cannot be empty, and is set in the link and domain settings for each space.

If you've decided that you want to set a custom domain at the collection level, you can [go to the next step](initiate/) for the details on how to set it. If you're not sure, keep reading to review your final option.

## Space-level custom domains

A custom domain set at the space level can override a custom domain set at the collection level (if the space is part of a collection) or at the organization level (if the space is owned by an organization).

The custom domain you set will be used exactly as-is for the space.

If you've decided that you want to set a custom domain at the space level, you can [go to the next step](initiate/) for the details on how to set it.
