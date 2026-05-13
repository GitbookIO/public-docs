# Inputs to gather up front

What to confirm with the user **before** scaffolding a new GitBook site or making state-changing API calls. If anything below is missing, ask once with a focused question rather than guessing.

## Contents

- GitBook PAT (auth)
- Organization confirmation
- Site plan and visibility
- The content seed
- OpenAPI spec (for API reference)
- Branding
- Site structure (sections)
- Git remote preference
- Site shape (single space vs multi-space)

## GitBook PAT

Required for all API calls. The user keeps this in 1Password and we fetch it at the start of each session via the `op` CLI:

```bash
export GITBOOK_TOKEN=$(op read "<secret-reference>")
```

The skill remembers the user's secret reference across sessions via Claude's memory feature. On first use:

1. Check user memories for a line like `User's GitBook PAT 1Password reference: op://...`. If present, use that reference directly.
2. If absent, ask the user once for their `op` secret reference (they can find it via "Copy Secret Reference" in the 1Password UI, or by running `op item get <item-name> --format=json`). After they share it, save it via `memory_user_edits add` so future sessions don't have to ask again.
3. If `op read` fails (not signed in, wrong reference, item moved), surface the exact error and stop. Don't fall back to asking the user to paste the token directly into the conversation — keeping it in `op` is the whole point.

Never write the token to a file, never echo it back in a response, never commit it.

## Organization confirmation

List the user's orgs with `GET /v1/orgs` and **show the list to the user, then ask them to confirm which one is the target by name**. Do this even if they have only one org — confirming once up front is cheap insurance against creating sites in the wrong place. Save the chosen `organizationId` for the rest of the session and refer to the org by its title (not its UUID) when narrating subsequent steps.

## Site plan and visibility

**Default to `type: site` on the Ultimate plan**, public visibility, unless the user explicitly says otherwise. Most real customers want the Ultimate feature set (custom domain, AI Assistant, advanced customization, hidden GitBook trademark, custom fonts, custom logos). The free tier (`type: basic`) is appropriate only for clearly low-stakes use cases like solo open-source side projects.

If you're unsure, ask: *"I'll set this up on the Ultimate plan unless you'd prefer the free tier — should I downgrade?"* — Ultimate features that are silently absent on `basic` (no AI assistant, no custom fonts, no custom domain) are a much bigger user surprise than briefly confirming the plan.

## The content seed

What's the site being built from? Common shapes:

- A folder of existing markdown — the cleanest starting point
- A handful of notes plus a competitor's site as a reference
- Just a description of what they want to document
- An existing site they want to restructure (in which case fetch `GET /v1/orgs/{orgId}/sites/{siteId}/structure` first)
- **A migration** from another docs platform (Mintlify, Docusaurus, ReadTheDocs, GitBook v1) — see `migration-from-other-platforms.md` for the workflow. Migration is its own discipline; don't treat it as a glorified file copy.

## OpenAPI spec for the API reference

If the site has any API reference content, **ask up front whether they have an OpenAPI spec** (or whether one can be generated from their codebase). If yes, the API reference space is one `builtin:openapi` SUMMARY entry plus a one-paragraph overview README per resource — dramatically less work than hand-authored endpoint pages, and never drifts. See `block-ecosystem.md` and `api-cheatsheet.md` for the workflow.

**Don't default to hand-authored endpoint pages** — they're almost always the wrong call.

## Branding

At minimum, primary color (hex). Optionally: logo URLs (light + dark), favicon, font choice (or one of GitBook's defaults), header links, footer text/links, theme preset (`clean`, `muted`, `bold`, `gradient`). For Ultimate sites, also consider AI-assistant starter prompts (3-5 short questions visitors are likely to ask).

Full schema: `branding-schema.md`. Worked examples: `customization-recipes.md`.

## Site structure (sections)

Sections, not site-spaces. If the site has more than one space, plan the **section list** with the user explicitly: each section has a title, a Font Awesome icon name, and a description. Section icons and descriptions are first-class navigation furniture — visitors see them — and gathering them up front saves a PATCH-per-section later.

Example:

```json
[
  {"title": "Guides",        "icon": "book-open",            "description": "Concepts and tutorials"},
  {"title": "API Reference", "icon": "code",                 "description": "REST API and SDKs"},
  {"title": "Changelog",     "icon": "clock-rotate-left",    "description": "Updates and release notes"}
]
```

Full structure-design heuristics: `site-structure-design.md`.

## Git remote preference

GitHub, GitLab, or local-only. Check whether `gh` or `glab` are installed *before* asking. If neither tool is available, **say so explicitly** and offer two paths:

1. Commit locally and put the "create the remote and push" step at the top of the user's handoff.
2. Ask the user to install the tool.

Don't quietly default to local-only without telling them — they'll have a repo with no remote and no instructions.

## Site shape

Single space or multi-space. Multi-space sites use **sections** to group spaces in the navigation; this is the right choice when content has clearly distinct audiences (e.g. user docs + API reference + changelog). Use site-spaces directly only for translation variants — see `api-cheatsheet.md`.
