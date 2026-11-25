---
description: Authenticate your requests with your user account when using the GitBook API
---

# Authentication

The GitBook API uses personal access tokens to authenticate requests.

You can view and manage your access tokens in the [Developer settings](https://app.gitbook.com/account/developer) of your GitBook user account.

API requests are authenticated using the [Bearer Auth scheme](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#authentication_schemes). To authenticate a request, provide the token in the `Authorization` header of the request:

```bash
curl -H "Authorization: Bearer <your_access_token>" https://api.gitbook.com/v1/user
```

Access tokens are tied to the GitBook user account for which they were created. A token can never do more than that account can.

{% hint style="warning" %}
Please be sure to keep your API access tokens secure! Do not share them in emails, chat messages, client-side code or publicly accessible sites.

If you have accidentally shared an API access token publicly, you can revoke it in the [Developer settings](https://app.gitbook.com/account/developer) of your GitBook user account by deleting it. Open the token’s **⋯** menu and choose **Delete**.
{% endhint %}

## Token access

When you create a token, you choose its access:

* **Read only**: the token can only read. The API refuses any request that would change something. Use this for dashboards, reporting scripts, and anything that doesn’t need to change content.
* **Read & write**: the token can read and change everything your account can access. This is the default, and tokens created before access levels existed have this access.

Choose read only unless the integration needs to write. If a read-only token is exposed, it can’t change your content.

## Restrict a token by IP address

You can allow or deny specific IP ranges for a token. Use this to limit a token to your CI runners or office network.

To add a rule when you create a token, click **Add rule**, choose **Allow** or **Deny**, and enter an IP address or CIDR range. With no rules, the token works from any IP address.

You can’t change a token’s access or IP rules after you create it. To change them, delete the token and create a new one. To see a token’s rules, open its **⋯** menu and choose **Details** in [Developer settings](https://app.gitbook.com/account/developer).
