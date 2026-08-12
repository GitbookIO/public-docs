---
description: >-
  Master GitBook’s powerful events aggregation endpoint to create custom
  analytics dashboards, understand user behavior patterns, and make data-driven
  decisions about your documentation strategy.
---

# Track advanced analytics with GitBook's Events Aggregation API

This guide will explain how to extract meaningful analytics data from your GitBook site, understand visitor behavior patterns, create custom analytics dashboards, track marketing campaign effectiveness, and identify content gaps and optimization opportunities.

## About GitBook’s analytics capabilities

GitBook offers several analytics endpoints to understand your documentation usage. The raw events endpoint provides individual visitor interactions, while the visitor segments endpoint handles visitor behavior segmentation. This guide focuses specifically on the events aggregation endpoint, which is the most powerful tool for creating custom analytics dashboards and reports.

### What makes events aggregation special

The aggregation endpoint transforms individual visitor events into meaningful insights. Instead of raw click data, you get organized information about what visitors are searching for, which API endpoints receive the most attention, visitor satisfaction patterns through feedback, and how visitors navigate through your documentation.

Unlike traditional web analytics, this endpoint is specifically designed for documentation sites and captures documentation-specific events that matter most to technical content creators.

## Setting up your analytics workflow

Before you begin, you’ll need a GitBook account with API access, your organization ID and site ID from your GitBook dashboard URLs, [a GitBook API token](https://gitbook.com/docs/developers/getting-started/setup-guide#create-a-personal-access-token), and your preferred programming language for making API calls. To use Python, you’ll want to [install Pandas](https://pandas.pydata.org/) as well.

Your GitBook URLs contain the IDs you’ll need. Look for this pattern in your dashboard: `https://app.gitbook.com/o/{organizationId}/s/{siteId}`

## Understanding your analytics data

GitBook’s analytics data is organized into dimensions and metrics. Dimensions represent the categorical information about each event, such as content details like URL and page information, visitor characteristics including geographic location and device type, traffic sources through referrer and UTM parameters, and time-based data showing when events occurred.

Metrics are the calculated values based on your data. These include events count for total interactions, visitors count for unique visitors, and sessions count for browsing sessions.

## Event and visitor counts by URL, ranked by total events over last 30 days

Let’s start with a query to identify which pages get the most visitor engagement:

{% tabs %}
{% tab title="Python" %}
```python
import requests
import pandas as pd

# Configuration
API_TOKEN = "your_api_token_here"
ORG_ID = "your_org_id"
SITE_ID = "your_site_id"

# API setup
url = f"https://api.gitbook.com/v1/orgs/{ORG_ID}/sites/{SITE_ID}/insights/events/aggregate"
headers = {
    "Authorization": f"Bearer {API_TOKEN}",
    "Content-Type": "application/json"
}

# Query for top pages
query = {
    "select": [
        {"column": "url"},
        {"column": "eventsCount"},
        {"column": "visitorsCount"}
    ],
    "groupBy": [{"column": "url"}],
    "order": {
        "by": {"column": "eventsCount"},
        "direction": "desc"
    },
    "range": "last30Days",
    "limit": 20
}

response = requests.post(url, headers=headers, json=query)
data = response.json()

# Convert to DataFrame for analysis
def convert_to_dataframe(api_response):
    columns_data = {}
    for item in api_response['columns']:
        columns_data[item['column']] = item['values']
    return pd.DataFrame(columns_data)

df = convert_to_dataframe(data)
print(df.head())
```
{% endtab %}

{% tab title="TypeScript" %}
```typescript
import { GitBookAPI, type SiteInsightsQueryEventsAggregation } from '@gitbook/api';

// Configuration
const API_TOKEN = "your_api_token_here";
const ORG_ID = "your_org_id";
const SITE_ID = "your_site_id";

// Initialize GitBook client
const client = new GitBookAPI({
    authToken: API_TOKEN
});

// Query for top pages - using proper types from SDK
const query: SiteInsightsQueryEventsAggregation = {
    select: [
        { column: "url" },
        { column: "eventsCount" },
        { column: "visitorsCount" }
    ],
    groupBy: [{ column: "url" }],
    order: {
        by: { column: "eventsCount" },
        direction: "desc"
    },
    range: "last30Days",
    limit: 20
};

// Convert API response to array of objects for easier use
function convertToRows(apiResponse: { columns: Array<{ column: string; values: any[] }> }) {
    const rows: Record<string, any>[] = [];
    const columnCount = apiResponse.columns[0]?.values.length || 0;
    
    for (let i = 0; i < columnCount; i++) {
        const row: Record<string, any> = {};
        apiResponse.columns.forEach((column) => {
            row[column.column] = column.values[i];
        });
        rows.push(row);
    }
    return rows;
}

// Make request using GitBook client's aggregateSiteEvents method
async function getTopPages() {
    try {
        const response = await client.orgs.aggregateSiteEvents(ORG_ID, SITE_ID, query);
        
        // The SDK returns the data directly in response.data
        const rows = convertToRows(response.data);
        console.log('Top pages by engagement:', rows.slice(0, 5));
        return rows;
    } catch (error) {
        console.error('Error:', error);
        throw error;
    }
}

// Execute the function
getTopPages();
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X POST "https://api.gitbook.com/v1/orgs/your_org_id/sites/your_site_id/insights/events/aggregate" \
  -H "Authorization: Bearer your_api_token_here" \
  -H "Content-Type: application/json" \
  -d '{
    "select": [
      {"column": "url"},
      {"column": "eventsCount"},
      {"column": "visitorsCount"}
    ],
    "groupBy": [{"column": "url"}],
    "order": {
      "by": {"column": "eventsCount"},
      "direction": "desc"
    },
    "range": "last30Days",
    "limit": 20
  }'
```
{% endtab %}

{% tab title="Untitled" %}
```typescript
import { GitBookAPI } from '@gitbook/api';

const client = new GitBookAPI({
  authToken: <your_access_token>
});

client.aggregateSiteEvents({
  organizationId: x,
  siteId: x,
  data: {
    select:
    where: 
  },
  params: x
})
```
{% endtab %}
{% endtabs %}

This query shows you your most engaged-with pages over the last 30 days.

## Essential analytics queries for documentation

### Event and visitor counts by event type over last 30 days

To understand how visitors interact with your documentation, group events by their type to see the distribution of page views, searches, link clicks, and other activities.

{% hint style="info" %}
The following examples use Python as it’s the most practical choice for data analysis and creating analytics dashboards. All queries will work the same in TypeScript/cURL using the same JSON structure shown in the first example above.
{% endhint %}

```python
behavior_query = {
    "select": [
        {"column": "eventType"},
        {"column": "eventsCount"},
        {"column": "visitorsCount"}
    ],
    "groupBy": [{"column": "eventType"}],
    "order": {"by": {"column": "eventsCount"}, "direction": "desc"},
    "range": "last30Days"
}

response = requests.post(url, headers=headers, json=behavior_query)
behavior_df = convert_to_dataframe(response.json())
print(behavior_df)
```

### Visitor counts by country and device type over last 30 days

Analyze where your visitors come from and what devices they use to make informed decisions about localization, mobile optimization, and regional content strategies.

```python
audience_query = {
    "select": [
        {"column": "visitorGeoCountry"},
        {"column": "visitorDevice"},
        {"column": "visitorsCount"}
    ],
    "groupBy": [{"column": "visitorGeoCountry"}, {"column": "visitorDevice"}],
    "order": {"by": {"column": "visitorsCount"}, "direction": "desc"},
    "range": "last30Days",
    "limit": 50
}

response = requests.post(url, headers=headers, json=audience_query)
audience_df = convert_to_dataframe(response.json())
print(audience_df.head(10))
```

### Search query text and frequency from search events over last 30 days

Analyze what visitors are searching for to identify content gaps and optimization opportunities. Search queries that return few results or low engagement often indicate missing documentation.

```python
search_query = {
    "select": [
        {"column": "eventSearchQuery"},
        {"column": "eventsCount"}
    ],
    "where": [
        {
            "column": "eventType",
            "operator": "in", 
            "values": ["search_type_query"]
        }
    ],
    "groupBy": [{"column": "eventSearchQuery"}],
    "order": {"by": {"column": "eventsCount"}, "direction": "desc"},
    "range": "last30Days",
    "limit": 30
}

response = requests.post(url, headers=headers, json=search_query)
search_df = convert_to_dataframe(response.json())
print("Top search queries:")
print(search_df)
```

### Visitor counts by UTM source, medium, and campaign over last 30 days

Track how marketing campaigns with UTM parameters perform by analyzing which sources, mediums, and campaigns drive the most engaged visitors to your documentation.

```python
campaign_query = {
    "select": [
        {"column": "utmSource"},
        {"column": "utmMedium"},
        {"column": "utmCampaign"},
        {"column": "visitorsCount"}
    ],
    "groupBy": [
        {"column": "utmSource"}, 
        {"column": "utmMedium"}, 
        {"column": "utmCampaign"}
    ],
    "order": {"by": {"column": "visitorsCount"}, "direction": "desc"},
    "range": "last30Days"
}

response = requests.post(url, headers=headers, json=campaign_query)
campaign_df = convert_to_dataframe(response.json())
print("Campaign performance:")
print(campaign_df)
```

### Working with time ranges

All analytics queries require a time range. You can use preset ranges for common time periods or create custom date ranges for precise analysis.

The available preset ranges are `lastYear` for comprehensive historical data, `last3Months` for quarterly analysis, `last30Days` for monthly reporting, `last7Days` for weekly insights, and `last24Hours` for daily monitoring.

For precise control over time periods, use custom date ranges:

```python
# Custom date range example
custom_range_query = {
    "select": [{"column": "eventsCount"}, {"column": "visitorsCount"}],
    "range": {
        "from": "2024-01-01T00:00:00Z",
        "to": "2024-12-31T23:59:59Z"
    }
}
```

### AI question text with timestamps, URLs, and frequency over last 30 days

One of the most valuable insights you can gather is seeing exactly what questions visitors ask your AI assistant. This reveals content gaps, common confusion points, and topics that need better coverage.

```python
# Get AI questions with their text, organized by date
ai_questions_query = {
    "select": [
        {"column": "datetime"},
        {"column": "eventSearchQuery"},  # The actual question text
        {"column": "url"},               # Which page it was asked on
        {"column": "eventsCount"}        # How many times
    ],
    "where": [
        {
            "column": "eventType",
            "operator": "in",
            "values": ["ask_question"]
        }
    ],
    "groupBy": [
        {"column": "datetime"},
        {"column": "eventSearchQuery"},
        {"column": "url"}
    ],
    "order": {
        "by": {"column": "datetime"},
        "direction": "desc"
    },
    "range": "last30Days",
    "limit": 100
}

response = requests.post(url, headers=headers, json=ai_questions_query)
questions_df = convert_to_dataframe(response.json())

# Show most common questions
question_totals = questions_df.groupby('eventSearchQuery')['eventsCount'].sum().sort_values(ascending=False)

print("Most common AI questions:")
for i, (question, count) in enumerate(question_totals.head(10).items(), 1):
    print(f"{i:2d}. [{count:3d}x] {question}")

# Daily question volume
daily_totals = questions_df.groupby('datetime')['eventsCount'].sum().sort_index(ascending=False)
print(f"\nDaily question volume:")
for date, total in daily_totals.head(7).items():
    unique_questions = len(questions_df[questions_df['datetime'] == date]['eventSearchQuery'].unique())
    print(f"{date} | {total:3d} total questions | {unique_questions:2d} unique questions")
```

### AI response rating counts (positive/negative) from rating events over last 30 days

Query the API to retrieve satisfaction ratings (thumbs up/down) that visitors give to AI responses, helping you understand response quality.

```python
# Track AI response satisfaction ratings
satisfaction_query = {
    "select": [
        {"column": "eventAskResponseRating"},
        {"column": "eventsCount"}
    ],
    "where": [
        {
            "column": "eventType",
            "operator": "in",
            "values": ["ask_rate_response"]
        }
    ],
    "groupBy": [{"column": "eventAskResponseRating"}],
    "order": {"by": {"column": "eventsCount"}, "direction": "desc"},
    "range": "last30Days"
}

response = requests.post(url, headers=headers, json=satisfaction_query)
satisfaction_df = convert_to_dataframe(response.json())

# Calculate satisfaction metrics
positive_ratings = satisfaction_df[satisfaction_df['eventAskResponseRating'] == 1]['eventsCount'].sum()
negative_ratings = satisfaction_df[satisfaction_df['eventAskResponseRating'] == -1]['eventsCount'].sum()
total_ratings = positive_ratings + negative_ratings

if total_ratings > 0:
    satisfaction_rate = (positive_ratings / total_ratings) * 100
    print(f"AI Satisfaction Rate: {satisfaction_rate:.1f}%")
    print(f"Positive ratings: {positive_ratings}")
    print(f"Negative ratings: {negative_ratings}")
```

### Event and visitor counts by URL for AI question events over last 30 days

See which pages generate the most AI questions to understand visitor needs and identify areas that may need clearer documentation.

```python
# Analyze AI questions by page
questions_query = {
    "select": [
        {"column": "url"},
        {"column": "eventsCount"},
        {"column": "visitorsCount"}
    ],
    "where": [
        {
            "column": "eventType",
            "operator": "in",
            "values": ["ask_question"]
        }
    ],
    "groupBy": [{"column": "url"}],
    "order": {"by": {"column": "eventsCount"}, "direction": "desc"},
    "range": "last30Days",
    "limit": 20
}

response = requests.post(url, headers=headers, json=questions_query)
questions_df = convert_to_dataframe(response.json())

print("Pages with most AI questions:")
print(questions_df.head(10))

# Calculate AI adoption rate
total_questions = questions_df['eventsCount'].sum()
unique_visitors = questions_df['visitorsCount'].sum()
print(f"\nTotal AI questions: {total_questions}")
print(f"Users asking questions: {unique_visitors}")
```

## Advanced analytics patterns

### Combined AI question and rating data with satisfaction rates by URL over last 30 days

For deeper analysis, combine AI satisfaction data with page-level insights to identify specific content areas that need improvement and understand how AI usage varies across your documentation.

```python
# Advanced AI analytics combining questions, ratings, and page insights
advanced_ai_query = {
    "select": [
        {"column": "url"},
        {"column": "eventType"},
        {"column": "eventAskResponseRating"},
        {"column": "eventsCount"},
        {"column": "visitorsCount"}
    ],
    "where": [
        {
            "column": "eventType",
            "operator": "in",
            "values": ["ask_question", "ask_rate_response"]
        }
    ],
    "groupBy": [{"column": "url"}, {"column": "eventType"}, {"column": "eventAskResponseRating"}],
    "order": {"by": {"column": "eventsCount"}, "direction": "desc"},
    "range": "last30Days",
    "limit": 100
}

response = requests.post(url, headers=headers, json=advanced_ai_query)
ai_df = convert_to_dataframe(response.json())

# Create comprehensive page-level AI insights
page_insights = {}
for url in ai_df['url'].unique():
    page_data = ai_df[ai_df['url'] == url]
    
    questions = page_data[page_data['eventType'] == 'ask_question']['eventsCount'].sum()
    ratings_data = page_data[page_data['eventType'] == 'ask_rate_response']
    
    # Calculate satisfaction rate for this page
    if not ratings_data.empty:
        positive = ratings_data[ratings_data['eventAskResponseRating'] == 1]['eventsCount'].sum()
        negative = ratings_data[ratings_data['eventAskResponseRating'] == -1]['eventsCount'].sum()
        total_ratings = positive + negative
        satisfaction = (positive / total_ratings * 100) if total_ratings > 0 else None
    else:
        satisfaction = None
        total_ratings = 0
    
    page_insights[url] = {
        'questions': questions,
        'total_ratings': total_ratings,
        'satisfaction_rate': satisfaction,
        'needs_attention': satisfaction < 60 if satisfaction is not None else False
    }

# Display insights
print("AI Performance by Page:")
sorted_pages = sorted(page_insights.items(), key=lambda x: x[1]['questions'], reverse=True)

for url, data in sorted_pages[:10]:
    status = "⚠️  Needs attention" if data['needs_attention'] else "✅ Good"
    sat_text = f"{data['satisfaction_rate']:.1f}%" if data['satisfaction_rate'] else "No ratings"
    print(f"{url[:50]}... | Questions: {data['questions']} | Satisfaction: {sat_text} | {status}")
```

## Building analytics strategies

### Essential metrics framework

To advance your understanding of your documentation metrics, you’ll want to build a comprehensive strategy around four key areas: content effectiveness through engagement rates, user experience via navigation flows, AI adoption through assistant usage, and business impact with conversion metrics.

### Automated monitoring principles

You can set up threshold-based alerts for behavioral changes and establish regular reporting cycles. Focus on identifying opportunities alongside problems by tracking positive trends and measuring content update effectiveness through before-and-after analysis.

## Best practices for documentation analytics

* Try to limit the number of results for your queries where possible to avoid hitting rate limits. For instance, if you only need data about certain event types, use `"where"` in your query to pre-filter the number of rows returned.
* Prioritize actionable metrics over vanity numbers. Events per visitor beats raw page views, search success rates show if users find what they need, and content completion indicates real engagement.
* Create a consistent rhythm: daily monitoring for issues, weekly tracking for trends, monthly analysis for strategic decisions, and quarterly reviews for overall effectiveness.
* Use analytics to drive content decisions. Popular topics need expansion, search queries reveal gaps, engagement data guides optimization, and geographic insights inform localization.

## Troubleshooting common issues

**API performance**: Choose appropriate time ranges, implement caching, and batch queries when possible.

**Data interpretation**: Remember that groupBy parameters affect calculations. Event counts include all interactions, so filter by specific types for focused analysis.

## Taking your analytics further

**Integration**: You can connect to your existing BI tools, set up automated alerts, and build custom visualizations for stakeholders.

**Advanced techniques**: Explore cohort analysis for retention, funnel analysis for workflows, and A/B testing for content improvements.

## Getting help

Check out the [GitBook API documentation](https://gitbook.com/docs/developers/gitbook-api/api-reference/docs-sites/site-insights#post-orgs-organizationid-sites-siteid-insights-events-aggregate) for technical details, [engage the community](https://github.com/orgs/GitbookIO/discussions) for best practices, or [contact support](https://www.gitbook.com/contact) for account-specific assistance.
