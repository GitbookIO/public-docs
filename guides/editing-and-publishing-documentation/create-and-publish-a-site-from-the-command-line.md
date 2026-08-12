---
description: >-
  Create a space, write your first page and publish a docs site — all from your
  terminal with the GitBook CLI
---

# Create and publish your first site from the command line

The [GitBook CLI](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/gitbook-cli) wraps the GitBook API as a set of commands, so most of what you’d click through in the app you can do from your terminal instead. It’s scriptable, it speaks JSON, and it runs happily inside an AI coding agent.

You’ll need a GitBook organization ([sign up](https://gitbook.com/join) if you don’t have one yet), Node v18 or later, and [the GitBook CLI installed](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/gitbook-cli). Signing in is the first step below.

From there, this guide starts with an organization that has nothing in it and finishes with a docs site live at its own URL.

### Let an agent do it

Eight commands stand between you and a published site, and an agent can run all of them. Paste this into Claude Code, Cursor, Codex, or whichever agent you work in:

{% prompt description="Create and publish a new docs site from the terminal." openInAIProviders="true" %}
```markdown
Using the `gitbook` CLI, create and publish a new GitBook docs site for me.

1. Run `gitbook whoami` to check I'm signed in. If I'm not, tell me to run `gitbook login` and stop there.
2. Run `gitbook organizations list` and show me what you find. Ask me which organization to use — don't guess, even if there's only one.
3. Ask me what the site should be called and what the first page should say. Show me the title, visibility and page outline you're planning, then wait for my yes before you create anything.
4. Create the space. Add the first page through a change request: create it, apply the content with `--changes`, then merge it. Use `##` and below for headings within the page.
5. Create the site with the space attached, publish it, then read the live URL back to me from `urls.published`.

Use `--json` so you can parse the output, show me each command before you run it, and stop if any of them fail.
```
{% endprompt %}

It’ll ask which organization to use before it creates anything. Keep that step if you edit the prompt — a new site is visible to everyone in the organization as soon as it exists.

Building something larger, with several spaces, Git Sync or your own branding? GitBook publishes a set of [agent skills](https://github.com/GitbookIO/gitbook-skills) for that:

```bash
npx skills add GitbookIO/gitbook-skills
```

`configure-site` covers site creation end to end, and `write-docs` handles the pages themselves.

### Or do it yourself

Here’s the same workflow, one command at a time. It’s worth walking through yourself at least once: you’ll see what the agent is doing on your behalf, and you’ll know where to look if something comes back wrong.

{% stepper %}
{% step %}
### Sign in

```bash
gitbook login
```

This opens GitBook in your browser and asks you to authorize the CLI. Sessions refresh automatically, so you only do this once per machine.

{% hint style="info" %}
**Note:** Browser sign-in covers everything in this guide, publishing included. You may spot a note in the CLI docs about publishing needing a personal API token — that one’s about publishing **integrations** to the marketplace, not about publishing a docs site.
{% endhint %}
{% endstep %}

{% step %}
### Find your organization

Nearly every command below starts with an organization ID, so grab yours first.

```bash
gitbook organizations list
```

You’ll get one line per organization, with its ID first. Copy the ID of the one you want to build in.

{% hint style="info" %}
**Tip:** You’ll see ten organization IDs at a time. If yours isn’t in the list, the footer gives you the exact flag to fetch the next page — something like `--page lEaOPV8dWgqNDmmGHpKM`.
{% endhint %}
{% endstep %}

{% step %}
### Create a space

Spaces and sites do different jobs. A [space](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/content-structure/space) is where your content lives — its pages, and the change requests you use to edit them. A site is what your readers visit: it takes one or more spaces and publishes them at a URL. So the space comes first, and you point a site at it later.

```bash
gitbook spaces create <organizationId> --body '{"title":"Product docs"}'
```

Copy the `id` from the output — that’s your space ID, and you’ll need it for every step that follows. Space titles are capped at 50 characters.

{% hint style="info" %}
**Tip:** Most commands take typed flags like `--title`. `spaces create` is the exception — it takes the whole request body as JSON, so keep the quoting exactly as it is above.
{% endhint %}
{% endstep %}

{% step %}
### Add your first page

A new space starts with a single empty page. Content goes in through a [change request](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/collaborate/change-requests) — the same flow you’d use in the editor, where you propose changes and then merge them. Nothing lands on your primary content until you merge, so you can review or preview it first.

Open a change request:

```bash
gitbook spaces change-requests create <spaceId> --subject "Add homepage"
```

Copy the change request ID from the output, then add a page to it:

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

`--changes` is required: it’s the list of operations you want applied, and there’s no shorthand command for adding a page. `insert_page` is one of four — `update_page`, `delete_page` and `revert_page` go in the same list — so this one command covers edits and deletions too.

When the changes look good, merge the change request into your primary content:

```bash
gitbook spaces change-requests merge <spaceId> <changeRequestId>
```

{% hint style="info" %}
**Tip:** A page’s title is stored separately from its body, and GitBook reads a single `#` heading at the top of your markdown as that title rather than as content. So repeating the title the way we have above is harmless — you won’t get it twice. Inside the page, use `##` and below: if your markdown has more than one `#` heading, they all become content.
{% endhint %}
{% endstep %}

{% step %}
### Create and publish the site

To publish your content, you need a site. A site takes at least one space as its content source, and you can attach the space you just made as you create it — paste in the same space ID you copied earlier:

```bash
gitbook organizations sites create <organizationId> --title "Product docs" --visibility public --spaces '["<spaceId>"]'
```

Copy the site ID, then publish:

```bash
gitbook organizations sites publish <organizationId> <siteId> --full
```

`--full` shows every field instead of a summary. Look for `published` under `urls` — that’s your live site. Open it, and the page you wrote is there.

{% hint style="warning" %}
**Note:** If your organization isn’t on a paid plan, publishing can hand back a checkout object rather than a site, and there’ll be no published URL. New sites default to the Ultimate plan for most organizations, so add `--type basic` to `sites create` if you’d rather start on the free tier.
{% endhint %}
{% endstep %}
{% endstepper %}

### Where to go next

You’ve got a published docs site with your first page on it. Everything you’d do next runs through the same command tree: `organizations sites customization update` changes your theme and layout, `organizations sites site-spaces add` brings in more spaces as your docs grow, and `organizations openapi create` uploads an OpenAPI spec if you want a generated API reference alongside your guides. As before, `gitbook --help` works at any level and lists what sits underneath it.

None of that is terminal-only, though — the same site is sitting in GitBook waiting for you, so you can keep writing in the editor, invite your team to review change requests, and set up a custom domain whenever you’re ready.

***

### Related reading

[**→ Read the GitBook CLI documentation**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/gitbook-cli)

[**→ Connect an agent with GitBook MCP**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/gitbook-mcp)

[**→ Work with the GitBook API**](/broken/spaces/NkEGS7hzeqa35sMXQZ4X/pages/oPMEQQq3E6uxpyIxGzqN)

[**→ Keep your docs in sync with Git Sync**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync)
