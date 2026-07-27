# Docs Restructure — Working Document

Branch: `docs-restructure`
Status: **Phase 1a + 1b(ai) + 1c(changelog) + 1d(api/cli/custom-components) complete — `documentation/`, `ai/`, `changelog/`, `api/`, `cli/`, and `custom-components/` migrated. One page (`ai/gitbook-mcp/mcp-tools-reference.md`) intentionally left open pending a real MCP tool list. GitBook MCP is now connected (see "Live source access" below) — used it to pull `changelog/` directly from the live `GitBook` org. `api/`, `cli/`, and `custom-components/` were instead migrated from the local checkout at `~/Desktop/Development/integrations/docs` (not the live site), each expanded well beyond its original thin stub set to hold the real source content — mirroring the same judgment call made earlier for `documentation/learn/api-documentation/`. Remaining: `education/`, `policies/`.**
Last updated: 2026-07-27

## Goal

Merge GitBook's other doc sections (API reference, CLI reference, Custom
components, Education, Changelog, Policies) into this repo alongside our
existing "Documentation" section, under one Git-synced monorepo driven by
`docs.yaml`. Content from this branch's prior structure gets migrated into
the new structure. Almost every URL will move, so redirects have to be
solved before cutover.

Target structure lives at `/Users/addisonschultz/Desktop/Development/docs`
(a separate, already-Git-synced GitBook repo used to plan the new tree). Its
pages are placeholders — each one currently contains only a "Stub for tree
test" note with a `Purpose`, `Canonical home of`, and `Cross-links` block
describing what content should eventually live there. That repo is the
source of truth for the *shape* of the new docs; this repo (`public-docs`)
is where the real, final content will actually live once migrated.

## What's in this repo right now

- `docs.yaml` + `ai/`, `api/`, `cli/`, `custom-components/`, `documentation/`,
  `education/`, `changelog/`, `policies/` — copied from the target repo.
  `ai/`, `api/`, `cli/`, `custom-components/`, `documentation/`, and
  `changelog/` now have real migrated content (see Phases below);
  `education/` and `policies/` are still **stubs**, not real content.
- `legacy-content/` — the entire previous state of this repo (everything
  that used to be at the root: `account-management/`, `ai-and-search/`,
  `api-references/`, `collaboration/`, `creating-content/`, `docs-site/`,
  `getting-started/`, `gitbook-agent/`, `help/`, `integrations/`,
  `publishing-documentation/`, `resources/`, `site-access/`, `README.md`,
  `SUMMARY.md`, the old `.gitbook.yaml`, and `.gitbook/` assets/includes).
  Kept as-is purely for copy/paste reference while migrating content. **This
  folder must be deleted before go-live** — it's not part of the new site.
- `legacy-content/_reference/live-urls-snapshot-2026-07-24.md` — a snapshot
  of every live URL currently published at gitbook.com/docs (pulled from
  `https://gitbook.com/docs/llms.txt`, 719 URLs across *all* sections, not
  just the one this repo used to own). This is a point-in-time snapshot —
  re-pull before finalizing redirects in case pages changed in the meantime.

## New site structure (from `docs.yaml`)

| Section | Path | Space dir | Notes |
|---|---|---|---|
| Developers ▸ API | `api` | `./api` | GitBook's own developer API reference |
| Developers ▸ CLI | `cli` | `./cli` | GitBook CLI reference |
| Developers ▸ Custom components | `custom-components` | `./custom-components` | Build integrations/ContentKit |
| Documentation (default) | `documentation` | `./documentation` | The canonical core — concepts, how-tos, reference |
| Build with AI | `ai` | `./ai` | Agent-driven authoring (Claude/Cursor/MCP clients) |
| Education | `education` | `./education` | Workflow guides & best practices |
| Changelog | `changelog` | `./changelog` | Releases |
| Policies | `policies` | `./policies` | Hidden section |

## Where new-section content will come from

Only two things exist in this repo's history: the **Documentation** section
(previously the entirety of `public-docs`) and a partial overlap with **Build
with AI** (`getting-started/ai-documentation/*`). Everything else is coming
from other GitBook spaces that currently live outside this repo.

| New section | Source available locally? | Notes |
|---|---|---|
| `documentation/` | ✅ `legacy-content/` (most folders) | Bulk of the migration work |
| `ai/` | ⚠️ Partial — `legacy-content/getting-started/ai-documentation/` | Rest (Skills, MCP tools reference, CLI-for-agents, Extend) likely needs net-new content or content from elsewhere |
| `api/` | ✅ `~/Desktop/Development/integrations/docs/gitbook-api/` (separate local checkout, not `legacy-content/`) | Migrated; expanded 5→9 pages |
| `cli/` | ✅ `~/Desktop/Development/integrations/docs/integrations/reference/` (same local checkout) | Migrated |
| `custom-components/` | ✅ `~/Desktop/Development/integrations/docs/integrations/` (same local checkout) | Migrated; expanded 9→14 pages |
| `education/` | ❌ Not in this repo | Net new or sourced elsewhere |
| `changelog/` | ✅ Pulled live via GitBook MCP | Direct copy from the live `Public Changelog` space |
| `policies/` | ❌ Not in this repo | Candidate space found via MCP (`GitBook Site Policy`, `-LBUnokgAHp7SX9tJUrr`), not yet migrated |

**Open question:** where does `education/` currently live (which GitBook
space/repo)? `policies/` has a known candidate space but hasn't been
migrated yet — confirm with the user before starting either.

## Section-level mapping: old → new (provisional)

First-pass, folder-level only — page-level mapping happens during Phase 1
per section, using each stub page's `Canonical home of` note as the source
of truth for exactly what goes where.

| Old (`legacy-content/...`) | New (provisional) |
|---|---|
| `account-management/` | `documentation/account-and-billing/` |
| `ai-and-search/` | `documentation/learn/gitbook-ai/assistant/`, `documentation/learn/gitbook-ai/readers-ai/`, `documentation/learn/gitbook-ai/ai-search.md` |
| `api-references/` | `documentation/learn/api-documentation/` (this is about the OpenAPI *feature*, not GitBook's own API — that's the new `api/` section) |
| `collaboration/` | `documentation/learn/collaboration/` |
| `creating-content/` | `documentation/learn/creating-content/` |
| `docs-site/` | `documentation/learn/customization/`, `documentation/learn/publishing/`, `documentation/learn/embed/`, `documentation/learn/analytics/` |
| `getting-started/` | `documentation/getting-started/`, `documentation/learn/git-sync/`; `ai-documentation/*` → `ai/` |
| `gitbook-agent/` | `documentation/learn/gitbook-ai/agent/` |
| `help/` | `documentation/resources/get-support.md` |
| `integrations/` | `documentation/learn/custom-components/` (install/manage, done in Phase 1a). The developer-facing `custom-components/` section was migrated separately in Phase 1d, from a different local checkout (`~/Desktop/Development/integrations/docs`), not from this `legacy-content/integrations/` folder. |
| `publishing-documentation/` | `documentation/learn/publishing/`, `documentation/learn/access/authenticated-access/custom-backend.md`, `documentation/learn/gitbook-ai/readers-ai/mcp-server-for-published-docs.md` |
| `resources/` | `documentation/resources/` |
| `site-access/` | `documentation/learn/access/` |

## Phases

- [x] **Phase 0 — Scaffold structure.** Copy new folder/`docs.yaml` structure
      in, archive old content to `legacy-content/`, snapshot live URLs, write
      this doc.
- [x] **Phase 1a — `documentation/` content migration.** All 14 subsections
      migrated from `legacy-content/` and committed: account-and-billing,
      getting-started, custom-components, git-sync, collaboration,
      customization, api-documentation, resources, embed, access,
      publishing, analytics, gitbook-ai, creating-content. See
      `CONTENT-MAP.md` for the full page-level mapping and the decisions
      made along the way (splits, merges, cut content, new pages added for
      gaps found during mapping).
- [x] **Phase 1b(ai) — `ai/` content migration.** All 19 pages migrated —
      turned out to have much more real legacy source
      (`legacy-content/getting-started/ai-documentation/{gitbook-mcp,
      ai-coding-assistants-and-skillmd,gitbook-cli}.md`) than the "mostly
      net-new" note in this doc originally suggested. One page,
      `ai/gitbook-mcp/mcp-tools-reference.md`, is intentionally left as an
      open stub — no source anywhere documents the actual MCP tool
      list/parameters, and the user chose not to have it guessed at. Needs
      real input from whoever owns the MCP server implementation.
- [x] **Phase 1c(changelog) — `changelog/` content migration.** Pulled
      directly from the live `GitBook` org via the GitBook MCP (see "Live
      source access" below), not from `legacy-content/`. Structure mirrors
      the live space: `README.md` (current year, 2026), `2025.md`,
      `2024.md`, `2023.md`, `2022-and-earlier.md`. The live space also has
      3 hidden/internal pages (`changelog-automation-spec`,
      `changelog-checklist`, `examples`) — internal process docs, not
      migrated since they aren't part of the public changelog.
- [x] **Phase 1d — `api/`, `cli/`, `custom-components/` content migration.**
      Migrated from a separate local checkout at
      `~/Desktop/Development/integrations/docs` (the source for GitBook's
      own developer docs site), not from `legacy-content/` and not by
      reading the live site — per the user's steer to use the local copy
      they already had.
      - `api/`: grew from 5 → 9 pages. Added `reference/rate-limiting.md`,
        `reference/pagination.md`, `reference/errors.md`,
        `reference/client-libraries.md` — real source content with no home
        in the original thin stub set (same pattern as the earlier
        `documentation/learn/api-documentation/` expansion).
      - `cli/`: all 5 pages migrated as originally stubbed. The CLI
        reference is the single canonical source for both content commands
        and integration commands — `custom-components/cli-reference.md` is
        now just a one-line pointer to it, to avoid duplicating the same
        reference in two spaces.
      - `custom-components/`: grew from 9 → 14 pages. Source had
        significant duplication — some files (`blocks/*`,
        `contentkit/interactivity.md`, `runtime/receiving-requests.md`,
        top-level `reference/action.md` etc.) were superseded copies not
        listed in the source repo's own `SUMMARY.md`; skipped those in
        favor of the versions actually in the source's nav
        (`guides/*`, `development/*`). Added `manifest-reference.md` (the
        full `gitbook-manifest.yaml` reference, previously going to be
        folded into `integration-concepts.md` but too large) and split
        `development-guides.md` into a `guides/` section with 4 real pages
        (interactivity, link unfurling, HTTP requests, webhook
        integration) instead of one stub. `getting-started/
        build-your-first-integration.md` looked pre-drafted from an
        earlier pass but turned out to be a header-only skeleton — filled
        in with the real quickstart steps.
      - Recurring risk handled throughout: relative markdown links cannot
        cross space boundaries (`api/`, `cli/`, `custom-components/` are
        three separate GitBook spaces) — replaced with descriptive text
        ("Developers → CLI → CLI reference") wherever the source linked
        across what are now space boundaries.

## Live source access (GitBook MCP)

As of 2026-07-27, this session has a working GitBook MCP connection
(`claude mcp add --transport http gitbook https://mcp.gitbook.com/mcp`,
then browser sign-in) authenticated as Addison, with access to the live
`GitBook` organization (id `d8f63b60-89ae-11e7-8574-5927d48c4877`) among
many others. This is a live, real GitBook account — treat it as read access
for pulling source content only. **Never write to the live org** —
everything in this repo only gets published to the real docs site once
Git Sync is wired up per the plan in this doc; nothing should go through
`create_change_request` / `submit_or_merge_change_request` against the
live spaces below as part of this migration.

`list_sites` on that org (`site_p4Xo4`, "GitBook Documentation") returned
this structure — space IDs worth reusing for later phases:

| Section | Space | Space ID | Notes |
|---|---|---|---|
| Changelog | Public Changelog | `PGZZo1PCN4rYgFLPD8Cl` | ✅ migrated into `changelog/` above. Git-synced to the private `GitbookIO/changelog` GitHub repo (confirmed private — `git clone`/API both 404 unauthenticated), so MCP was the only way in. |
| Developers → Developers documentation | Developer documentation | `mWAQqV10C1JYYSHIhazJ` | Unverified candidate for `cli/` and/or the developer-facing half of `custom-components/` — content not yet inspected. |
| Developers → API Reference | API Reference | `sl6xsVSSdwhn9wsovTPU` | Unverified candidate for `api/` — content not yet inspected. |
| Resources → Policies | GitBook Site Policy | `-LBUnokgAHp7SX9tJUrr` | Unverified candidate for `policies/` — content not yet inspected. |
| Resources → Help Center | Help Center | `Ua3kTfM3iWAoECzM0u90` | Not currently mapped to any new section — may be worth a look, could overlap with `documentation/resources/get-support.md`. |
| Developers (top-level section) | Developer Documentation | `2SyQSbIa1iYS7z6Dx5di` | A *second*, differently-named "Developers" entry alongside the "Developers" section group above — likely one is stale. Needs a look before trusting either as the `api/`/`cli/` source. |

No candidate space spotted yet for `education/`.

To pull a page: `get_page(spaceId, path)`. Large pages exceed the tool's
inline token limit and get saved to a `tool-results/*.txt` file instead —
strip the first two lines (an MCP-added `Page "..." — id: ..., path: ...`
header + blank line) before using the rest as the real page content.
- [ ] **Phase 2 — Redirects.** Diff the live URL snapshot against the final
      new structure; build old→new redirect map. Figure out where redirects
      live under the new multi-space `docs.yaml` setup (old setup used a
      single root `.gitbook.yaml` `redirects:` block — need to confirm
      whether that's per-space now, or site-level).
- [ ] **Phase 3 — QA & cutover.** Verify no dead links, no missing redirects,
      review with team, wire up Git Sync per the new `docs.yaml`, go live.

## Redirects

- Old redirect format (for reference): `legacy-content/.gitbook.yaml` had a
  root-level `redirects:` map of `old-path: relative/file.md`.
  `legacy-content/.gitbook.yaml` only covers redirects *within* this repo's
  prior restructures — it does not cover the other sections being merged in.
- Full current live URL list: `legacy-content/_reference/live-urls-snapshot-2026-07-24.md`.
  Re-fetch from `https://gitbook.com/docs/llms.txt` closer to cutover since
  it'll drift as other teams keep publishing.
- Redirect mapping itself (old URL → new path) is Phase 2 work, blocked on
  Phase 1 being far enough along to know final new paths.

## Open questions

- Where do the source repos/spaces for `api`, `cli`, `education`,
  `changelog`, `policies` live? Need locations before Phase 1 can start on
  them.
- Does `docs.yaml` support per-space redirect config, or is there a
  site-level redirects mechanism for the new monorepo setup?
- Any content that should be cut/retired entirely rather than migrated?
