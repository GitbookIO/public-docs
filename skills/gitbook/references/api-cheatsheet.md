# GitBook API cheatsheet

All endpoints are at `https://api.gitbook.com/v1`. Authentication is `Authorization: Bearer $GITBOOK_TOKEN` on every request. JSON throughout.

This cheatsheet is scoped to what the `manage-gitbook-site` skill actually needs. The full API surface is much larger — for less common endpoints, search the GitBook docs directly.

## Auth and discovery

The PAT lives in 1Password — fetch it once at the start of the session and export it as an env var. Never store it on disk, never echo it back, never commit it.

```bash
# Fetch the PAT from 1Password (replace with the user's actual secret reference)
export GITBOOK_TOKEN=$(op read "op://<vault>/<item>/<field>")

# Verify token and get the authenticated user
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/user

# List the user's organizations
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs
```

If `op read` fails (not signed in, wrong reference, missing item), surface the exact error and stop — don't fall back to asking the user to paste the token.

When the user has multiple orgs, **show the list with org titles and ask them to confirm by name**, even if there's only one — site creation in the wrong org is a real and visible mistake. Save the chosen `organizationId` for the rest of the session.

## Sites

### Create a site

```bash
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "My Product Docs",
    "type": "basic",
    "visibility": "public"
  }' \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites
```

Request body fields:

- `title` (required, 2–128 chars)
- `type` — `basic | premium | ultimate | sponsored`. Defaults to `basic`. Premium/ultimate features (custom logos, custom fonts, etc.) require a paid plan.
- `visibility` — `public | unlisted | share-link | visitor-auth`. Defaults to `public`.
- `spaces` — optional array of existing space IDs to link immediately. Omit when creating a fresh site without pre-existing spaces.

Response is the full `Site` object. Save `id` for subsequent calls; the `urls.app` is the dashboard URL the user can open.

### List sites in an org

```bash
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites
```

### Get / update a site

```bash
# Get
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID

# Update (PATCH)
curl -s -X PATCH -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title": "New Title"}' \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID
```

## Spaces

### Create a space (in an org)

```bash
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Guides",
    "emoji": "📚",
    "visibility": "in-collection"
  }' \
  https://api.gitbook.com/v1/orgs/$ORG_ID/spaces
```

Notes:

- `title` is required (max 50 chars)
- `emoji` is optional but useful for nav
- `visibility` for site spaces is typically `in-collection` (visibility is then controlled by the site)
- The created space starts empty; you'll connect it to git or import content separately

### Get a space / list a space's tree

```bash
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/spaces/$SPACE_ID

# Get the content tree (pages and groups)
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/spaces/$SPACE_ID/content
```

### Get the Git Sync state of a space

```bash
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/spaces/$SPACE_ID/git/info
```

Returns `{repoName, installationProvider: "github" | "gitlab", integration, url, updatedAt}` when sync is set up; 404 when not. Use this to verify the user finished the UI handoff.

**There is no API to *set up* Git Sync.** This is the load-bearing constraint of this whole workflow.

## Site sections, section groups, and site-spaces

A site's navigation is structured as one of three shapes:

1. A flat list of site-spaces (no sections), or
2. A list of sections, each containing one or more site-spaces, or
3. A list of section groups and/or sections, with section groups containing nested sections (used to bucket related sections in the top nav)

A **section** is a unit of top-nav navigation; a **section group** wraps related sections; a **site-space** is the binding between a section and a space.

### Sections vs. site-spaces — pick the right one

This is the most common API confusion. The TL;DR:

- If the spaces are **semantically distinct** (the common case — "Guides", "API Reference", "Changelog" are different bodies of content) → **use sections**. Each section gets its own top-nav tab and URL slug.
- If the spaces are **variants of the same content** → use site-spaces directly. The canonical use case is auto-translation (one English space, plus auto-translated French/German/Japanese variants — all at the same URL with a language switcher). It's a niche feature.

Defaulting to sections is almost always correct. If you find yourself reaching for `POST /site-spaces` for unrelated content, you probably want `POST /sections` instead.

### Add a section to a site

The pattern is **POST + PATCH** because the POST silently drops some fields:

```bash
# Step 1: POST creates the section with title, icon, and the linked space
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "spaceId": "<existing-space-id>",
    "title": "Developers",
    "icon": "code"
  }' \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/sections
# → returns the created section with id="<section-id>"

# Step 2: PATCH sets the description (POST silently drops it)
curl -s -X PATCH -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "description": "API reference, SDKs, and webhooks."
  }' \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/sections/<section-id>
```

Required on POST: `spaceId` (existing space). Strongly recommended: `title` (2–128 chars), `icon` (Font Awesome name like `code`, `house`, `id-card`, `clock-rotate-left`).

**`description` must be set via PATCH after creation** — POSTing it inline is accepted by the API but the value is dropped from the created section. Same applies to `localizedTitle` and `localizedDescription` (language→string maps).

The created section also gets `path` (URL slug derived from title), `default`, `draft`, and a `siteSpaces` array.

### The auto-created wrapper section gotcha

When you create a site with `type: site` and then add spaces via `POST /site-spaces` (instead of `POST /sections`), GitBook auto-creates a wrapper section named after the site itself to contain them. If you later want to convert to a proper sections-based layout, you have to:

1. Create the new sections you actually want.
2. `DELETE` the auto-created wrapper section.

Conversely, if you start with sections from the beginning, this never appears. **Default to creating sections explicitly from the start** to avoid the cleanup later.

### Add an existing space to a site as a site-space (translation variants)

For the auto-translation variant case only:

```bash
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "spaceId": "<existing-space-id>",
    "sectionId": "<optional-section-id>"
  }' \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/site-spaces
```

If `sectionId` is omitted, the space is added at the root level (or in the default section). For unrelated content, **use sections instead** — see above.

### Section groups

When a site has 3+ closely related sections, they can be wrapped in a **section group** (e.g. "Products" wrapping Payments / Identity / Connect). The structure response shows these as objects with `"object": "site-section-group"` containing a `sections` array. Section groups are typically created and reordered through the GitBook UI today; the API documentation should be checked for current support before assuming a specific endpoint shape.

### Get the full site structure

```bash
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/structure
```

Returns `{type: "sections" | "siteSpaces", structure: [...]}`. Each entry in `structure` has an `object` field — `site-space`, `site-section`, or `site-section-group` — and is recursive (groups can contain more groups).

For each `site-section`, the `siteSpaces` array contains one entry per language. Only the language that originated from Git has a populated `gitSync` field on its space; the rest are auto-translated and live entirely in GitBook. See `references/example-site/structure.json` for a complete real-world example.

## Customization (branding)

The customization endpoints are the meat of the branding workflow. The schema is large — there are recipe examples in `customization-recipes.md`; this section just shows the mechanics.

### Get current customization

```bash
# Site-wide (the default that applies to all spaces)
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/customization

# Per-site-space override
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/site-spaces/$SITE_SPACE_ID/customization
```

### Update customization

The customization endpoint expects a *full* `SiteCustomizationSettings` payload. The safe pattern is read-modify-write:

```bash
# 1. Get current
CURRENT=$(curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/customization)

# 2. Modify in jq (or in a small script)
NEW=$(echo "$CURRENT" | jq '.styling.primaryColor = {"light": "#0E5BFF", "dark": "#5B8CFF"} | .styling.theme = "clean"')

# 3. PUT it back
curl -s -X PUT -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d "$NEW" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/customization
```

### Reset a per-site-space override

```bash
curl -s -X DELETE -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/site-spaces/$SITE_SPACE_ID/customization
```

This drops the override; the site-space falls back to the site-wide settings.

## Imports (alternative to Git Sync)

When the user wants to ingest existing external content quickly:

```bash
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "source": {
      "type": "website",
      "url": "https://docs.example.com"
    },
    "target": {
      "space": "<spaceId>"
    },
    "enhance": true
  }' \
  https://api.gitbook.com/v1/org/$ORG_ID/imports
```

Source can also be `{"type": "file", "files": [...]}` for a file-based import. The `enhance: true` flag has GitBook's AI clean up the imported content. Returns a `ContentImportRun` with an `id` you can poll.

## Apply a space template

```bash
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"id": "<template-id>"}' \
  https://api.gitbook.com/v1/spaces/$SPACE_ID/content/template
```

Templates are a quick way to seed an empty space with reasonable starter content. The template ID must be one the org has access to.

## OpenAPI specs

API reference spaces should auto-generate their endpoint pages from an OpenAPI spec rather than have them hand-authored. The spec is registered at the org level and referenced from a space's `SUMMARY.md` via `type: builtin:openapi`.

### Register a spec from a URL

The simplest path — the spec lives somewhere reachable (GitHub Pages, raw file in a repo, your own CDN), and GitBook fetches it on a schedule.

```bash
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "slug": "lyra-feedback-v1",
    "source": {
      "url": "https://lyra-app.github.io/api/v1/openapi.yaml"
    }
  }' \
  https://api.gitbook.com/v1/orgs/$ORG_ID/openapi
```

Response includes the spec object with `id`, `slug`, `processingState`. The slug is what goes into the space's SUMMARY.md.

### Register a spec by uploading the file directly

Use this when the spec isn't hosted publicly, or when the source-of-truth should live in GitBook rather than a separate repo.

```bash
curl -s -X POST -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -F "slug=lyra-feedback-v1" \
  -F "file=@./openapi.yaml" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/openapi
```

### List, get, update, delete

```bash
# List specs in an org
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/openapi

# Get one spec
curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/openapi/$SPEC_ID

# Update (replace) a spec — same body shape as create
curl -s -X PATCH -H "Authorization: Bearer $GITBOOK_TOKEN" ...

# Delete
curl -s -X DELETE -H "Authorization: Bearer $GITBOOK_TOKEN" \
  https://api.gitbook.com/v1/orgs/$ORG_ID/openapi/$SPEC_ID
```

### Two upload strategies — when to pick which

| Strategy | Best when | Cons |
|---|---|---|
| URL-based (GitBook fetches from your URL) | Spec is auto-generated by CI in your repo, has its own review process, or needs to live alongside other developer assets | GitBook only refreshes on a schedule or manual trigger; broken/unreachable URL means no docs |
| Direct upload (file goes into GitBook) | Spec is hand-authored, doesn't change often, or you want GitBook to own the canonical copy | No automatic refresh from upstream; updates require a re-upload |

**Ask the user which they prefer.** Both are valid; assuming one is wrong roughly half the time.

### Reference the spec from SUMMARY.md

Once the spec is registered, link to it from the space's `SUMMARY.md`. The pattern uses a fenced YAML block as the bullet content rather than a regular link:

````markdown
## Feedback API

* [Overview](feedback-api/README.md)
* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: true
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: lyra-feedback-v1
  ```
````

`spec: lyra-feedback-v1` matches the slug from the registration step. `models: true` includes a separate "Models" page; `downloadLink: true` adds a "Download spec" button to the rendered pages.

GitBook expands this entry at render time into one nav item per operation in the spec, grouped by tag. The hand-authored `Overview` page above stays as prose context (base URL, version policy, what this resource is for), with the auto-generated operation pages alongside it.

## Error handling notes

- **401 Unauthorized** — bad PAT. Surface this clearly; don't retry silently.
- **403 Forbidden** — usually a permission issue (PAT belongs to a user without access to the org/site, or the feature requires a higher site plan).
- **404 Not Found** — wrong ID, or the resource was deleted. For sites/spaces this is permanent after 7 days.
- **409 Conflict** — usually means the requested operation would not change state (e.g. transferring a space to its current org).
- **412 Precondition Failed** — operation can't be done in the current state.
- **400 Bad Request** — schema problem; the response body usually says which field.

When a customization update fails with 400, log the offending field and check `customization-recipes.md` for the right shape — it's almost always a missing required nested field or a wrong color format.
