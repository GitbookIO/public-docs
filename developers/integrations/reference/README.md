---
description: Install the GitBook CLI to build and publish integrations
---

# Install the CLI

The CLI can be used to create, test and publish integrations for GitBook’s integration platform. To start using the CLI, you’ll first need to install it globally on your machine:

```bash
npm install @gitbook/cli -g
```

After installing the CLI, you’ll need to authenticate your user in order to create and publish an integration.

To authenticate your user, run:

```bash
gitbook auth
```

This will prompt you to add your developer token from your GitBook account. You can generate a personal developer token in your [GitBook Developer settings](https://app.gitbook.com/account/developer).

To skip the prompt, for example in CI, over SSH, or in an AI agent sandbox, pass the token directly:

```bash
gitbook auth --token <token>
```

{% hint style="info" %}
You can also sign in through your browser with `gitbook login`. Browser sign-in works for everyday CLI commands, but publishing an integration (`gitbook integration publish` / `unpublish`) requires a personal access token, so use `gitbook auth` for integration work. If you've already signed in with gitbook login, run gitbook logout first, then gitbook auth. See the [GitBook CLI guide](https://gitbook.com/docs/docs-as-code/gitbook-cli) for more.
{% endhint %}

After authenticating your user, you’ll be able to bootstrap an integration, publish an integration, and more. Refer to the [Quickstart](../quickstart.md) to learn more about building an integration using the CLI.
