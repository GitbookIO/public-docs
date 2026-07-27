# Authenticating

Sign in once and the CLI stores your credentials locally, refreshing them as needed.

{% tabs %}
{% tab title="Browser (OAuth)" %}
The quickest way to sign in:

```bash
gitbook login
```

This opens GitBook in your browser, asks you to authorize the CLI, and stores the resulting token locally. This is the recommended path for everyday use.
{% endtab %}

{% tab title="Personal API token" %}
To skip the browser flow — for CI, scripts, or publishing integrations — authenticate with a personal API token instead. Create one at [app.gitbook.com/account/developer](https://app.gitbook.com/account/developer), then run:

```bash
gitbook auth --token <token>
```

If you omit `--token`, the CLI prompts you for it.
{% endtab %}
{% endtabs %}

Confirm who you're signed in as at any time:

```bash
gitbook whoami
```

To sign out, run `gitbook logout`.

{% hint style="warning" %}
Publishing integrations (`gitbook integration publish` / `unpublish`) requires a personal API token — a browser (OAuth) session can't perform those operations. Run `gitbook auth --token <token>` for publishing workflows. The two credentials can coexist: use browser sign-in for everyday commands, and a token for publishing.
{% endhint %}