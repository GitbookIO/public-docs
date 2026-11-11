---
description: Create and publish a docs site from a coding agent using the GitBook CLI.
hidden: true
---

# Setting up GitBook with a coding agent

This page is for coding agents setting up GitBook on behalf of someone. Your goal is a live docs site at a public URL.

Use the [GitBook CLI](../docs-as-code/gitbook-cli.md) as the primary route. The commands below are the full flow. The [CLI guide](https://gitbook.com/docs/guides/editing-and-publishing-documentation/create-and-publish-a-site-from-the-command-line.md) has more detail, including a copyable prompt.

[GitBook MCP](../docs-as-code/gitbook-mcp.md) and [skill.md](https://gitbook.com/docs/skill.md) are optional and described at the end of this page.

## Before you start

You need Node v18 or later. Install the CLI with the following command:

```bash
npm install @gitbook/cli -g
```

The person you’re working with needs a GitBook account. If they don’t have one, they can [create an account](https://app.gitbook.com/join) before signing in.

## Publish a site with the CLI

Use `--json` so you can parse each response. Show each command before you run it, and stop if a command fails. Ask which organization to use — don’t guess, even if there’s only one.

1. Check whether you’re already signed in:

```bash
gitbook whoami
```

2. If you’re not signed in, run the following command:

```bash
gitbook login
```

This is the one step you can’t complete alone. It opens GitBook in the browser and asks the person you’re working with to authorize the CLI. Stop and ask them to open the link, create an account if they need one, and sign in. Once `gitbook whoami` shows an authenticated user, continue.

To skip the browser flow, they can create a personal API token in [developer settings](https://app.gitbook.com/account/developer) and you can run `gitbook auth --token <token>`.

3. List organizations and confirm which one to use:

```bash
gitbook organizations list
```

4. Create a space and copy its `id` from the output:

```bash
gitbook spaces create <organizationId> --body '{"title":"Product docs"}'
```

Space titles are capped at 50 characters. `spaces create` takes the request body as JSON, not a `--title` flag.

5. Open a change request, add a page, then merge it. A new space starts with a single empty page, so content goes in through a change request. Create the change request with the following command:

```bash
gitbook spaces change-requests create <spaceId> --subject "Add homepage"
```

Add a page to the change request:

```bash
gitbook spaces change-requests content update <spaceId> <changeRequestId> --changes '[
  {
    "operation": "insert_page",
    "title": "Welcome",
    "document": {
      "markdown": "# Welcome\n\nThis page was published from the command line.\n"
    }
  }
]'
```

When the changes look good, merge the change request into the primary content:

```bash
gitbook spaces change-requests merge <spaceId> <changeRequestId>
```

Use `##` and below for headings within the page. A single `#` heading is treated as the page title.

6. Create a public site with the space attached, then publish it:

```bash
gitbook organizations sites create <organizationId> --title "Product docs" --visibility public --spaces '["<spaceId>"]'
```

{% hint style="warning" %}
If the organization isn’t on a paid plan, publishing can return a checkout object rather than a site, with no published URL. New sites default to the Ultimate plan for most organizations, so add `--type basic` to `sites create` to start on the free tier.
{% endhint %}

Publish the site and request the full output:

```bash
gitbook organizations sites publish <organizationId> <siteId> --full
```

7. Read `urls.published` from the publish output, open that URL, and confirm the page is live. That’s the result to report back.

## Optional: GitBook MCP and skill.md

If the person you’re working with wants GitBook tools inside the agent session, they can connect [GitBook MCP](../docs-as-code/gitbook-mcp.md) at `https://mcp.gitbook.com/mcp` and give you [skill.md](https://gitbook.com/docs/skill.md).

This path needs them to approve access in the browser. Some clients also need a session reload before the tools become available, so it can block sandboxed or unattended agents. Prefer the CLI unless they ask for MCP.
