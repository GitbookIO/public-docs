---
description: Explore the full reference guide for GitBook’s CLI commands
---

# CLI reference

### `gitbook login`

Sign in through your browser. The CLI opens GitBook, waits for the authorization to redirect back to a local callback, and stores the resulting session.

The browser must run on the same machine as the CLI, so this doesn't work over SSH, in containers, in CI, or in sandboxed AI agents. Use `gitbook auth` in those environments. Browser sign-in also can't publish or unpublish integrations.

### `gitbook auth`

Authenticate the CLI with a GitBook Developer API token. You can generate a personal developer token in your [GitBook Developer settings](https://app.gitbook.com/account/developer). This works in CI, over SSH, and in AI agent sandboxes, and is required to publish integrations.

The token can also be provided using the command line argument `--token=<token>`; If none is provided, it'll be prompted.

### `gitbook integration new <dir>`

Create and initialize a new integration locally. The program will prompt for information about the integration.

### `gitbook integration dev`

Create a live connection from your integration to your GitBook editor. Updates made locally while the connection is running will automatically be received in the editor.

See the [development section](../development/) to learn more.

### `gitbook integration publish`

Publish the integration defined in the `gitbook-manifest.yaml` file. See the [GitBook Manifest reference](../configurations.md) documentation to learn more.

See the [publishing section](../publishing.md) to learn more about publishing your integration to GitBook.

### `gitbook integration unpublish <integration-name>`

Unpublish your integration from the GitBook integration platform. Pass the name of the integration as an argument to the command.

{% hint style="info" %}
`gitbook integration` (singular) holds the commands for building and publishing your own integration. `gitbook integrations` (plural) holds the commands generated from the GitBook API for managing integrations, such as listing installations. Run `gitbook integration --help` or `gitbook integrations --help` to see each group.
{% endhint %}

### `gitbook whoami`

Print information about the currently authenticated user.

### `gitbook help`

View the GitBook CLI commands and information on using them.
