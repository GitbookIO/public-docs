---
description: >-
  This guide will help you set up a directory sync for provisioning users and
  teams using the GitBook API.
---

# Guide: Directory Sync using the GitBook API

SCIM/Directory sync is not currently publicly available in GitBook. If your organization is struggling to manually manage its members and teams in GitBook, we recommend using [the GitBook API](https://developer.gitbook.com/api/resources/organizations/members) to programmatically add/remove members and teams as your directory changes as most identity providers offer ways to hook into these events.

{% hint style="info" %}
Directory sync allows you to automatically provision/de-provision users and teams from your company directory into your GitBook organization. In GitBook it can only be achieved by using our API outlined in the guide below.&#x20;
{% endhint %}

## 1. Getting Started

First of all, you'll need to be set up and accustomed to working with [the GitBook API](https://developer.gitbook.com/getting-started/setup-guide).

## 2. Setting up your environment

First, let's understand from a high-level how user provisioning works:

<img src="../../.gitbook/assets/file.excalidraw.svg" alt="A high-level overview of how user provisioning works" class="gitbook-drawing">

The step in purple will change depending on your Identity Provider (IdP). Most modern directories offer workflows to hook into events like users adding/leaving your organization, but you might have to build this piece yourself.

### IdPs that support automation out of the box

* Okta supports this through [Okta Workflows](https://www.okta.com/uk/platform/workflows-new/). Their documentation features [an example](https://www.okta.com/uk/demo/workflows-template-make-api-requests-with-the-http-request-card/) of using Okta Workflows to send an HTTP request when an event happens in your directory.

### Your API Key

You'll need to make sure you've generated a valid API key and that you're an adminstrator of the target GitBook organization. For now, API keys are generated per user (so if you leave your GitBook organization you'll need another admin to use their key) - though [we are looking at](https://github.com/GitbookIO/community/discussions/30) organization API keys!

## 3. Building the Workflows

Let's build the key workflows you'll need:

### Provision a new user

When a new user joins your organization, you need to provision them in GitBook.

To do this, we'll use [the invites endpoint](https://developer.gitbook.com/gitbook-api/resources/organizations/members).

```powershell
curl --location 'https://api.gitbook.com/v1/orgs/$YOUR_ORG_KEY/invites' \
--header 'Authorization: Bearer $YOUR_GITBOOK_API_KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "emails": [
        "newuser@yourorg.com"
    ],
    "role": "read",
    "sso": true
}'
```

Make sure you've included `sso` in the body so that the user is created as a proper SSO user, and the appropriate `role` for the user.

If you're batching users together, this endpoint accepts a list of emails.

#### Storing the response

The API will tell you the ID of this newly created user:

```json
{
    "users": [
        "PERerEOAQ6QWXj1flmrlVzl3XJ22"
    ],
    "invited": 0
}
```

If you can, try to save this user ID alongside the user in your directory. It'll help when we run future operations.

### Deprovision/remove a user

When a user leaves your organization, you need to remove them from GitBook. You'll need the GitBook ID of the user who's leaving, which ideally would be saved alongside the user in your directory.

{% hint style="info" %}
If you can't save the user ID alongside your directory user, please get in touch with our support team.
{% endhint %}

We'll then use the remove member endpoint to remove the user:

```powershell
curl --location --request DELETE 'https://api.gitbook.com/v1/orgs/$YOUR_ORG_ID/members/$USER_ID' \
--header 'Authorization: Bearer $YOUR_GITBOOK_API_KEY'
```

### Add/remove a user to/from a team

When group memberships change in your organization, you'll want to replicate these changes in GitBook. We have [a single API endpoint for this](https://developer.gitbook.com/gitbook-api/resources/organizations/teams), where team members can be added/removed in one call.

```powershell
curl --location --request PUT 'https://api.gitbook.com/v1/orgs/$YOUR_ORG_ID/teams/$TEAM_ID/members' \
--header 'Authorization: Bearer $YOUR_GITBOOK_API_KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "add": [
        "new_team_member@yourorg.com"
    ],
    "remove": [
        "old_team_member@yourorg.com"
    ]
}'
```

## Idempotency

All of the above operations are idempotent - you can run them multiple times and put them behind retry logic.

## Usage Limits

The GitBook API has some usage limits to prevent malicious users from abusing the system. If you're on our enterprise plan, you won't face these limits. However, if you're on one of our other plans and you're running into rate-limiting errors with the API please [get in touch](mailto:sales@gitbook.com) so we can remove these limits for you.

{% hint style="info" %}
We're always trying to improve our API to enable more complex workflows tailored to your organization. If you have feedback for us about ways the API could be improved, [please let us know via our community](https://github.com/GitbookIO/community/discussions)!
{% endhint %}

If you have further questions, please [get in touch](mailto:sales@gitbook.com).
