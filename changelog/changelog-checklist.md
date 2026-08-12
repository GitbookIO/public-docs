---
hidden: true
noIndex: true
---

# Changelog checklist

## Changelog classification checklist

Use this checklist for every merged PR since the last changelog entry.

### Step 1 — Extract the inputs

* [ ] PR title
* [ ] Release note text
* [ ] Release note tag: Feature / Fix / Chore
* [ ] PR labels (if any)
* [ ] Linked Linear issue(s) (if any)
* [ ] Relevant Slack #changelog explainer post(s) (if any)

### Step 2 — Public-facing or internal-only?

#### Include if it affects users directly

* [ ] Published docs UX (navigation, mobile, TOC, AI Assistant, theming)
* [ ] Editing UX (change requests, comments, permissions, merge rules)
* [ ] Search UX (in-app search, published search)
* [ ] Customization settings users can access
* [ ] API blocks / API reference features
* [ ] Reliability/performance issues users would notice
* [ ] Permission issues that impact workflows

#### Exclude if it’s primarily internal

* [ ] Backend refactor with no visible change
* [ ] Infra migration
* [ ] Logging/metrics changes
* [ ] Dependency bumps
* [ ] Internal tooling
* [ ] Minor chores with no user-visible effect

**If unclear:** exclude and flag for review.

### Step 3 — Choose a changelog section

#### Featured changes (top `##` narratives)

Use Featured if:

* [ ] Net-new capability
* [ ] Major UX change on published docs
* [ ] Big customization addition
* [ ] High-impact change affecting many users
* [ ] Benefits from screenshots/video and a narrative

#### Improvements (bullets)

Use Improvements if:

* [ ] Refinement of an existing feature
* [ ] Workflow or discoverability tweak
* [ ] Consistency or usability improvement
* [ ] Noticeable, but not a “headline” change

#### Fixed (bullets)

Use Fixed if:

* [ ] Bug fix a user could encounter
* [ ] Reliability/performance issue users would notice
* [ ] UI bug or interaction bug

Write as: “Fixed an issue where X would happen when Y.”

### Step 4 — Add “why” context (when helpful)

Add context if it explains:

* [ ] The pain users experienced
* [ ] The workflow this enables
* [ ] Why the change matters now
* [ ] What users should do next

Sources, in order:

* [ ] Linear issue description
* [ ] PR description / release note
* [ ] Slack explainer post

### Step 5 — Drafting rules

#### Featured narratives

* [ ] Use a clear `##` heading in sentence case
* [ ] Add media if available (embed or figure)
* [ ] Write 2–6 short paragraphs
* [ ] Link to docs when relevant
* [ ] Bold UI names with exact capitalization

#### Improvements and Fixed

* [ ] Bulleted list
* [ ] One idea per bullet
* [ ] Nested bullet only when needed
* [ ] No internal implementation details

### Step 6 — Quality check

* [ ] No internal-only items included
* [ ] No duplicate bullets
* [ ] Titles are specific, not vague
* [ ] Fixes describe the bug in user terms
* [ ] Writing is skimmable and concise
* [ ] Formatting matches the changelog template

### Step 7 — Review notes for humans

In the changelog PR description, include:

* [ ] PRs excluded as internal-only (with links)
* [ ] PRs excluded due to ambiguity (with links)
* [ ] Items that might deserve Featured treatment
* [ ] Any missing context the author should confirm
