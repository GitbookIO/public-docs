# Choosing a subdomain

{% hint style="info" %}
Please follow the steps to set a custom domain in this order:

1. [**Choosing a subdomain**](choose.md) **(you are here)**
2. [Deciding where to set the custom domain](location.md)
3. [Initiating the custom domain setup](initiate/) (at the [organization](initiate/organization-level-custom-domain.md), [collection](initiate/collection-level-custom-domain.md), or [space](initiate/space-level-custom-domain.md) level)
4. [Configuring DNS](configure-dns.md)
5. [Confirming the custom domain setup](finalize.md)
{% endhint %}

_Only_ subdomains can be used to serve your GitBook documentation. It's not possible to use an apex domain.

Here are some examples of what you could and could not choose — just replace `example.com` with your own domain:

| Domain type      | Example                                                                                                       | Supported? |
| ---------------- | ------------------------------------------------------------------------------------------------------------- | :--------: |
| Apex domain      | `example.com`                                                                                                 |      ❌     |
| `www` subdomain  | `www.example.com`                                                                                             |      ✅     |
| Custom subdomain | <p><code>docs.example.com</code></p><p><code>help.example.com</code><br><code>anything.example.com</code></p> |      ✅     |

Once you have chosen your custom domain, you're ready to move onto the next step: [deciding where to set the custom domain](location.md).
