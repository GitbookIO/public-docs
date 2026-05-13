# Example complete page

A complete worked example showing multiple GitBook features in one page: hints, tabs, steppers, columns, expandable details, and a button. Use this as a reference shape when scaffolding feature-rich documentation pages.

For broader content patterns (which block to reach for in which situation), see `block-ecosystem.md`. For each block's full syntax, see `custom-blocks.md`. For larger production-style examples spanning many files, see `references/example-site/`.

## The page

````markdown
# API Authentication Guide

Learn how to authenticate with our API using API keys or OAuth 2.0.

{% hint style="info" %}
All API requests require authentication. Choose the method that best fits your use case.
{% endhint %}

## Authentication Methods

{% tabs %}
{% tab title="API Key" %}
The simplest authentication method. Include your API key in the request header:

```bash
curl -H "X-API-Key: your-api-key" https://api.example.com/v1/users
```

{% hint style="warning" %}
Never commit API keys to version control. Use environment variables instead.
{% endhint %}
{% endtab %}

{% tab title="OAuth 2.0" %}
More secure for user-facing applications:

{% stepper %}
{% step %}
## Register your application

Get your client ID and secret from the developer dashboard.
{% endstep %}

{% step %}
## Request authorization

Redirect users to our OAuth endpoint.
{% endstep %}

{% step %}
## Exchange code for token

Use the authorization code to get an access token.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

## Rate Limits

{% columns %}
{% column %}
### Free Tier

- 1,000 requests/hour
- 10,000 requests/day
{% endcolumn %}

{% column %}
### Pro Tier

- 10,000 requests/hour
- 100,000 requests/day
{% endcolumn %}
{% endcolumns %}

<details>
<summary>Need higher limits?</summary>

Contact our sales team to discuss enterprise plans with custom rate limits and SLAs.
</details>

<a href="https://example.com/signup" class="button primary" data-icon="rocket">Get Started</a>
````

## What this example demonstrates

- **Top-level hint** for a "must-read" piece of context before the page proper begins
- **Tabs** as the primary structural choice when two distinct authentication paths each have their own workflow
- **Nested hint inside a tab** for the security warning specific to the API-key path
- **Stepper inside the OAuth tab** for the ordered exchange flow
- **Columns** to compare two parallel rate-limit tiers without needing a markdown table
- **Expandable (`<details>`)** for a CTA-style aside that doesn't need to be visible up front
- **Button** as the final call-to-action

Notice that the page uses **zero plain markdown tables and zero "## YYYY-MM-DD"-style structural prose** — everything that could be a block, is one. That's the default to aim for.
