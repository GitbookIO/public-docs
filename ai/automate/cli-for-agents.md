---
description: When to move an agent workflow from conversational MCP to deterministic CLI steps.
---

# CLI for agents

The GitBook CLI (`@gitbook/cli`) wraps the GitBook API as a set of terminal commands. Where GitBook MCP is built for conversational, back-and-forth agent sessions, the CLI is a better fit once a workflow becomes repeatable and scriptable — a CI step, a scheduled job, or an agent that already works comfortably in a terminal.

{% hint style="info" %}
This page covers *when and why* to reach for the CLI in agent and automation workflows. For the full command reference, see Developers → CLI → CLI reference.
{% endhint %}

### Human and agentic workflows

The CLI serves two kinds of use:

* **Human-driven** — you type commands to look things up, script one-off tasks, or manage integrations by hand, with output formatted for readability in an interactive shell.
* **Agentic** — an AI coding agent runs the CLI on your behalf as part of a larger task. Machine-readable output (`--json`) and a predictable command structure make it easy for an agent to call commands, parse results, and chain them together.

{% hint style="info" %}
Want an agent to create and edit content through a purpose-built protocol instead of shelling out to commands? See [GitBook MCP](../gitbook-mcp/overview.md). The CLI is the better fit for scriptable commands, integration development, or an agent that already works comfortably in a terminal.
{% endhint %}

### Output formats an agent can parse

Every CLI command supports the same output flags — `--json` is the one to reach for when a script or agent needs to parse the result reliably, rather than the human-readable default:

```bash
gitbook organizations list --json | jq '.items[].title'
```

### Driving the CLI from an agent

Because the CLI is scriptable and speaks JSON, an agent can use it as a tool while it works — authenticating, exploring your content, and acting on the results.

{% prompt description="Explore an organization's docs from the terminal." %}
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

Building or publishing an integration is one of the most common scripted, CLI-driven workflows — see Developers → CLI → CLI reference for the full `gitbook integration` command set.
