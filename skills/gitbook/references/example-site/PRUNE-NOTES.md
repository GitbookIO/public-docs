# PRUNE-NOTES — what's missing from this bundled copy

This `example-site/` is a curated subset of the full Evolve Demo repo, trimmed to keep the skill under client file limits while preserving every distinctive structural and syntactic pattern. The original site has more content; if you want to study it in its complete form, look at the source repo on GitHub or the published site.

The full original tree is faithfully captured in two files alongside this one — read them when you need the un-pruned picture:

- **`structure.json`** — the response from `GET /v1/orgs/{orgId}/sites/{siteId}/structure` for the original site. Lists every section, section-group, and site-space (including all auto-translated language variants). The English site-spaces it lists are what the original Git repo had as folders; everything pruned below is still represented here.
- **`SUMMARY.md`** files within each remaining space — these still describe the original page tree, including any pages whose individual `.md` files were removed in the prune. Treat the SUMMARY as canonical for the original IA.

## What was removed

### `developers/v1/` and `developers/v3/` — entire folders gone

The original site demonstrated a **versioned developer documentation** pattern: three coexisting versions of the developer docs side-by-side, used to show how a real product handles API lifecycles in GitBook.

- `developers/v1/` — the **legacy** version (older API, kept around for customers who haven't migrated).
- `developers/v2/` — the **current stable** version (kept in this bundled copy).
- `developers/v3/` — the **beta / prerelease** version (next major API, available for early adopters).

All three folders had the same internal structure:

```
developers/v{N}/
├── README.md
├── SUMMARY.md
├── .gitbook/vars.yaml
├── connect-api/README.md
├── identity-api/README.md
├── payments-api/README.md
├── getting-started/
│   ├── authentication.md
│   ├── conventions.md
│   ├── for-ai-agents.md
│   ├── quickstart.md
│   └── sdks.md
├── mcp/
│   ├── README.md
│   └── connecting-an-agent.md
└── webhooks/
    ├── README.md
    ├── event-catalog.md
    ├── retries-and-replay.md
    └── verifying-signatures.md
```

The content differences across versions were small and version-specific — endpoint paths, deprecation notices, breaking-change callouts, slightly different OpenAPI references. The structural and component patterns are identical, so v2 alone is a faithful representative.

The `developers/openapi/` folder still contains all three versioned spec files (`v1/`, `v2/`, `v3/`) — those are tiny and demonstrate the pattern of co-located versioned OpenAPI specs that the developer spaces reference.

**The pattern to take away**: when a product has multiple coexisting API versions, give each its own space, group them under one section ("Developers"), and keep their structure parallel so users can compare like-for-like across versions. Each version's space gets its own folder in the Git repo. The customization can use a top-level navigation hint (e.g. "v2 is current — view [v1](legacy) or [v3 beta](preview)") to orient visitors.

### `connections/blog/`, `community/`, `youtube/` — kept one article each

The original site had **6–7 article HTML files per connections subfolder**, intended as external content surfaces that the GitBook AI assistant indexes alongside the docs. These aren't pages in any space — they're standalone HTML files that simulate "the company's blog / forum / YouTube channel" for demo purposes.

Each subfolder now contains:

- The `index.html` (which lists what was there originally — keep this as a record of what existed)
- One representative article showing the metadata pattern

What this demonstrates:

- **Blog**: `<meta name="author">` (real-name byline), `article:published_time`, topical `keywords`. Standard editorial content. Sample kept: `same-day-payouts-tradeoffs.html`.
- **Community forum**: similar shape but `author` is a username/handle — gives the AI assistant a different signal about authority and tone. Sample kept: `webhook-retries-backoff.html`.
- **YouTube**: distinctive `<meta property="video:duration">` and `og:type=video.other` — useful when the AI assistant wants to recommend video content over written content. Sample kept: `webhooks-deep-dive.html`.

The `index.html` files in each subfolder reference the full original article list, so the original shape is recoverable from those.

**The pattern to take away**: external content surfaces (blog, forum, video) that the AI assistant pulls from alongside docs should each have consistent metadata (`author`, `published_time`, `keywords` at minimum) so the assistant can attribute and rank them. Different content types benefit from type-specific OpenGraph metadata (e.g. video duration).

## What was kept and why

Everything else is intact, including:

- All product spaces (`payments`, `identity`, `connect`) with their full page trees
- The `home/` space with its `.gitbook/includes/` content blocks
- All `guides/` subspaces (help-center, integrations, tutorials)
- `partners/` and `changelog/` in full
- `developers/v2/` (the canonical example) and `developers/openapi/` (all three versions)
- All `.gitbook/vars.yaml` files
- All `SUMMARY.md` files
- Top-level `customization.json` and `structure.json`
