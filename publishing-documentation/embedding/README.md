---
description: Embed your documentation in your product or website using the Docs Embed.
icon: window-restore
---

# Embed in your product

The Docs Embed is a powerful window into your product knowledge that you can add to any product or website. Users can ask their questions to the [GitBook Assistant](../gitbook-ai-assistant.md) or browse your docs directly, without leaving your product. You can open the Embed with a button, put it in any component you want, or control it completely programatically.

<div data-with-frame="true"><figure><img src="../../.gitbook/assets/emebeddable_assistant.png" alt="Embed GitBook Assistant into your product or website"><figcaption><p>Embed your docs into your product or website</p></figcaption></figure></div>

## Overview

The Docs Embed consists of multiple tabs that get shown automatically, depending on your site's configuration:

* **Assistant**: The [GitBook Assistant](../gitbook-ai-assistant.md) - an AI-powered chat interface to help users find answers
* **Docs**: A browser for navigating your documentation site

You can customize and override the default configuration with custom actions, tools, suggested questions, [Authenticated Access](../authenticated-access/), and more.

## Get started

{% stepper %}
{% step %}
#### Prerequisites

Before embedding your docs, ensure:

1. **Your docs are published** and accessible at a URL (e.g., `https://docs.company.com`).
2. **You have retrieved the embed script URL** from your site settings (Settings → AI & MCP → Embed).

{% hint style="info" %}
If you want to use the Assistant tab, [GitBook Assistant must be enabled](../gitbook-ai-assistant.md) for your docs site (Settings → AI & MCP).
{% endhint %}
{% endstep %}

{% step %}
#### Implementation

Pick the approach that matches your setup:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3><i class="fa-code">:code:</i></h3></td><td><strong>Standalone script tag</strong></td><td>Drop in a &#x3C;script> tag for the fastest setup, then customize its appearance</td><td><a href="implementation/script.md">script.md</a></td></tr><tr><td><h3><i class="fa-box">:box:</i></h3></td><td><strong>Node.js/NPM</strong></td><td>Install via NPM for server-side rendering or build-time control</td><td><a href="implementation/nodejs.md">nodejs.md</a></td></tr><tr><td><h3><i class="fa-react">:react:</i></h3></td><td><strong>React component</strong></td><td>Use prebuilt React components for seamless integration</td><td><a href="implementation/react.md">react.md</a></td></tr></tbody></table>

{% hint style="info" %}
If your docs use [Authenticated Access](../authenticated-access/), follow the steps in [how to set up the embed with authenticated docs](authentication/using-with-authenticated-docs.md).
{% endhint %}
{% endstep %}

{% step %}
#### Configuration

* [Customizing the Embed](configuration/customizing-docs-embed.md) – Add welcome messages, custom actions, and suggestions
* [Creating custom tools](configuration/creating-custom-tools.md) – Connect Assistant to your product APIs
{% endstep %}
{% endstepper %}

## Further reading

For the complete API reference and source code, see the [`@gitbook/embed` package on GitHub](https://github.com/GitbookIO/gitbook/tree/main/packages/embed).
