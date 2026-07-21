---
description: Connect external sources to GitBook Assistant and GitBook Agent
icon: link-simple
tags:
  - beta
  - add-on
---

# Connections

Connections let you bring external content into your docs site.

Connected content can appear in [AI Search](../../docs-site/ai-search.md) and [GitBook Assistant](../gitbook-ai-assistant.md). Some connections can also help GitBook generate change requests.

To add a connection, open your site’s **Settings** and click on **Connections**.

<figure><img src="../../.gitbook/assets/2026-07-13_connections@2x.png" alt=""><figcaption></figcaption></figure>

### Available connections

You can connect support platforms, developer communities, and other content sources:

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4>Intercom</h4></td><td><a href="intercom.md">intercom.md</a></td></tr><tr><td><h4>Zendesk</h4></td><td><a href="zendesk.md">zendesk.md</a></td></tr><tr><td><h4>Freshdesk</h4></td><td></td></tr><tr><td><h4>Front</h4></td><td></td></tr><tr><td><h4>HubSpot</h4></td><td></td></tr><tr><td><h4>Zoho Desk</h4></td><td></td></tr><tr><td><h4>Pylon</h4></td><td><a href="pylon.md">pylon.md</a></td></tr><tr><td><h4>GitHub Discussions</h4></td><td><a href="github-discussions.md">github-discussions.md</a></td></tr><tr><td><h4>GitHub Issues</h4></td><td><a href="github-issues.md">github-issues.md</a></td></tr><tr><td><h4>YouTube</h4></td><td></td></tr><tr><td><h4>Website</h4></td><td></td></tr><tr><td><h4>MCP server</h4></td><td></td></tr></tbody></table>

### How connections work

{% stepper %}
{% step %}
#### Connect a source

Select a source type. Then authorize it, or enter the URL you want GitBook to import.

{% hint style="info" %}
If you connect YouTube, enter the channel ID — not the channel name.

A channel name won't work for this source.

In YouTube Studio, open **Settings** → **Channel** → **Advanced settings**.

Copy the **Channel ID**.

If your channel URL contains `/channel/`, copy the part after `/channel/`.
{% endhint %}

Each connection creates a stream of records from that source, such as issues, discussions, tickets, conversations, pages, or videos.
{% endstep %}

{% step %}
#### GitBook syncs records

After you save the connection, GitBook starts syncing records from that source.

In the connections list, you can review the sync status, record count, and last sync time.

Connected URLs refresh once a day by default. You can also trigger a refresh manually from your site’s **Settings** → **Connections**.
{% endstep %}

{% step %}
#### Choose how the records are used

For each connection, you can choose whether its records appear in search and GitBook Assistant, and whether they help GitBook generate change requests.

You can also adjust the connection’s search ranking to prioritize or deprioritize its records.
{% endstep %}
{% endstepper %}

### Connection settings

When you edit a connection, you can configure these options:

#### Label

Use **Label** to give the connection a clear name.

This makes the source easier to identify in the connections list, especially if you connect multiple repositories, websites, or channels.

#### Auto-generate change requests

{% hint style="warning" %}
Auto generating change requests is currently in early access.

See [automatic-docs-improvements.md](../../gitbook-agent/automatic-docs-improvements.md "mention") for information on requesting access
{% endhint %}

Turn on **Auto-generate change requests** to let GitBook learn from the connection’s records and suggest documentation updates.

GitBook can use those records to create change requests with suggested changes for your team to review.

#### Expose in search / assistant

Turn on **Expose in search / assistant** to make records from this connection searchable by visitors and available to answer questions.

This allows connected content to appear in your site’s AI-powered search experience and in GitBook Assistant responses.

{% hint style="warning" %}
Enabling **Expose in search / assistant** makes records from that connection available to anyone who can access the site — including external visitors if the site is shared externally.
{% endhint %}

#### Search ranking boost

Use **Search ranking boost** to prioritize or deprioritize records from a connection in search.

Increase the value if this source should appear more often. Lower it if this source should have less weight than your primary docs.

### Data retention and privacy

#### What does GitBook index?

GitBook indexes content from your connections and uses it across search, change requests, and other content-driven features. Each item we index from a connection is called a **record.** Examples of records are Intercom tickets, Freshdesk tickets, website pages, and more.

We use records to suggest content changes and provide additional context to agents running across GitBook.

We retain records for as long as the source remains connected. If you remove the connection, we delete all stored records. We do not delete any content that was generated using those records as context, or remove the content of records from any stored AI conversation logs.

For example, you might connect Intercom and GitBook suggests a documentation change based on a closed Intercom support ticket. If you then remove the Intercom connection, all our Intercom specific stored data is deleted, but the change requests will remain.

More information about our connectors can be found on the specific page for each connector.

#### FAQ

<details>

<summary>What is your policy around PII?</summary>

Generally, GitBook only requests source fields that it can use as context (see connector pages for more specifics on each source).

When we ingest a record, we pass it through PII redaction processes. The first is an in-memory redaction of any emails, phone numbers, addresses, and other personal information.

We then pass the record through a 2nd PII step using a 3rd party LLM. This is a ZDR-compliant, no-store request that is not stored on the servers of our 3rd party and is not used in any training.

PII may exist on our servers for a few minutes whilst we do this pre-processing, but we only store the post-processed record.

</details>

<details>

<summary>Do you send data to any 3rd parties?</summary>

We use a 3rd party to redact PII after our initial, internal PII redaction is done.

We also use the redacted record content in 3rd party providers when creating change requests and responding to user questions.

For example, when writing content with GitBook Agent, the agent may include content from an external record as additional context.

</details>

<details>

<summary>Does GitBook use data for any model training, either itself or via 3rd parties</summary>

No, we do not use record data for training and verify with our 3rd party providers that they do not either.

</details>

<details>

<summary>Can I limit which records GitBook fetches?</summary>

See our specific connector pages for what can be configured for each source.

* [Intercom](intercom.md)
* [Zendesk](zendesk.md)
* Freshdesk
* Front
* HubSpot
* Zoho Desk
* [Pylon](pylon.md)

</details>
