# 1. Choose a subdomain and its location

Here are some examples of domains you can set in GitBook.&#x20;

| Domain type      | Example                                                                                                       | Supported? |
| ---------------- | ------------------------------------------------------------------------------------------------------------- | :--------: |
| Apex domain      | `example.com`                                                                                                 |      ❌     |
| `www` subdomain  | `www.example.com`                                                                                             |      ✅     |
| Custom subdomain | <p><code>docs.example.com</code></p><p><code>help.example.com</code><br><code>anything.example.com</code></p> |      ✅     |

## Decide where to set the custom domain

There are two levels at which a custom domain can be set:

1. At the **organization level**
2. At the **docs site** level

{% hint style="warning" %}
**Your URL path will depend on where you set the domain.**&#x20;
{% endhint %}

## Organization custom domains

Because organizations can contain many sites (and internal spaces) any custom domain set for the organization will apply to all published sites unless overridden.&#x20;

{% hint style="info" %}
Each published site will follow after your organization's domain

**`Org-domain/site-name/page-group/page`**
{% endhint %}

If you’ve decided that you want to set a custom domain at the organization level, you can [go to the next step](organization-level-custom-domain.md) for details on how to set it. If you’re not sure, keep reading to review your other options.

## Site custom domains

If you want to set up a domain different from your main organization domain, or you want to maintain a shorter URL path, you should set the domain directly at a site level.

For example, the domains set for _Site A_ and _Site B_ could be:&#x20;

* `site-a-domain/page-group/page`
* `site-b-domain/page-group/page`

{% hint style="info" %}
Domains set at a site level will have the following path

If no page groups are used: **`site-domain/page`**

(Or, if page groups are used:**`site-domain/page-group/page)`**
{% endhint %}

If you’ve decided that you want to set a custom domain at the organization level, you can [go to the next step](organization-level-custom-domain.md) for details on how to set it. If you’re not sure, keep reading to review your other options.
