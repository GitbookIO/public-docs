# API workflow

The standard sequence of GitBook REST API calls for creating, updating, and verifying sites. For exact request bodies and response shapes, use this in conjunction with `api-cheatsheet.md`.

## Contents

- The standard sequence for a new site
- Multi-language sites and auto-translated spaces
- Section groups (three levels of nav nesting)
- Updating an existing site
- When to use Imports vs. Git Sync
- Verification

All endpoints are at `https://api.gitbook.com/v1`. Auth is `Authorization: Bearer $GITBOOK_TOKEN`.

## The standard sequence for a new site

1. **Verify the token and find the org**: `GET /v1/user`, then `GET /v1/orgs`.
2. **Create the site**: `POST /v1/orgs/{organizationId}/sites` with `{title, type, visibility, spaces?}`. **Default to Ultimate** (`type: "site"` is the API value; the plan tier is set on the site after creation or via the org's billing). Use `type: "basic"` (free) only when the user explicitly opts in. Don't include `spaces` if no spaces exist yet — you can add them later.
3. **Decide how spaces will come into being.** Two paths:
   - **Git-Sync-first (recommended)**: tell the user to create each space in the GitBook UI by clicking "Add new space" → "Sync to a GitHub or GitLab repository", picking the repo and the per-space project directory. This creates the space, sets up sync, and links it to the site in one action. The skill's job is to give exact, copyable instructions (one block per space). See `git-sync-handoff.md`.
   - **API-first**: create empty spaces via the API (see `api-cheatsheet.md`), add them to the site with `POST /v1/orgs/{orgId}/sites/{siteId}/site-spaces`, and use the Imports API or template application to load content. The user will still need to wire Git Sync in the UI later if they want bidirectional sync.
4. **Add sections** (multi-space sites with grouped navigation): `POST /v1/orgs/{orgId}/sites/{siteId}/sections`. A section is created by associating a space with a title and optional icon.
5. **Resolve cross-space link sentinels**: if the scaffolded markdown contains `XSPACE_<KEY>` placeholders (which it should, for any link that crosses a space boundary), now is when you substitute them for the real space IDs returned by step 3 or 4. See `cross-space-links.md` for the substitution script. Commit and push the changes — the next Git Sync run picks them up.
6. **Apply customization** (branding): `PUT` the `SiteCustomizationSettings` for the site or for individual site-spaces. Full schema in `branding-schema.md`. Worked examples in `customization-recipes.md`.
7. **Verify**: `GET /v1/orgs/{orgId}/sites/{siteId}/structure` to see the final tree and `GET .../customization` to confirm settings.

## Multi-language sites and auto-translated spaces

GitBook supports **auto-translated site-spaces**: a single English space (synced from Git) can be paired with computed translations in other languages. The translations are not separate spaces in the Git repo — they live entirely in GitBook and are configured through the UI under each section's settings. The API exposes them as additional `site-space` objects under the same section, each with a different `language` and no `gitSync` field.

What this means in practice:

- **Don't scaffold per-language directories in the repo.** The Git repo has one space per topic, in English. Write one set of markdown files per content area, full stop.
- **Each section can hold many site-spaces.** A "Payments" section might contain `Payments` (en, git-synced), `Payments (FR)` (fr, computed), `Payments (DE)` (de, computed), etc. The structure response will list all of them; only the English ones need a Git Sync handoff.
- **`localizedTitle` shows up everywhere.** Sections, section-groups, header links, footer links, and the site title itself all carry a `localizedTitle: {de: "...", fr: "...", ...}` map. When reading the customization, expect to see translations even for fields the user only set in English. Don't strip these out unless asked.
- Auto-translation is a UI-only feature today. If the user wants it enabled on a section, surface that as part of the Git Sync handoff: "After Git Sync is configured, go to **Site → Sections → Payments → Translations** and enable the languages you want."

When the user asks for "a docs site in five languages", the answer is one English content tree in Git plus auto-translation enabled per section in the UI — not five copies of the markdown.

## Section groups (three levels of nav nesting)

A site's structure has three possible levels of nesting in the navigation:

1. **Site-spaces** at the root (a flat site, no sections)
2. **Sections** containing site-spaces (the typical multi-space site)
3. **Section groups** containing sections containing site-spaces (used to bucket related sections, e.g. "Products" group containing Payments / Identity / Connect sections)

The `GET /v1/orgs/{orgId}/sites/{siteId}/structure` response is recursive — a section-group's `sections` array can hold both sections and other section-groups. When designing the structure, use section-groups only when there are 3+ closely related sections that benefit from being visually grouped in the top nav. For a 2-section site, sections at the root level are clearer.

## Updating an existing site

When asked to modify a site that already exists, *always* fetch the current state first:

- `GET /v1/orgs/{orgId}/sites/{siteId}` for site metadata
- `GET /v1/orgs/{orgId}/sites/{siteId}/structure` for sections + spaces
- `GET /v1/orgs/{orgId}/sites/{siteId}/customization` (or the per-site-space variant) for branding

Then make targeted PATCH/PUT/POST/DELETE calls. Don't replace whole customization payloads if you only mean to change one field — get the current settings, modify in memory, and PUT the result back.

## When to use Imports vs. Git Sync

- **Imports API** (`POST /v1/org/{orgId}/imports`) is for ingesting external content (a website URL, a set of files) into a space. It's good for one-shot migrations from another doc tool.
- **Git Sync** is for ongoing two-way sync between a Git repo and a space. This is what the standard flow optimizes for.
- If the user has already-good content sitting outside both Git and GitBook (e.g. a Notion export), use Imports to get it in, then optionally turn on Git Sync afterward.
