---
description: >-
  Set up GitBook from a coding agent or AI assistant and publish a docs site,
  either new docs or docs moved from another tool.
hidden: true
---

# Set up GitBook

This page is for AI agents helping someone set up GitBook. Your goal is a published docs site at a public URL, with either new docs or docs moved from another tool.

{% hint style="info" %}
**For people**

Start with the [Quickstart](https://gitbook.com/docs/getting-started/quickstart). To hand the setup to your coding agent, paste this prompt into it: `Set up GitBook for me by following https://gitbook.com/docs/setup.md`.
{% endhint %}

## Check whether you already have GitBook tools

If GitBook MCP tools are already in this session, for example from the Claude, ChatGPT, or Cursor plugin, confirm they work with a read-only call: `get_usage_guide` with the topic `onboarding`. If it answers, ask the question in [Step 1](#step-1-ask-what-theyre-doing), then go to [Step 4](#step-4-resume-and-publish). You don't need to connect anything, hand off, or save a plan file.

If there are no GitBook tools, find your row:

| Who's reading                                                        | What you can do                                     | Where to go next                                             |
| -------------------------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| A coding agent that can run commands and edit files                  | Connect GitBook, bring the person in once, publish  | [How GitBook setup works](#how-gitbook-setup-works)          |
| A hosted chat assistant, such as Claude.ai or ChatGPT                | Only the person can add the GitBook plugin          | [Relay the plugin setup](#relay-the-plugin-setup)            |
| A person                                                             | Set up in the app, or hand the setup to your agent  | [Quickstart](https://gitbook.com/docs/getting-started/quickstart) |

### Relay the plugin setup

Send the person these steps as a numbered list:

> GitBook connects to me as a plugin. I can't add it myself, but you can in a few clicks:
>
> 1. If you don't have a GitBook account, [create one](https://app.gitbook.com/join) and finish signup until you see your organization.
> 2. Install the GitBook plugin: [Claude](https://claude.ai/directory/connectors/gitbook-mcp) or [ChatGPT](https://chatgpt.com/apps/gitbook/asdk_app_6a576f075ec4819196c203b7049542be).
> 3. Approve the GitBook sign-in that opens.
> 4. Start a new conversation so the GitBook tools load.
>
> Tell me when it's done, and I'll help you plan and publish your docs.

Then stop. The rest of this page is for agents that can run commands and edit files. In the new conversation, start again from [Check whether you already have GitBook tools](#check-whether-you-already-have-gitbook-tools).

## How GitBook setup works

GitBook needs an account. There's no way to publish a site and hand it over later, so the person signs up or signs in at least once. Plan around that moment: do all your prep first, send one short "your turn" message, then resume.

You have three tools. Pick by situation, not by preference:

| Tool                                                | Use it when                                                                                        | Sign-in                                   |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| [GitBook MCP](docs-as-code/gitbook-mcp.md)          | Default. The client can reload its config, and the person can approve a browser sign-in.           | OAuth in the browser                      |
| [GitBook CLI](docs-as-code/gitbook-cli.md)          | The MCP tools can't load in this session, for example because the client can't restart.             | `gitbook login` in the browser            |
| [GitBook API](https://gitbook.com/docs/developers/gitbook-api/api-reference) | A step neither the MCP nor the CLI covers.                                  | A personal access token                   |

The MCP server is `https://mcp.gitbook.com/mcp`. It supports streamable HTTP only, not `stdio` or `SSE`.

## Keep messages to the person short

Each message says what's done and the one thing they do next, in two or three sentences. Don't relay IDs, tokens, file paths, or command output. Give a link only when they need to open it now.

## Step 1: ask what they're doing

Before you configure anything, ask:

> Are you starting new docs, or moving docs you already have?

* **Starting new.** Ask what the docs are for and who reads them. If there's a codebase here, read it so you can propose real pages.
* **Moving docs.** Ask where they live now: a folder or Git repository, a published website, or another tool such as Confluence or Notion. If they're on this machine, read them and say back what you found so they can confirm.

Draft a short plan: site title, page structure, and how the content gets in (see [Moving existing docs](#moving-existing-docs)). Save it to `gitbook-setup-plan.md` in the working directory, and don't commit it. The restart in Step 3 ends your session, and the plan file is how you pick up again.

## Step 2: connect GitBook MCP

### Ground rules

* **Read before you write.** Config files hold the person's other MCP servers. Read the file, back it up if it exists, add or update only the `gitbook` entry, and confirm the result parses.
* Say which file you're about to change before you change it.
* **If Claude Code's auto mode blocks a command, don't retry it or route around it.** Hand-editing the config is the same action it refused. Tell the person what the command does and let them run it.

Work out which client you're running in. If you can't tell, ask. A config in the wrong place fails silently.

### Claude Code

```bash
claude mcp add --transport http --scope user gitbook https://mcp.gitbook.com/mcp
```

`--scope user` makes GitBook available in every project. Without it, the server only exists in the current directory. Check it registered with `claude mcp get gitbook`. To undo, run `claude mcp remove gitbook --scope user`.

After a restart, the person types `/mcp` and picks GitBook to sign in. That's a slash command, so you can't run it for them.

### Codex

```bash
codex mcp add gitbook --url https://mcp.gitbook.com/mcp
```

The browser sign-in starts after you add it. Check it with `codex mcp get gitbook`, and retry a sign-in with `codex mcp login gitbook`. To undo, run `codex mcp remove gitbook`. The tools load in a new Codex task.

### Cursor

The person can install the [GitBook plugin for Cursor](https://cursor.com/marketplace/gitbook). To configure it yourself, add this to `~/.cursor/mcp.json`, or to `.cursor/mcp.json` for this project only:

```json
{
  "mcpServers": {
    "gitbook": {
      "url": "https://mcp.gitbook.com/mcp"
    }
  }
}
```

Cursor prompts for the sign-in. Leave auth fields out.

### VS Code

Add this to `.vscode/mcp.json` in the workspace:

```json
{
  "servers": {
    "gitbook": {
      "type": "http",
      "url": "https://mcp.gitbook.com/mcp"
    }
  }
}
```

The person starts it from the MCP view and signs in.

### Other clients

Add a remote streamable HTTP server at `https://mcp.gitbook.com/mcp`. With OAuth, the client handles the sign-in and you add no auth fields. If the client can't do OAuth, send a personal access token as `Authorization: Bearer <token>`. The person creates it in their [developer settings](https://app.gitbook.com/account/developer).

### Verify before the restart

Re-read the file you changed, or run the client's `get` command, and confirm the `gitbook` entry is there and the file parses. The restart ends your session, so check now.

### Optional: add GitBook skills

You don't need skills to publish, but they help the first pages come out right. The `write-docs` skill teaches GitBook-flavored Markdown, such as hints, tabs, and steppers, so pages render correctly in GitBook. Tell the person what you're installing, then run:

```bash
npx -y skills add GitbookIO/gitbook-skills -y
```

Without both `-y` flags, the installer waits for input. If Claude Code's auto mode blocks the command, hand it to the person instead. Don't commit the installed skill files unless they ask.

The [GitBook skills repository](https://github.com/GitbookIO/gitbook-skills) includes `write-docs`, `configure-site`, `write-openapi`, `cr-create`, `cr-review`, and `build-integration`, for pages, site setup, OpenAPI references, change requests, and integrations.

## Step 3: hand off once

Send one message that covers everything the person needs to do:

> I've added GitBook to [client] and saved our plan. Your turn:
>
> 1. If you don't have a GitBook account, [create one](https://app.gitbook.com/join) and finish signup until you see your organization.
> 2. Restart [client], then sign in to GitBook when it asks. In Claude Code, type `/mcp` and pick GitBook.
> 3. Tell me "done" and I'll pick up from the plan.
>
> To undo this, [how to undo for this client].

If the session can't restart, don't wait. Use [the CLI](#fallback-the-gitbook-cli) instead.

## Step 4: resume and publish

1. Read `gitbook-setup-plan.md`, if you saved one.
2. Call `get_usage_guide` with the topic `onboarding`, and follow it. Use `editing` for adding content.
3. List the person's organizations with `invoke_operation` and `listOrganizationsForAuthenticatedUser`. Ask which one to use, even if there's only one.
4. Call `get_subscription_information`. If the organization isn't on a paid plan, create the site with `type` set to `basic`. Other types can return a checkout instead of a published site.
5. Create the site and add the content, following the plan.
6. Show the person what you're about to publish and wait for a yes. Merging a change request and publishing a site are public and can't be undone.
7. Publish, then go to [Step 5](#step-5-verify-and-report).

### Moving existing docs

Only route content through paths that exist. For Markdown already in a GitHub or GitLab repository, including exports from another docs tool, use [Git Sync](docs-as-code/git-sync/README.md). It's the recommended path for large migrations and supports up to 5,000 pages. Create the site with no spaces and don't apply the template. Git Sync setup isn't available through the MCP, so the person connects it in the GitBook app and picks the direction **GitHub → GitBook**. Warn them that the other direction can overwrite the repository. The [Git Sync migration guide](https://gitbook.com/docs/guides/editing-and-publishing-documentation/import-or-migrate-your-content-to-gitbook-with-git-sync) has the steps. Resume when they confirm the sync finished.

When the person names a source, use this table:

| Source | Route | Who does what |
| --- | --- | --- |
| Mintlify | Docs are Markdown or MDX in a Git repo, so use Git Sync. Mintlify-specific MDX components may need converting to GitBook blocks. The agent can do that in the repo before the person connects Git Sync. | Agent prepares the repo. Person connects Git Sync in the GitBook app. |
| Docusaurus | Docs are Markdown or MDX in a Git repo, so use Git Sync. | Agent prepares the repo. Person connects Git Sync in the GitBook app. |
| ReadMe | If the project already uses [Git Connection](https://docs.readme.com/main/docs/bi-directional-sync), the docs are Markdown or MDX in a Git repo. Use Git Sync. If not, the person can connect Git Connection to an empty repo (ReadMe writes the files), or export Guides as Markdown with [`rdme docs export`](https://github.com/readmeio/rdme/blob/main/documentation/commands/docs.md). Then use Git Sync. If neither export is available, the person uses the Import panel on the published site (20-page cap). | Agent prepares the repo once the Markdown is available. Person enables Git Connection or exports, then connects Git Sync, or uses the Import panel. |
| Confluence, Notion, Google Docs, Word, or other published sites | The person uses the [Import panel](getting-started/import.md) in the GitBook app. It takes up to 20 pages per import. | The person runs the import. |
| A few Markdown files on this machine | Add them as pages in a change request, the same way you'd add new content. | The agent adds the pages. |

Name the human step plainly in your plan, and put it in the Step 3 message so it happens in the same hand-off.

## Step 5: verify and report

Read the published URL from the publish response, open it, and confirm the content is live. Then tell the person in two or three sentences: what's published, the link, and one suggested next step. Delete `gitbook-setup-plan.md` if they don't want it.

Suggested first tasks:

```
Add a getting started page to my GitBook site based on this repo's README
Open a change request in GitBook with release notes for this week's changes
```

## Fallback: the GitBook CLI

Use the CLI when the MCP tools can't load in this session, for example because the client can't restart. The CLI needs Node v18 or later:

```bash
npm install @gitbook/cli -g
```

**Sign in with `gitbook login`.** It opens GitBook in the browser, and the sign-in returns to a localhost callback on the machine running the CLI. On the person's own machine, run it in the background and tell them to approve the sign-in in the browser. In a cloud or remote session, the browser can't reach that callback, so the person runs `gitbook login` in their own terminal.

Confirm with `gitbook whoami`, then run the flow below. Add `--json` to every command so you can parse the output, show each command before you run it, and stop if one fails.

1. List organizations and ask which one to use:

```bash
gitbook organizations list
```

2. Create a space and copy its `id`. The body is JSON, not a `--title` flag, and titles are capped at 50 characters:

```bash
gitbook spaces create <organizationId> --body '{"title":"Product docs"}'
```

3. Add content through a change request, then merge it:

```bash
gitbook spaces change-requests create <spaceId> --subject "Add homepage"
```

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

```bash
gitbook spaces change-requests merge <spaceId> <changeRequestId>
```

A single `#` heading becomes the page title, so use `##` and below inside the page.

4. Create the site with the space attached. Use `--type basic` unless the organization has a paid plan:

```bash
gitbook organizations sites create <organizationId> --type basic --title "Product docs" --visibility public --spaces '["<spaceId>"]'
```

5. Publish and read `urls.published` from the output:

```bash
gitbook organizations sites publish <organizationId> <siteId> --full
```

The [CLI guide](https://gitbook.com/docs/guides/editing-and-publishing-documentation/create-and-publish-a-site-from-the-command-line) has more detail.

## When neither covers a step

Use the [GitBook API](https://gitbook.com/docs/developers/gitbook-api/api-reference) with a personal access token. With the MCP connected, `search`, `describe_operation`, and `invoke_operation` reach most API operations without leaving the session.

## Stuck, or something here is wrong?

* **Ask the docs.** Send a GET request to any GitBook docs page URL ending in `.md`, with `ask` set to your question and `goal` set to what the person wants to achieve. For example: `https://gitbook.com/docs/setup.md?ask=<question>&goal=<goal>`.
* **Report it.** With the MCP connected, call `report_tool_feedback` with what you tried and what happened. Leave tokens and private content out.
