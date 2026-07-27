---
description: Work with GitBook Agent from Slack, GitHub, and Linear.
---

# Use Agent in Slack, GitHub, and Linear

{% hint style="warning" %}
Channels are in early access, and access is rolling out gradually.
{% endhint %}

{% hint style="info" %}
Channels are available on the Ultimate plan.
{% endhint %}

Channels bring [GitBook Assistant](../assistant/README.md) and [GitBook Agent](README.md) into the tools your team already uses. Once connected, mention `@GitBook` in Slack, GitHub, or Linear to ask questions, open change requests, and keep your docs up to date without leaving your workflow.

{% hint style="info" %}
Looking to embed GitBook Assistant in your own website or product instead? See [Embed GitBook in your product](../../embed/README.md).
{% endhint %}

### Roles and permissions

Each channel configuration runs in one of two modes — you can run multiple configurations per channel, e.g. Support agent mode for a customer-facing Slack channel, Collaborator mode for your docs team's channel.

**Support agent** — GitBook Assistant answers questions from your team or visitors directly in the channel, pulling from your docs. In Slack, citations link to the published site URL for the docs referenced (not `app.gitbook.com`). Read-only — it doesn't make content changes.

**Collaborator** — GitBook Agent joins as a teammate. Mention `@GitBook` to open change requests, request edits, or keep docs in sync with what's happening in that tool. In Slack, messages can link to `app.gitbook.com` when referencing internal workflow context, like a change request or draft. When Agent creates a change request from a channel, it automatically links it back to the originating thread, issue, or pull request.

Use Channels when support questions, bug reports, or product feedback start in Slack, GitHub, or Linear, and you want GitBook to respond in place — turning conversations that started outside GitBook into docs updates.

### Supported platforms

* **Slack** — conversations and support threads.
* **GitHub** — issues, pull-request context, and discussion workflows.
* **Linear** — issue tracking and product feedback workflows.

Each platform uses the same core model: GitBook receives supported events, gathers context from your knowledge, and responds through Assistant or Agent depending on the channel's role.

{% hint style="info" %}
**Coming soon:** Discord, Intercom, Microsoft Teams, Google Chat. [Request a channel](https://github.com/orgs/GitbookIO/discussions/new?category=feature-requests).
{% endhint %}

### How it works

{% stepper %}
{% step %}
#### Receive an event

The connected platform sends a supported event — a new message, a mention, an issue update, or similar — to GitBook through the installed channel.
{% endstep %}

{% step %}
#### Gather context

GitBook looks up relevant docs context and any other available knowledge for the site.
{% endstep %}

{% step %}
#### Apply the channel role

A **Support agent** channel returns read-only information. A **Collaborator** channel can also turn the conversation into docs work through GitBook Agent.
{% endstep %}

{% step %}
#### Reply in the source tool

The response appears back in Slack, GitHub, or Linear, keeping the workflow in one place.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Exact event coverage depends on the platform and your early access rollout.
{% endhint %}

### Install and authorization

Open your site's **Settings** → **Channels**, and choose the platform to connect. Each uses an OAuth or app-install flow — GitBook sends you to the platform, you approve access, then return to finish setup.

{% hint style="warning" %}
Review the authorization screen carefully before approving access — platform-specific permission scopes and admin requirements can vary.
{% endhint %}

{% tabs %}
{% tab title="Slack" %}
{% stepper %}
{% step %}
#### Start the install

In **Settings → Channels**, select **Slack**.
{% endstep %}

{% step %}
#### Authorize Slack

Sign in if needed, choose the workspace to install into, and approve the requested access.
{% endstep %}

{% step %}
#### Finish setup in GitBook

After Slack redirects you back, choose the channel's role and save the configuration.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="GitHub" %}
{% stepper %}
{% step %}
#### Start the install

In **Settings → Channels**, select **GitHub**.
{% endstep %}

{% step %}
#### Authorize GitHub

Sign in if needed, choose the account or organization to install the GitBook app into, and approve access.
{% endstep %}

{% step %}
#### Finish setup in GitBook

After GitHub redirects you back, choose the channel's role and save the configuration.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Linear" %}
{% stepper %}
{% step %}
#### Start the install

In **Settings → Channels**, select **Linear**.
{% endstep %}

{% step %}
#### Authorize Linear

Sign in if needed, choose the workspace to connect, and approve access.
{% endstep %}

{% step %}
#### Finish setup in GitBook

After Linear redirects you back, choose the channel's role and save the configuration.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

### Feedback and reactions

Reactions let your team give quick feedback on channel replies, signaling whether a response was helpful — this helps GitBook understand which responses work well in real workflows.

{% hint style="info" %}
Exact reaction mapping isn't fully documented yet, and can vary by platform during early access.
{% endhint %}
