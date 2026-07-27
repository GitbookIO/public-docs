---
description: Reference for every GitBook CLI command, grouped by content commands and integration commands.
---

# CLI reference

The `gitbook` CLI wraps the GitBook API as a command-line tool. It's used two ways — to create, test, and publish integrations for the GitBook integrations platform, and to call the GitBook API directly to work with your content. Install it with `npm install @gitbook/cli -g` (see [Install the CLI](../getting-started/install-the-cli.md)).

## Authentication commands

Shared by both content and integration commands — see [Authenticating](../getting-started/authentication.md) for the full walkthrough.

### `gitbook login`

Authenticate through your browser using OAuth. Opens GitBook in your default browser, prompts you to authorize the CLI, and stores the resulting token locally. Tokens refresh automatically.

{% hint style="warning" %}
Publishing integrations (`gitbook integration publish` / `unpublish`) isn't available with a browser session — it still requires a personal API token. Use `gitbook auth` for those.
{% endhint %}

### `gitbook auth`

Authenticate with a personal API token, generated from your [GitBook developer settings](https://app.gitbook.com/account/developer). Pass it with `--token=<token>`, or omit the flag to be prompted.

### `gitbook whoami`

Print information about the currently authenticated user.

### `gitbook logout`

Remove the authentication stored for the current environment.

## Content commands

Most of the command tree is generated directly from the GitBook API: each API operation is exposed as a command group, e.g. `gitbook organizations list` or `gitbook spaces get <space>`. Run `gitbook --help` to explore the full tree, or add `--help` to any command (e.g. `gitbook spaces --help`) to see its subcommands and options. Run `gitbook completion --install` to set up shell completion.

### Run your first commands

List the organizations you belong to:

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

### Output formats

Every API command supports the same output flags:

| Flag | Output |
|---|---|
| `--pretty` | Human-readable summaries (default in an interactive terminal) |
| `--json` | JSON — best for scripts and agents |
| `--yaml` | YAML (default when output is piped or redirected) |
| `--full` | Show every field instead of the compact summary |

Pass `--json` explicitly when piping into tools like `jq`:

```bash
gitbook organizations list --json | jq '.items[].title'
```

### Ask your docs a question

Query your content with natural language, streaming the answer as it's generated:

```bash
gitbook organizations ask stream <organizationId> --query "How do I reset my password?"
```

The answer streams to your terminal, followed by its sources and suggested follow-up questions. Press `Ctrl-C` to stop early.

## Integration commands

Commands for building, running, and publishing an integration on the Developers → Custom components platform.

### `gitbook integration new <dir>`

Create and initialize a new integration locally. Prompts for information about the integration.

### `gitbook integration dev <spaceId>`

Create a live connection between your local integration and a space in your organization — updates you make locally are received automatically in that space while the connection runs. See Developers → Custom components → Development guides.

### `gitbook integration publish`

Publish the integration defined in the project's `gitbook-manifest.yaml`. See Developers → Custom components → Publishing and submitting integrations.

### `gitbook integration unpublish <integration-name>`

Unpublish an integration from the platform. Pass the integration's name as an argument.

{% hint style="info" %}
The integration lifecycle commands (`new`, `dev`, `publish`, `unpublish`, `tail`, `check`) are also accepted at the top level (`gitbook publish`, …) as deprecated aliases that print a warning. Prefer the `gitbook integration <verb>` form.
{% endhint %}

## Using the CLI in CI

Use the CLI in a CI environment to publish an integration on every commit. Store a personal API token (from [app.gitbook.com/account/developer](https://app.gitbook.com/account/developer)) in your CI provider's secrets, then authenticate and publish as a build step.

**With GitHub Actions:**

```yaml
jobs:
  publish:
    name: Publish to GitBook
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18.x
      - run: npm ci
      - run: npm install -g @gitbook/cli
      - run: gitbook integration publish .
        env:
            GITBOOK_TOKEN: ${{ secrets.GITBOOK_TOKEN }}
```

## `gitbook help`

View the GitBook CLI commands and information on using them.
