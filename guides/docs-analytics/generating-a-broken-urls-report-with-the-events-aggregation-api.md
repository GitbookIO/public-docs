---
description: >-
  Export broken URL activity from GitBook analytics with curl and jq to build a
  practical monthly report.
---

# Generating a broken URLs report with the Events Aggregation API

Broken URLs appear in [Site analytics](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/analytics/insights).

This guide shows how to export the same signal with the [Events Aggregation API](track-advanced-analytics-with-gitbooks-events-aggregation-api.md).

Use this workflow to build a monthly report from the command line.

### Before you begin

You’ll need:

* Your organization ID
* Your site ID
* A GitBook API token
* `curl`
* `jq`

The GitBook dashboard URL includes the IDs you need: `https://app.gitbook.com/o/{organizationId}/s/{siteId}`

### Endpoint

Send your request to:

```
POST https://api.gitbook.com/v1/orgs/{organizationId}/sites/{siteId}/insights/events/aggregate
```

{% stepper %}
{% step %}
### Set your local variables

Export your IDs and token so you can reuse the commands below:

```bash
export GITBOOK_ORG_ID="your_org_id"
export GITBOOK_SITE_ID="your_site_id"
export GITBOOK_API_TOKEN="your_api_token_here"
```
{% endstep %}

{% step %}
### Query broken URL events for the last 30 days

This request finds events where the requested URL did not resolve to a page.

It includes direct page views and search result opens. It groups results by URL. It sorts by total event count.

```bash
curl -sS \
  -X POST "https://api.gitbook.com/v1/orgs/${GITBOOK_ORG_ID}/sites/${GITBOOK_SITE_ID}/insights/events/aggregate" \
  -H "Authorization: Bearer ${GITBOOK_API_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "select": [
      {"column": "url"},
      {"column": "datetime"},
      {"column": "eventsCount"},
      {"column": "visitorsCount"}
    ],
    "where": [
      {"column": "eventType", "operator": "in", "values": ["page_view", "search_open_result"]},
      {"column": "page", "values": [null]}
    ],
    "groupBy": [{"column": "url"}],
    "order": {
      "by": {"column": "eventsCount"},
      "direction": "desc"
    },
    "range": "last30Days"
  }' > broken-urls.json
```

The API returns a column-oriented response. Each field comes back as an array of values.
{% endstep %}

{% step %}
### Turn the response into a readable table with jq

Use `jq` to reshape the response into rows, rename `datetime` to `last_seen`, and print a table:

```bash
jq -r '
  .columns as $cols
  | ($cols[0].values | length) as $n
  | [range(0; $n) as $i
      | reduce $cols[] as $col ({};
          . + { ($col.column): $col.values[$i] }
        )
      | {
          url,
          last_seen: .datetime,
          events: .eventsCount,
          visitors: .visitorsCount
        }
    ]
  | (["url", "last_seen", "events", "visitors"]),
    (.[] | [.url, .last_seen, (.events | tostring), (.visitors | tostring)])
  | @tsv
' broken-urls.json | column -t -s $'\t'
```

A typical result looks like this:

```
url                                      last_seen             events  visitors
https://docs.example.com/old-guide       2026-06-22T14:18:11Z  82      61
https://docs.example.com/api/v1/auth     2026-06-21T09:44:02Z  37      29
https://docs.example.com/help/legacy     2026-06-18T16:05:47Z  14      11
```
{% endstep %}
{% endstepper %}

### How to read the report

Use the results to prioritize fixes:

* The highest `events` count usually means the highest impact.
* Recent `last_seen` values usually mean the issue is still active.
* Several broken URLs under one path often point to moved, renamed, or unpublished content.

If you want to go deeper on query structure, filters, and other reporting patterns, see [Track advanced analytics with GitBook's Events Aggregation API](track-advanced-analytics-with-gitbooks-events-aggregation-api.md).

### Caveats

Keep these limits in mind:

* The aggregation endpoint returns at most 1,000 rows per request.
* Results only include URLs that visitors actually requested.
* Empty results can mean no broken URL activity, or that the Broken URLs feature isn’t enabled on the site.

### Next step

Run this query once a month. Compare the top results over time.

If the same path cluster keeps returning, add redirects. You can also restore the missing content.
