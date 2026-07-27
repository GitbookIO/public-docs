# Authenticating

The GitBook API uses personal access tokens to authenticate requests. View and manage your access tokens in your [Developer settings](https://app.gitbook.com/account/developer).

API requests are authenticated using the [Bearer Auth scheme](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#authentication_schemes). Provide the token in the request's `Authorization` header:

```bash
curl -H "Authorization: Bearer <your_access_token>" https://api.gitbook.com/v1/user
```

Access tokens are tied to the GitBook user account that created them — **a token provides the same level of access and privileges that its associated user account would have.**

{% hint style="warning" %}
Keep your API access tokens secure. Don't share them in emails, chat messages, client-side code, or publicly accessible sites.

If you accidentally share a token publicly, revoke it in your [Developer settings](https://app.gitbook.com/account/developer) by clicking the "X" button beside it.
{% endhint %}