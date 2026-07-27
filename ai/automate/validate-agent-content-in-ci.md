---
description: Validate agent-written content against your docs standards in CI before merging.
---

# Validate agent content in CI

Agent-written content should get the same scrutiny as any other change before it lands — always review and test it, whether the agent worked through GitBook Agent, an MCP-connected assistant, or a coding agent using GitBook Skills.

### What to check

The most common ways agent-generated content goes wrong:

* Unclosed custom blocks
* Invalid YAML in frontmatter
* Broken variable references
* Links that don't match your actual page structure
* Custom blocks that don't render as expected in GitBook

Concretely, that means: verify custom blocks render correctly, check that internal links resolve, confirm frontmatter is valid YAML, and test that variables reference the correct scope (page vs. section).

### Building this into CI

If your docs are Git Sync'd, you already have a natural point to catch these before they merge — a CI step on the pull request, same as you'd lint application code. A few practical building blocks already covered elsewhere in these docs:

* Run a YAML linter over changed Markdown files' frontmatter, so malformed frontmatter fails the build instead of silently breaking Git Sync.
* Use the GitBook CLI's `--json` output (see [CLI for agents](cli-for-agents.md)) to script checks against your content programmatically, rather than relying on manual review alone.
* Use a link checker over your repository's Markdown files to catch relative links that don't resolve.
* For a human-in-the-loop layer on top of automated checks, request a [GitBook Agent review](../gitbook-skills/overview.md) on the change request itself — it can flag style guide violations and factual inconsistencies that a syntax-level CI check won't catch.

None of these replace reading the diff yourself — treat them as a first pass that catches mechanical errors before a human review looks at content quality.
