---
description: >-
  Track creators, reviewers, and contributors with GitBook’s API to understand
  how your team collaborates
---

# Analyze change request contributors with GitBook’s API

GitBook’s API makes it possible to track change request creators, reviewers, and contributors across all your spaces.

Understanding who contributes to your documentation helps you recognize documentation champions, balance review workloads, and identify opportunities to grow your documentation culture.&#x20;

This guide walks through using GitBook’s API to build a complete picture of how your team collaborates on documentation. You’ll learn to fetch change requests, and analyze who’s creating, reviewing, and contributing to your documentation changes.

### Before you begin

To follow along with this guide, you’ll need [a GitBook account](https://app.gitbook.com/join) with API access and a personal access token. You can [create a token](https://gitbook.com/docs/developers/getting-started/setup-guide#create-a-personal-access-token) from your GitBook account settings.&#x20;

You’ll also need your organization ID, which you can find in your GitBook dashboard URL — it’s the part that looks like `https://app.gitbook.com/o/{organizationId}/...`

On the technical side, this guide uses Python with the `requests` and `pandas` libraries. If you’re using a different language, the concepts translate directly — you’ll just need to adapt the HTTP requests and data processing to your preferred tools.

### Setting up your environment

First, set up your configuration with the necessary credentials:

{% code title="contribution_analytics.py" %}
```python

import requests
import pandas as pd
from datetime import datetime, timedelta, timezone

# Configuration
API_TOKEN = "your_api_token_here"
ORG_ID = "your_org_id"
SPACE_ID = "your_space_id"
DAYS_BACK = 30  # Number of days to analyze
```
{% endcode %}

### Fetch change requests for a space

Once you have your spaces, you can retrieve change requests for any of them.&#x20;

Change requests are proposed documentation changes that go through your team’s review process before being merged into the published documentation.&#x20;

The API lets you filter by status, so you can focus on merged changes if you want to analyze what actually made it into your docs, or look at open changes to understand what’s currently in progress.

{% code title="contribution_analytics.py" %}
```python
def get_change_requests(space_id, api_token, status="merged", limit=100):
    """Get all change requests for a space with given status."""
    response = requests.get(
        f"https://api.gitbook.com/v1/spaces/{space_id}/change-requests",
        headers={
            "Authorization": f"Bearer {api_token}",
            "Accept": "*/*"
        },
        params={"status": status, "limit": limit}
    )
    response.raise_for_status()
    return response.json()

# Use a specific space or the first one in your list
change_requests_data = get_change_requests(SPACE_ID, API_TOKEN)

print(f"Found {len(change_requests_data['items'])} change requests")
```
{% endcode %}

The `status` parameter gives you flexibility in what you analyze. Set it to `merged` to focus on changes that made it into production, `open` to see what’s currently being worked on, or `closed` to examine changes that were abandoned.&#x20;

You can see [all of the possible parameters here](analyze-change-request-contributors-with-gitbooks-api.md#fetch-change-requests-for-a-space).

### Process and filter change requests by date

The raw API response contains a lot of information. Converting it to a pandas DataFrame makes it easier to work with.&#x20;

This function extracts the key fields you’ll need for analysis and filters the results to focus on recent activity.&#x20;

{% code title="contribution_analytics.py" %}
```python
def process_change_requests(cr_data, days_back=30):
    """Convert change request data to DataFrame and filter by date."""
    records = []
    for item in cr_data['items']:
        record = {
            'id': item['id'],
            'number': item['number'],
            'status': item['status'],
            'subject': item['subject'],
            'createdAt': item['createdAt'],
            'updatedAt': item['updatedAt'],
            'creator_name': item['createdBy']['displayName'],
            'creator_email': item['createdBy']['email'],
            'comments': item['comments'],
            'outdated': item['outdated']
        }
        records.append(record)
    
    df = pd.DataFrame(records)
    df['createdAt'] = pd.to_datetime(df['createdAt'])
    df['updatedAt'] = pd.to_datetime(df['updatedAt'])
    
    # Filter to recent change requests
    cutoff_date = datetime.now(timezone.utc) - timedelta(days=days_back)
    recent_df = df[df['createdAt'] >= cutoff_date]
    
    return recent_df

recent_crs = process_change_requests(change_requests_data, DAYS_BACK)
print(f"Found {len(recent_crs)} change requests in the last {DAYS_BACK} days")
```
{% endcode %}

### Analyze change request creators

Now that you have your change requests in a DataFrame, you can get some stats on who creates them.&#x20;

{% code title="contribution_analytics.py" %}
```python
# Count change requests by creator
creator_counts = recent_crs['creator_name'].value_counts()

print("Top change request creators:")
print(creator_counts.head(10))
```
{% endcode %}

This tells you which team members are most active in proposing documentation updates and helps you identify your documentation champions.

### Get change request contributors

Contributors are slightly different from creators — they include anyone who has made edits within a change request, even if they weren’t the person who originally opened it.&#x20;

{% code title="contribution_analytics.py" %}
```python
def get_cr_contributors(space_id, change_request_id, api_token):
    """Get all contributors to a change request."""
    response = requests.get(
        f"https://api.gitbook.com/v1/spaces/{space_id}/change-requests/{change_request_id}/contributors",
        headers={
            "Authorization": f"Bearer {api_token}",
            "Accept": "*/*"
        },
    )
    response.raise_for_status()
    return response.json()

# Get contributors for all recent change requests
all_contributors = []

for cr_id in recent_crs['id']:
    try:
        contributors_data = get_cr_contributors(SPACE_ID, cr_id, API_TOKEN)
        for contributor in contributors_data.get('items', []):
            contributor_name = contributor.get('user').get('displayName')
            contributor_email = contributor.get('user').get('email')
            all_contributors.append({
                'cr_id': cr_id,
                'contributor_name': contributor_name,
                'contributor_email': contributor_email
            })
    except Exception as e:
        print(f"Warning: Could not get contributors for CR {cr_id}")

# Analyze contributor activity
if all_contributors:
    contributors_df = pd.DataFrame(all_contributors)
    print(f"\nFound {len(all_contributors)} contributor records")
    print("\nTop contributors:")
    print(contributors_df['contributor_name'].value_counts().head(10))
```
{% endcode %}

This data reveals collaborative patterns and shows you when multiple people work together on documentation changes.

### Get change request commenters

Comments on change requests provide valuable context about the review process and reveal where discussion happens most. The comments endpoint shows you all the feedback, questions, and suggestions that reviewers and contributors leave on each change request.

{% code title="contribution_analytics.py" %}
```python
def get_cr_comments(space_id, change_request_id, api_token):
    """Get all comments for a change request."""
    response = requests.get(
        f"https://api.gitbook.com/v1/spaces/{space_id}/change-requests/{change_request_id}/comments",
        headers={
            "Authorization": f"Bearer {api_token}",
            "Accept": "*/*"
        },
    )
    response.raise_for_status()
    return response.json()

# Get comments for all recent change requests
all_comments = []

for cr_id in recent_crs['id']:
    try:
        comments_data = get_cr_comments(SPACE_ID, cr_id, API_TOKEN)
        print(comments_data)
        for comment in comments_data.get('items', []):
            comment_id = comment.get('id')  or ''
            commenter_name = comment.get('postedBy').get('displayName')  or ''
            commenter_email = comment.get('postedBy').get('email') or '',
            posted_at = comment.get('postedAt')  or ''
            body = comment.get('body') or ''
            
            all_comments.append({
                'cr_id': cr_id,
                'comment_id': comment_id,
                'commenter_name': commenter_name,
                'posted_at': posted_at,
                'commenter_email': commenter_email,
                'body': body
            })
    except Exception as e:
        print(f"Warning: Could not get comments for CR {cr_id}")

# Analyze comment activity
if all_comments:
    comments_df = pd.DataFrame(all_comments)
    print(f"\nFound {len(all_comments)} comments")
    print("\nMost active commenters:")
    print(comments_df['commenter_name'].value_counts().head(10))
    
    # Find change requests with most discussion
    cr_comment_counts = comments_df.groupby('cr_id').size().sort_values(ascending=False)
    print(f"\nAverage comments per change request: {len(comments_df) / len(recent_crs):.1f}")
```
{% endcode %}

### Building a complete contributor analysis

Combine all the data to create comprehensive insights about contributors to your documentation:

{% code title="contribution_analytics.py" %}
```python
# Summary statistics
print("=" * 60)
print("CONTRIBUTOR ANALYSIS SUMMARY")
print("=" * 60)
print(f"Time period: Last {DAYS_BACK} days")
print(f"Total change requests: {len(recent_crs)}")
print(f"Unique creators: {recent_crs['creator_name'].nunique()}")

if not contributors_df.empty:
    print(f"Total contributor records: {len(contributors_df)}")
    print(f"Unique contributors: {contributors_df['contributor_name'].nunique()}")

if not comments_df.empty:
    print(f"Total comments: {len(comments_df)}")
    print(f"Unique commenters: {comments_df['commenter_name'].nunique()}")

# Calculate engagement metrics
avg_contributors_per_cr = len(contributors_df) / len(recent_crs) if not contributors_df.empty else 0
avg_comments_per_cr = len(comments_df) / len(recent_crs) if not comments_df.empty else 0

print(f"\nAverage contributors per change request: {avg_contributors_per_cr:.1f}")
print(f"Average comments per change request: {avg_comments_per_cr:.1f}")

# Find most discussed change requests
if not comments_df.empty:
    most_discussed = comments_df.groupby('cr_id').size().sort_values(ascending=False).head(5)
    print("\nMost discussed change requests:")
    for cr_id, comment_count in most_discussed.items():
        cr_info = recent_crs[recent_crs['id'] == cr_id].iloc[0]
        print(f"  CR #{cr_info['number']}: {cr_info['subject']}")
        print(f"    Comments: {comment_count}")
        print(f"    Creator: {cr_info['creator_name']}")
        print()
```
{% endcode %}

### Use cases for contributor analytics

Once you have contributor data flowing, you can use it to make meaningful improvements to your documentation culture.&#x20;

The most common use case is recognizing documentation champions — those team members who consistently contribute to documentation deserve recognition, and having the data makes it easy to identify them objectively.&#x20;

Tracking unique contributors over time can also you a concrete measure of whether your documentation culture is growing or staying stagnant.&#x20;

The data also helps surface knowledge silos. When you see areas where only one person contributes, that’s a signal that you may want to bring in other people to share knowledge.&#x20;

### Best practices

Contributor analytics work best when you run them regularly.&#x20;

Monthly analysis helps you spot trends in contribution patterns and team engagement before they become problems.&#x20;

Rather than analyzing just one space at a time, consider looping through multiple spaces to understand contribution patterns across your entire documentation ecosystem.

Finally, watch for signals that might indicate training needs. If you’re seeing low contributor counts despite having a sizable team, that might suggest people need better onboarding on your documentation workflow or more clarity about how to contribute.

### Getting help

For technical details about the API endpoints used in this guide, see the [GitBook API documentation](https://gitbook.com/docs/developers/gitbook-api/api-reference).

Have questions or want to share your own analytics approaches? [Join the community discussion](https://github.com/orgs/GitbookIO/discussions).

Need help with your specific use case? [Contact GitBook’s support team](https://www.gitbook.com/contact) — they’ll be happy to help.
