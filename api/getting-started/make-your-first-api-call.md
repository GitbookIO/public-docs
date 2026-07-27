# Make your first API call

{% stepper %}
{% step %}
#### Create a GitBook account

Sign up for free at [app.gitbook.com/join](https://app.gitbook.com/join) if you don't already have an account.
{% endstep %}

{% step %}
#### Create a personal access token

Create one in your [developer settings](https://app.gitbook.com/account/developer) — see [Authenticating](authentication.md). This token represents your user in GitBook, and lets you make API calls, create integrations, and publish them to any space you're part of to test them.

{% hint style="warning" %}
This token is specific to your user — don't share it for use outside your personal account.
{% endhint %}
{% endstep %}

{% step %}
#### Make your first call

The example below asks GitBook Assistant a question about a site in your organization, using the Ask API.
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="HTTP" %}
Send a POST request to `/v1/orgs/{organizationId}/sites/{siteId}/ask`, with your token for authentication and the question you want answered:

```http
POST /v1/orgs/{organizationId}/sites/{siteId}/ask HTTP/1.1
Host: api.gitbook.com
Authorization: Bearer YOUR_SECRET_TOKEN
Content-Type: application/json
Accept: */*

{
  "question": "How do I get started?",
  "scope": {
    "mode": "default"
  }
}
```

The API returns an answer generated from your site's content.
{% endtab %}

{% tab title="JavaScript" %}
Using [GitBook's client library](../reference/client-libraries.md):

```bash
npm install @gitbook/api
```

```javascript
import { GitBookAPI } from "@gitbook/api";

const ORGANIZATION_ID = "<your organization id>"
const SITE_ID = "<your site id>"
const API_TOKEN = "<your gitbook api token>"

const client = new GitBookAPI({
    authToken: API_TOKEN
});

const stream = await client.orgs.streamAskInSite(
    ORGANIZATION_ID,
    SITE_ID,
    {
        question: "How do I get started?",
        scope: {
            mode: "default",
        },
    },
);

// Stream chunks as they arrive
for await (const chunk of stream) {
    console.log(chunk);
}
```

The response contains the generated answer, based on your site's content.
{% endtab %}

{% tab title="Python" %}
Make a POST request to `/v1/orgs/{organizationId}/sites/{siteId}/ask`, with your token for authentication and the question, context, and scope in the body:

```python
import json
import requests

ORGANIZATION_ID = "<your organization id>"
SITE_ID = "<your site id>"
API_TOKEN = "<your gitbook api token>"

response = requests.post(
    f"https://api.gitbook.com/v1/orgs/{ORGANIZATION_ID}/sites/{SITE_ID}/ask",
    headers={
        "Authorization": f"Bearer {API_TOKEN}",
        "Content-Type": "application/json"
    },
    json={
        "question": "How do I get started?",
        "scope": {"mode": "default"}
    },
    stream=True
)

# Get the last response before "done"
final = None
for line in response.iter_lines():
    if line:
        line = line.decode('utf-8')
        if line.startswith('data: ') and line[6:] != 'done':
            final = json.loads(line[6:])

print(final)
```

This returns the Ask API's generated answer, based on your site's content.
{% endtab %}
{% endtabs %}

GitBook's API has many endpoints for interacting with GitBook in different ways. After sending your first request, head to the [API Reference](../reference/api-reference.md) to explore what else is available.
