---
description: >-
  Work with your GitBook content from the command line — sign in, query the API,
  and drive docs workflows from scripts or AI coding agents.
---

# GitBook CLI

The GitBook CLI (`@gitbook/cli`) is a command-line tool for working with your GitBook content and organizations directly from your terminal.

It wraps the GitBook API as a set of commands, so you can list organizations, inspect spaces and pages, ask questions against your docs, and build and publish integrations — all without leaving the shell.

## Human and agentic workflows

The CLI is built for two kinds of use:

* **Human-driven** — you type commands in your terminal to look things up, script one-off tasks, or manage integrations by hand. Output is formatted for readability in an interactive shell.
* **Agentic coding** — an AI coding agent (Claude Code, Codex, Cursor, and similar) runs the CLI on your behalf as part of a larger task. Machine-readable output (`--json`) and predictable command structure make it easy for an agent to call commands, parse results, and chain them together.

{% hint style="info" %}
If you want an AI agent to create and edit content through GitBook’s API using a purpose-built protocol, see [GitBook MCP](gitbook-mcp.md). The CLI is a good fit when you want scriptable commands, integration development, or an agent that already works comfortably in a terminal.
{% endhint %}

## Install

The GitBook CLI requires Node v18 or later. Install it globally from npm:

```bash
npm install @gitbook/cli -g
```

This installs the `gitbook` command. Check it's working:

```bash
gitbook --version
```

## Authenticate

Sign in once and the CLI stores your credentials locally, refreshing them as needed.

{% tabs %}
{% tab title="Browser (OAuth)" %}
The quickest way to sign in is through your browser:

```bash
gitbook login
```

This opens GitBook in your browser, asks you to authorize the CLI, and stores the resulting token locally. Sessions are refreshed automatically.

This is the recommended path for everyday use.
{% endtab %}

{% tab title="Personal API token" %}
To skip the browser flow — for CI, scripts, or publishing integrations — authenticate with a personal API token. Create one at [app.gitbook.com/account/developer](https://app.gitbook.com/account/developer), then run:

```bash
gitbook auth --token <token>
```

If you omit `--token`, the CLI prompts you for it.
{% endtab %}
{% endtabs %}

Confirm who you're signed in as at any time:

```bash
gitbook whoami
```

To sign out, run `gitbook logout`.

{% hint style="warning" %}
Publishing integrations (`gitbook integration publish` / `unpublish`) requires a personal API token — the browser (OAuth) session can't perform those operations. Run `gitbook auth --token <token>` for publishing workflows. The two credentials can coexist, so you can use browser sign-in for everyday commands and a token for publishing.
{% endhint %}

## Run your first commands

Most commands are generated from the GitBook API and grouped by resource — `organizations`, `spaces`, `collections`, and so on. Start by listing the organizations you belong to:

```bash
gitbook organizations list
```

Grab an organization ID from that output, then list its spaces:

```bash
gitbook spaces list --organization <organizationId>
```

Fetch the details of a single space:

```bash
gitbook spaces get <spaceId>
```

List the pages in a space:

```bash
gitbook spaces content pages list <spaceId>
```

{% hint style="info" %}
Path parameters like `<spaceId>` can be passed as a positional argument or as a flag — `gitbook spaces get <spaceId>` and `gitbook spaces get --spaceId <spaceId>` are equivalent.
{% endhint %}

Run `gitbook --help` to browse the full command tree, or add `--help` to any command (for example `gitbook spaces --help`) to see its subcommands and options.

## Output formats

Every API command supports the same output flags:

| Flag | Output |
|---|---|
| `--pretty` | Human-readable summaries (default in an interactive terminal) |
| `--json` | JSON — best for scripts and agents |
| `--yaml` | YAML |
| `--full` | Show every field instead of the compact summary |

If you don't pass a flag, the CLI picks a sensible default: pretty output in an interactive terminal, and YAML when the output is piped or redirected. Pass `--json` explicitly when you're piping into tools like `jq`:

```bash
gitbook organizations list --json | jq '.[].title'
```

## Ask your docs a question

The CLI can query your content with natural language and stream the answer back as it's generated:

```bash
gitbook organizations ask stream <organizationId> --query "How do I reset my password?"
```

The answer streams to your terminal, followed by its sources and suggested follow-up questions. Press `Ctrl-C` to stop early and keep whatever streamed so far.

## Drive the CLI from an AI coding agent

Because the CLI is scriptable and speaks JSON, an AI coding agent can use it as a tool while it works. Point your agent at the commands above and let it authenticate, explore your content, and act on the results.

{% prompt description="Explore an organization’s docs from the terminal." %}
```markdown
Using the `gitbook` CLI, help me get oriented in my GitBook content.

1. Run `gitbook whoami` to confirm I'm signed in. If not, tell me to run `gitbook login`.
2. List my organizations with `gitbook organizations list --json` and show me the names and IDs.
3. Ask me which organization to explore, then list its spaces.
4. Summarize what you find — how many spaces, and what each one appears to cover based on its title.

Use `--json` for every command so you can parse the output reliably, and show me the exact commands you run.
```
{% endprompt %}

{% prompt description="Answer a question using my docs and cite sources." %}
```markdown
Using the `gitbook` CLI, answer a question from my documentation.

1. Confirm I'm signed in with `gitbook whoami`.
2. List my organizations and confirm which one to search.
3. Run `gitbook organizations ask stream <organizationId> --query "<my question>"` and relay the answer.
4. Include the sources the CLI returns so I can verify the answer against the original pages.
```
{% endprompt %}

## Build integrations

Beyond querying content, the CLI is the primary tool for developing [GitBook integrations](https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/integrations/quickstart). Scaffold a new project with:

```bash
gitbook integration new
```

Then use `gitbook integration dev` to run it locally and `gitbook integration publish` to ship it. See the integrations documentation for the full development workflow.
