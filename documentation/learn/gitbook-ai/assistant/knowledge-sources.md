---
description: Connect external knowledge sources so GitBook Assistant can answer from more than your docs.
---

# Connect knowledge sources

{% hint style="info" %}
Connections are in beta, and priced as an add-on.
{% endhint %}

GitBook Assistant can extend its knowledge beyond your docs using **connections** and **MCP servers**:

| | Best for |
|---|---|
| **Connections** | Content-heavy sources: GitHub issues and discussions, Slack or Discord conversations, support content, external docs, help centers, and websites. |
| **MCP servers** | Live tools and data: current account/product state, internal systems that change often, actions like creating tickets or filing bugs, or sources you don't want to sync into GitBook. |

{% tabs %}
{% tab title="Add a connection" %}
{% stepper %}
{% step %}
#### Open your site's settings

**Settings → Connections**.
{% endstep %}

{% step %}
#### Connect a source

Choose a source type, then authorize it or enter the URL to import.
{% endstep %}

{% step %}
#### Expose records to GitBook Assistant

Turn on **Expose in search / assistant** for the connection, so GitBook can use those records in search and Assistant.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Add an MCP server" %}
{% stepper %}
{% step %}
#### Open your site's settings

**Settings → AI & MCP**.
{% endstep %}

{% step %}
#### Add a new server

In the MCP servers table, click **Add MCP server**.
{% endstep %}

{% step %}
#### Enter the server details

Name the server, add its URL, and configure any HTTP headers GitBook must send with each request.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

## How connections work

{% stepper %}
{% step %}
#### Connect a source

Select a source type, then authorize it or enter the URL you want GitBook to import.

{% hint style="info" %}
Connecting YouTube? Enter the **channel ID**, not the channel name — find it in YouTube Studio under **Settings → Channel → Advanced settings**. If your channel URL contains `/channel/`, copy the part after it.
{% endhint %}

Each connection creates a stream of records from that source — issues, discussions, tickets, conversations, pages, or videos.
{% endstep %}

{% step %}
#### GitBook syncs records

After saving, GitBook starts syncing records. Review sync status, record count, and last sync time in the connections list. Connected URLs refresh once a day by default, or trigger a manual refresh from **Settings → Connections**.
{% endstep %}

{% step %}
#### Choose how records are used

For each connection, choose whether its records appear in search and Assistant, and whether they help generate change requests. You can also adjust the connection's search ranking to prioritize or deprioritize its records.
{% endstep %}
{% endstepper %}

### Connection settings

**Label** — a clear name for the connection, useful when you connect multiple repositories, websites, or channels.

**Auto-generate change requests** *(early access)* — lets GitBook learn from a connection's records and suggest documentation updates as change requests for your team to review. See [Run an Agent audit](../agent/run-an-audit.md).

**Expose in search / assistant** — makes records from this connection searchable by visitors and available to answer questions, appearing in your site's AI-powered search and Assistant responses.

{% hint style="warning" %}
Enabling this makes records from that connection available to anyone who can access the site — including external visitors, if the site is shared externally.
{% endhint %}

**Search ranking boost** — prioritize or deprioritize a connection's records in search. Increase it if a source should appear more often; lower it if it should carry less weight than your primary docs.

## Available connections

<table><thead><tr><th></th><th></th></tr></thead><tbody>
<tr><td><strong>Intercom</strong></td><td>Available</td></tr>
<tr><td><strong>Zendesk</strong></td><td>Available</td></tr>
<tr><td><strong>Pylon</strong></td><td>Available</td></tr>
<tr><td><strong>GitHub Discussions</strong></td><td>Available</td></tr>
<tr><td><strong>GitHub Issues</strong></td><td>Available</td></tr>
<tr><td><strong>Freshdesk, Front, HubSpot, Zoho Desk, YouTube, Website</strong></td><td>Listed in the connections picker</td></tr>
</tbody></table>

### Intercom, Zendesk, and Pylon

These three connectors work the same way — conversations from the connected tool can be passed as context to [GitBook Assistant](README.md), and Agent can [identify content gaps](../agent/run-an-audit.md) from resolved conversations.

**What we store:** GitBook only indexes resolved conversations with at least one reply from a human or AI support agent — it doesn't index open, unresolved, or spam conversations. GitBook stores only the conversation itself (no metadata or user information), and redacts sensitive information before storage.

**How to connect:**

* **Intercom** — requires an API key with read access to conversations. You own and control this key's scope and expiry.
* **Zendesk** — requires your Zendesk subdomain (e.g. `gitbook.zendesk.com`) and an API key with read access to conversations.
* **Pylon** — requires credentials with read access to conversations.

### GitHub Issues and GitHub Discussions

Issues and discussions from your repositories can be passed as context to [GitBook Assistant](README.md), and Agent can [identify content gaps](../agent/run-an-audit.md) from resolved issues or discussions.

**What we store:** GitBook only indexes resolved issues, and resolved discussions with at least one reply — it doesn't index open items or spam. GitBook stores only the conversation (no metadata or user information), and redacts sensitive information before storage.

**How to connect:** requires credentials with read access to issues and/or discussions.

### Slack and Discord

{% hint style="info" %}
Not yet available as a connection.
{% endhint %}

### External documentation sites

{% hint style="info" %}
Not yet available as a connection.
{% endhint %}

### MCP servers as sources

Connect an MCP server so Assistant can query live systems and data, rather than synced records — see [Add an MCP server](#add-an-mcp-server) above.

## Data retention and privacy

**What does GitBook index?** Content from your connections, used across search, change requests, and other content-driven features. Each indexed item is a **record** — an Intercom ticket, a website page, and so on. Records help suggest content changes and provide context to agents running across GitBook.

GitBook retains records as long as the source stays connected. Removing a connection deletes all its stored records — but not content already generated using those records as context, or record content already in stored AI conversation logs. For example, if GitBook suggests a doc change based on a closed Intercom ticket and you later remove the Intercom connection, the Intercom-specific stored data is deleted, but the resulting change request remains.

<details>

<summary>What is your policy around PII?</summary>

GitBook generally only requests source fields it can use as context (see each connector's notes above for specifics). Every ingested record passes through PII redaction: first an in-memory redaction of emails, phone numbers, addresses, and other personal information, then a second pass using a third-party LLM under a ZDR-compliant, no-store request — not stored on the third party's servers, and not used for training. PII may exist on GitBook's servers for a few minutes during this pre-processing, but only the post-processed record is stored.

</details>

<details>

<summary>Do you send data to any third parties?</summary>

A third party is used to redact PII after GitBook's initial internal redaction. Redacted record content is also used with third-party providers when creating change requests and responding to user questions — for example, GitBook Agent may include content from an external record as additional context when writing.

</details>

<details>

<summary>Does GitBook use data for model training, itself or via third parties?</summary>

No — GitBook doesn't use record data for training, and verifies with third-party providers that they don't either.

</details>

<details>

<summary>Can I limit which records GitBook fetches?</summary>

See each connector's notes above for what's configurable per source.

</details>
