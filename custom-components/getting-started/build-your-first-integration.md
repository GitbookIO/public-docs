---
description: Scaffold, run, and publish your first GitBook integration.
---

# Build your first integration (Quickstart)

> **Tutorial.** Follow every step in order — at the end your integration will be installed and running in your own organization.

GitBook's developer platform lets you build integrations that connect GitBook to internal tools, third-party services, and custom workflows. You can use it to automate repetitive tasks, embed interactive components in pages, pull in data from other systems, and manage authentication programmatically.

{% stepper %}
{% step %}
#### Create a GitBook account

You need a GitBook account to use the developer platform. [Sign up for free](https://app.gitbook.com/join) if you don't already have one.
{% endstep %}

{% step %}
#### Create a personal access token

Create a personal access token in your [developer settings](https://app.gitbook.com/account/developer). This token represents your user, and lets you make API calls, create integrations, and publish them to spaces you're a part of to test them.

{% hint style="warning" %}
This token is specific to your user account — don't share it or use it outside your own machine.
{% endhint %}
{% endstep %}

{% step %}
#### Install the GitBook CLI

The CLI requires Node v18 or later.

```bash
npm install @gitbook/cli -g
```

Authenticate the CLI with your personal access token:

```bash
gitbook auth
```
{% endstep %}

{% step %}
#### Scaffold your integration

Bootstrap your first integration by running the following in your terminal:

```bash
gitbook new
```

You'll be prompted for a `name`, `title`, `organization`, and `scopes`.

{% hint style="warning" %}
To publish your integration, it must have a unique `name` and an `organization` id that your authenticated user is a member of.
{% endhint %}

This generates a project with a `gitbook-manifest.yaml` file and an entry script — open it in your IDE and you're ready to build.
{% endstep %}

{% step %}
#### Publish it

Before you can develop your integration locally, you need to publish it once. From the root of your integration, run:

```bash
gitbook publish
```

By default your integration publishes privately, owned by the organization set in the manifest. This command returns a link you can use to install it.
{% endstep %}

{% step %}
#### Run it locally

Install your integration into at least one space or site using the link from the previous step, then start a local development server:

```bash
gitbook dev
```

This ties a development server to your organization. All integration traffic is now served from your local machine instead of the published version — you don't need to visit the URL the command prints; instead, open the space or site you installed the integration into and interact with it there. Any UI changes need a browser refresh to show up, and it's worth [disabling browser caching](https://stackoverflow.com/a/7000899) while you work.
{% endstep %}

{% step %}
#### Install and see it work 🎉

Once you're happy with it, install your integration on a space or site (using the link from `gitbook publish`) and trigger it. When you see it respond, you've shipped your first integration.
{% endstep %}
{% endstepper %}

### Next steps

* [Integration concepts](../integration-concepts.md) — the vocabulary used throughout these docs.
* [ContentKit overview](../contentkit/contentkit-overview.md) — build custom UI components.
* Guides for unfurling links, interactive blocks, and receiving webhooks.
