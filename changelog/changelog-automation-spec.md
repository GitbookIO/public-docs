---
hidden: true
noIndex: true
---

# Changelog automation spec

This repo contains GitBook’s public changelog, synced to GitBook and written in Markdown.

A changelog update is generated from merged pull requests since the previous changelog entry. Each PR includes a release note tagged as one of:

* Feature
* Fix
* Chore

Not all PRs should be included in the public changelog.

### Output format

Each changelog entry must follow this structure:

* Wrapped in `{% update date="YYYY-MM-DD" %} … {% endupdate %}`
* One or more featured items at the top (optional)
* Then `### Improvements`
* Then `### Fixed`

#### Template

```md
{% update date="YYYY-MM-DD" %}

## <Featured change title>

<Optional media: {% embed url="…" %} or <figure>…</figure>>

<2–6 short paragraphs describing the user-facing change, what it enables, and where to find it.>

### Improvements

* ...

### Fixed

* ...

{% endupdate %}
```

### Section definitions

#### Featured changes (top `##` sections)

Use a featured item when the change:

* introduces a new capability
* significantly improves published docs UX
* adds meaningful new customization options
* impacts a wide set of users
* benefits from screenshots, a video, or a short narrative explanation

Featured items must be written as short, user-facing narratives.

#### Improvements

Improvements are smaller changes that:

* refine an existing feature
* improve discoverability, workflow, or usability
* make the product more consistent
* do not need a full narrative section

Improvements are written as bullet points.

#### Fixed

Fixed items are user-facing bug fixes:

* issues users could reasonably encounter
* performance or reliability problems users notice
* UI or interaction bugs

Fixed items must describe the bug in user terms:\
“Fixed an issue where X would happen when Y.”

### Inclusion rules

#### Include in the public changelog

Include changes that affect:

* published docs UX (navigation, mobile, search, AI Assistant, layout, theming)
* editing and collaboration UX (change requests, permissions, comments, merge rules)
* API blocks and API reference features
* customization settings that users can access
* reliability/performance issues that users notice
* permission issues that impact user workflows

#### Exclude from the public changelog

Exclude changes that are primarily:

* backend refactors
* infra migrations
* internal tooling changes
* logging/metrics changes
* dependency bumps
* minor chores with no user-visible impact

If a change is ambiguous, exclude it and flag it for review in the changelog PR description.

### Enriching with context (“why”)

Whenever it improves clarity, enrich changelog entries using:

1. Linear issue context (problem statement, user pain, expected outcome)
2. PR description and release note
3. Slack #changelog explainer posts (screenshots, phrasing, deeper explanation)

Only include “why” when it helps users understand:

* what pain is solved
* what workflow is enabled
* what they should do next (where to click, what setting to change)

### Style guide

* Sentence case for headings
* Use smart quotes
* Use contractions
* Use em dashes with spaces — like this
* Use en dashes for ranges
* Bold UI element names with exact capitalization (e.g. **Customization**, **Sharing**, **Agent**)
* Prefer user outcomes over implementation details
* Include doc links where they help users learn or act
* Keep featured narratives concise and skimmable

### Safety and workflow expectations

* The generator must only propose changes via a pull request.
* Never commit directly to the default branch.
* If uncertain, prefer excluding items and flagging them for human review.
