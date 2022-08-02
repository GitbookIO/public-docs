# Choose a subdomain

{% hint style="info" %}
This is **step 1** of a 3-step process for setting up a custom domain. Make sure to follow the steps in the correct order!

1. Choose a subdomain (you are here)
2. [Configure DNS](dns-configuration.md)
3. [Set the custom domain in GitBook](custom-domain-setup-on-gitbook.md)
{% endhint %}

_Only_ subdomains can be used to serve your documentation. It's not possible to use an apex domain.

Here are some examples of what you could and could not choose — just replace `example.com` with your own domain:

| Domain type      | Example                                                                                                       | Supported? |
| ---------------- | ------------------------------------------------------------------------------------------------------------- | :--------: |
| Apex domain      | `example.com`                                                                                                 |      ❌     |
| `www` subdomain  | `www.example.com`                                                                                             |      ✅     |
| Custom subdomain | <p><code>docs.example.com</code></p><p><code>help.example.com</code><br><code>anything.example.com</code></p> |      ✅     |

Once you've chosen your subdomain, you can move onto [step 2: configuring DNS](dns-configuration.md).
