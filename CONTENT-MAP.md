# Content Map — legacy-content → new structure

Page-level companion to `RESTRUCTURE.md` (which has folder-level mapping and
phase status). This file is planning-only — **no content has been migrated
based on this map yet**, though the first review pass below did add/remove a
handful of stub pages to close structural gaps found during mapping.

## Summary

- **175** new content pages across `ai/`, `api/`, `cli/`, `custom-components/`,
  `documentation/`, `education/`, `changelog/`, `policies/` (excluding
  `SUMMARY.md` files; includes every hub `README.md`). Originally 171 —
  net +4 after this review pass added 6 stub pages (`configure-the-test-it-button.md`,
  `use-the-openapi-proxy.md`, `updates.md`, `mermaid.md`, `prompt.md`,
  `agent/style-guide.md`) and cut 1 (`snippets.md`, no source, confirmed not needed).
  - **~99** have a clear 1:1 or split/merge source in `legacy-content/`.
  - **~15** are already fully drafted, real content (not stubs) — mostly the
    "quickstart"-style tutorials. Nothing to migrate into these.
  - **~60** have **no local source** — concentrated in `api/`, `cli/`,
    `education/`, `changelog/`, `policies/`, and the developer-facing half of
    `custom-components/`. Confirms the gap already noted in `RESTRUCTURE.md`.
- **178** legacy pages (excluding root `README.md`, `SUMMARY.md`,
  `.gitbook/includes/*` snippets, and `.gitbook/assets/*`).
  - **All 178** now map onto one or more new pages after this review pass
    resolved every originally-unmapped group — see "Unmapped legacy pages"
    below.
- Phase status: still **Phase 0 complete, Phase 1 not started** (see
  `RESTRUCTURE.md`). This map is prep for Phase 1.

Legend: **✅ source** = legacy page(s) to draw from. **⚠️ partial** = related
but incomplete source. **❌ none** = no local source, needs net-new content or
content from another GitBook space.

## Decisions log (resolved after first review)

- **OpenAPI "Test it"/proxy gap** — resolved. Added two new stub pages:
  `learn/api-documentation/configure-the-test-it-button.md` and
  `learn/api-documentation/use-the-openapi-proxy.md`, wired into
  `documentation/SUMMARY.md`. Source: `api-references/guides/configuring-the-test-it-button.md`,
  `api-references/guides/using-openapi-proxy.md`.
- **Updates / Mermaid / Prompt blocks** — resolved. Added three new stub
  pages under `learn/creating-content/blocks/`: `updates.md`, `mermaid.md`,
  `prompt.md`, wired into `documentation/SUMMARY.md`. Source:
  `creating-content/blocks/updates.md`, `mermaid-blocks.md`, `prompt.md`.
- **Snippets block** — cut. No legacy source and confirmed not needed;
  removed the stub page and its `SUMMARY.md` entry.
- **Divider block** — kept. No legacy source, but confirmed as a real
  current block; stays as a blank stub until Phase 1 content is written.
- **`gitbook-agent/automatic-docs-improvements.md` split** — confirmed. This
  one legacy page is the source for two different new pages:
  `documentation/learn/gitbook-ai/agent/run-an-audit.md` (the Agent-run-audit
  workflow) and `documentation/learn/analytics/insights/fix-gaps-with-agent.md`
  (the "fix this content gap" action from the Insights dashboard). Phase 1
  needs to actually split this content across both rather than duplicating it
  wholesale — table in "Learn → Analytics" below has the detail.
- **Billing FAQ duplicate** — confirmed, already resolved in the table below:
  `account-management/cancelling-a-plan.md` → `account-and-billing/cancel-a-subscription.md`;
  `account-management/billing-faq/cancelling-a-plan.md` (the FAQ fragment) →
  `account-and-billing/plans-and-billing-policy.md`, which absorbs billing
  policy + FAQ together. Don't migrate the FAQ file's content into
  `cancel-a-subscription.md` too.
- **`integrations/` retire candidates** — cut, confirmed. `integrations/slack.md`,
  `integrations/visual-studio-code.md`, and all of `integrations-beta/`
  (`README.md`, `slack.md`, `visual-studio-code.md`, `github-entities.md`) are
  old/stale per-integration pages — do not migrate. No new stub needed.
- **`docs-site/insights.md` split** — proposed split below (see "Learn →
  Analytics" section) covering Traffic / Pages & Feedback / Broken URLs /
  Search / Links into `analytics/README.md`, MCP into
  `readers-ai/mcp-server-for-published-docs.md`, and OpenAPI into
  `api-documentation/how-gitbook-renders-openapi.md`. Flagged for a look
  since it touches three different sections — see that section for the full
  reasoning.
- **Orphaned pages** — folded into existing pages per section tables below:
  `all-content.md` + `searching-your-content/*` → `resources/the-gitbook-interface.md`;
  `collaboration/notifications.md` → `account-and-billing/personal-and-organization-settings.md`;
  `creating-content/broken-links.md` → FAQ note in `learn/publishing/create-redirects.md`.
  **Exception:** `creating-content/styleguide.md` was too large to fold into
  an existing page — resolved instead by adding a new standalone stub,
  `learn/gitbook-ai/agent/style-guide.md`, wired into `SUMMARY.md` under
  GitBook AI → Agent.

---

## Documentation (`documentation/`)

### `account-and-billing/`

| New page | Source | Notes |
|---|---|---|
| `cancel-a-subscription.md` | ✅ `account-management/cancelling-a-plan.md` | Duplicate exists at `account-management/billing-faq/cancelling-a-plan.md` — same topic, reconcile during migration, don't merge both verbatim. |
| `how-pricing-works.md` | ✅ `account-management/plans/README.md`, `plans/community/README.md`, `plans/community/sponsored-site-plan.md`, `plans/legacy-plans.md` | |
| `personal-and-organization-settings.md` | ✅ `account-management/account-settings.md`, `account-management/organization-settings.md` + `collaboration/notifications.md` | Notifications (app/email notification settings, delivery troubleshooting) folds in here — resolved, see decisions log. |
| `plans-and-billing-policy.md` | ✅ `account-management/plans/billing-policy.md` + billing FAQ content in `account-management/billing-faq/cancelling-a-plan.md` | Stub note says this "absorbs billing policy and billing FAQ" — confirms the FAQ duplicate above gets folded in here, not into cancel-a-subscription. |
| `sso-and-saml.md` | ✅ `account-management/sso-and-saml/README.md`, `sso-and-saml/sso-members-vs-non-sso.md` | |

### `getting-started/`

| New page | Source | Notes |
|---|---|---|
| `quickstart.md` | Already drafted (tutorial) | Legacy `getting-started/quickstart.md` is reference/inspiration only, not a direct source. |
| `switch-to-gitbook.md` | ✅ `getting-started/import.md` | |

### `learn/access/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ implied by `site-access/authenticated-access/README.md` + `site-access/adaptive-content/README.md` | No single legacy hub page — new hub merges two legacy hubs. |
| `adaptive-content-concepts.md` | ✅ `site-access/adaptive-content/README.md`, `enabling-adaptive-content/authenticated-access.md` | |
| `configure-adaptive-content.md` | ✅ `site-access/adaptive-content/enabling-adaptive-content/README.md`, `cookies.md`, `url.md`, `feature-flags.md`, `authenticated-access.md` | Four legacy pages (one per claim-source method) merge into one new page. |
| `write-content-conditions.md` | ✅ `site-access/adaptive-content/adapting-your-content.md` + `creating-content/blocks/conditional-content.md` | Conditional-content block docs move out of "Creating content" and into "Access" here — confirms the folder-level note in `RESTRUCTURE.md`. |
| `test-with-segments.md` | ✅ `site-access/adaptive-content/testing-with-segments.md` | |
| `troubleshoot-adaptive-content.md` | ❌ none | No legacy troubleshooting page for adaptive content exists — net new. |
| `authenticated-access/README.md` | ✅ `site-access/authenticated-access/README.md`, `enabling-authenticated-access.md` | |
| `authenticated-access/auth0.md` | ✅ `site-access/authenticated-access/setting-up-auth0.md` | |
| `authenticated-access/aws-cognito.md` | ✅ `site-access/authenticated-access/setting-up-aws-cognito.md` | |
| `authenticated-access/azure-ad.md` | ✅ `site-access/authenticated-access/setting-up-azure-ad.md` | |
| `authenticated-access/okta.md` | ✅ `site-access/authenticated-access/setting-up-okta.md` | |
| `authenticated-access/oidc.md` | ✅ `site-access/authenticated-access/setting-up-oidc.md` | |
| `authenticated-access/custom-backend.md` | ✅ `publishing-documentation/authenticated-access/setting-up-a-custom-backend.md` | |

### `learn/analytics/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `docs-site/insights.md` (intro) | |
| `google-analytics.md` | ✅ `docs-site/insights.md` (GA cookie/integration section) | Only a fragment of the legacy page — most of `insights.md` is the Traffic/Search/Links/MCP/OpenAPI sections, which don't have their own new stub (see below). |
| `events-aggregation-api.md` | ❌ none | No legacy page documents an analytics API — net new. |
| `insights/README.md` | ✅ `docs-site/ai-insights.md` (intro/dashboard) | |
| `insights/dashboard.md` | ✅ `docs-site/ai-insights.md` (AI insights dashboard section) | |
| `insights/browse-by-topic.md` | ✅ `docs-site/ai-insights.md` (Topics section) | |
| `insights/identify-content-gaps.md` | ✅ `docs-site/ai-insights.md` (FAQ: "How do I use AI insights?") | |
| `insights/review-an-answer.md` | ✅ `docs-site/ai-insights.md` (Questions section) | |
| `insights/fix-gaps-with-agent.md` | ⚠️ partial — `gitbook-agent/automatic-docs-improvements.md` | Same legacy source also feeds `gitbook-ai/agent/run-an-audit.md` below — confirmed one-to-two split. Suggested divide: `run-an-audit.md` covers *running* an Agent audit from the Agent/change-request surface; `fix-gaps-with-agent.md` covers *acting on a specific gap* surfaced from the Insights dashboard (the "fix with Agent" button on a question/gap row). Same underlying feature, two different entry points. |

**Resolved (proposed split, flag for a look since it spans sections):**
`docs-site/insights.md` covers Site Analytics as a whole, with 9 sub-sections.
Two of them (Agent & LLMs, Ask AI) already duplicate content covered by the
`ai-insights.md`-sourced pages above — don't re-migrate those, they're the
same feature described twice in legacy. The rest split as:
- **Traffic, Pages & Feedback, Broken URLs, Search, Links** → fold into
  `analytics/README.md` as the core "Site Analytics dashboard" walkthrough
  (filters/groups, custom time periods, and these five data-type tabs). This
  matches the stub's own purpose note ("hub for insights and analytics
  integrations").
- **OpenAPI** (analytics tab) → fold into
  `learn/api-documentation/how-gitbook-renders-openapi.md` as a short
  "viewing OpenAPI analytics" section.
- **MCP** (analytics tab) → fold into
  `learn/gitbook-ai/readers-ai/mcp-server-for-published-docs.md` as a short
  "viewing MCP analytics" section.
This spreads one legacy page across three different new sections — flagging
so it doesn't get missed when those other two sections are migrated.

### `learn/api-documentation/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `api-references/openapi/README.md` | |
| `add-an-openapi-spec.md` | ✅ `api-references/openapi/add-an-openapi-specification.md`, `insert-api-reference-in-your-docs.md` | |
| `structure-your-api-reference.md` | ✅ `api-references/guides/structuring-your-api-reference.md` + `api-references/guides/openapi-layouts.md` | |
| `code-samples-and-enums.md` | ✅ `api-references/guides/adding-custom-code-samples.md`, `describing-enums.md` | |
| `automate-spec-updates.md` | ✅ `api-references/guides/support-for-ci-cd-with-api-blocks.md` | |
| `openapi-extensions.md` | ✅ `api-references/extensions-reference.md` | |
| `how-gitbook-renders-openapi.md` | ⚠️ partial — `api-references/guides/managing-api-operations.md` | Best-guess fit but not a clean match; "managing operations" is more operational than conceptual. Also absorbs the OpenAPI-analytics fragment of `docs-site/insights.md` — see the Analytics section flag. |
| `configure-the-test-it-button.md` *(new)* | ✅ `api-references/guides/configuring-the-test-it-button.md` | New stub page added — see decisions log. |
| `use-the-openapi-proxy.md` *(new)* | ✅ `api-references/guides/using-openapi-proxy.md` | New stub page added — see decisions log. |

### `learn/collaboration/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `collaboration/share.md` (intro) | |
| `invite-and-manage-members.md` | ✅ `collaboration/share.md`, `member-management/invite-members-to-your-organization.md`, `member-management/teams.md` | |
| `roles-permissions-inheritance.md` | ✅ `collaboration/member-management/permissions-and-inheritance.md`, `member-management/roles.md` | |
| `comments-and-live-editing.md` | ✅ `collaboration/comments.md`, `collaboration/live-edits.md` | |
| `change-requests/README.md` | ✅ `collaboration/change-requests/README.md` | Stub note says it "absorbs the old workflow concept page" — confirms this is the merge target. |
| `change-requests/create.md` | ✅ `collaboration/change-requests/change-requests-screen.md` | |
| `change-requests/review-and-merge.md` | ✅ `collaboration/change-requests/change-requests-in-a-space.md` | |
| `change-requests/merge-rules.md` | ✅ `collaboration/merge-rules.md` | |

**Resolved:** `collaboration/notifications.md` folds into
`documentation/account-and-billing/personal-and-organization-settings.md`
(see Account and billing section below) — it's fundamentally an account
settings page (notification preferences, email delivery troubleshooting),
not a collaboration-feature page.

### `learn/creating-content/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `creating-content/formatting/README.md` (intro) | |
| `the-editor.md` | ❌ none | No legacy page describes the editor as a standalone concept — net new. |
| `format-your-content.md` | ✅ `creating-content/formatting/README.md`, `creating-content/formatting/inline.md` | |
| `markdown-reference.md` | ✅ `creating-content/formatting/markdown.md` | |
| `content-structure.md` | ✅ `creating-content/content-structure/README.md`, `content-structure/space.md`, `content-structure/collection.md`, `content-structure/page/README.md` | |
| `version-history-and-page-tags.md` | ✅ `creating-content/content-structure/page/tags.md`, `creating-content/version-control.md` | |
| `reusable-content-and-variables.md` | ✅ `creating-content/variables-and-expressions.md`, `creating-content/reusable-content.md` | |
| `blocks/README.md` | ✅ `creating-content/blocks/README.md` | |
| `blocks/paragraph.md` | ✅ `creating-content/blocks/paragraph.md` | |
| `blocks/heading.md` | ✅ `creating-content/blocks/heading.md` | |
| `blocks/unordered-list.md` | ✅ `creating-content/blocks/unordered-list.md` | |
| `blocks/ordered-list.md` | ✅ `creating-content/blocks/ordered-list.md` | |
| `blocks/task-list.md` | ✅ `creating-content/blocks/task-list.md` | |
| `blocks/hint.md` | ✅ `creating-content/blocks/hint.md` | |
| `blocks/quote.md` | ✅ `creating-content/blocks/quote.md` | |
| `blocks/code-block.md` | ✅ `creating-content/blocks/code-block.md` | |
| `blocks/files.md` | ✅ `creating-content/blocks/insert-files.md` | Renamed. |
| `blocks/image.md` | ✅ `creating-content/blocks/insert-images.md` | Renamed. |
| `blocks/embed-a-url.md` | ✅ `creating-content/blocks/embed-a-url.md` | |
| `blocks/table.md` | ✅ `creating-content/blocks/table.md` | |
| `blocks/cards.md` | ✅ `creating-content/blocks/cards.md` | |
| `blocks/tabs.md` | ✅ `creating-content/blocks/tabs.md` | |
| `blocks/expandable.md` | ✅ `creating-content/blocks/expandable.md` | |
| `blocks/stepper.md` | ✅ `creating-content/blocks/stepper.md` | |
| `blocks/drawing.md` | ✅ `creating-content/blocks/drawing.md` | |
| `blocks/math-and-tex.md` | ✅ `creating-content/blocks/math-and-tex.md` | |
| `blocks/page-link.md` | ✅ `creating-content/blocks/page-link.md` | |
| `blocks/columns.md` | ✅ `creating-content/blocks/columns.md` | |
| `blocks/button.md` | ⚠️ partial — `creating-content/formatting/inline.md#buttons` | Legacy content is a section inside `inline.md`, not a standalone file. |
| `blocks/divider.md` | ❌ none | No legacy source — confirmed real current block, kept as a blank stub for now (no cut). |
| ~~`blocks/snippets.md`~~ | — | **Cut, confirmed.** No legacy source. Stub page and SUMMARY.md entry removed. |
| `blocks/updates.md` *(new)* | ✅ `creating-content/blocks/updates.md` | New stub page added — see decisions log. |
| `blocks/mermaid.md` *(new)* | ✅ `creating-content/blocks/mermaid-blocks.md` | New stub page added — see decisions log. |
| `blocks/prompt.md` *(new)* | ✅ `creating-content/blocks/prompt.md` | New stub page added — see decisions log. |

**Still open:** the `inline.md` anchors for **Icons**, **Expressions**, and
**Custom blocks** have no explicit new home (Expressions likely folds into
`reusable-content-and-variables.md`; Custom blocks likely means
`documentation/learn/custom-components/`; Icons is unclear) — not addressed
yet, needs a decision before Phase 1 touches this page.

**Resolved — folded into other pages (not this section):**
`creating-content/all-content.md` and `creating-content/searching-your-content/README.md`
+ `quick-find.md` (Quick Find palette) → `documentation/resources/the-gitbook-interface.md`
(see Resources section below) — these are app-navigation/UI-tour content, a
better fit there than in Creating content. `creating-content/broken-links.md`
→ a short FAQ note in `learn/publishing/create-redirects.md` (see Publishing
section below) — the page itself says the feature is currently unavailable
and points readers to redirects instead, so treat as retired functionality
with just a pointer, not a full migration.

**Resolved:** `creating-content/styleguide.md` (style guide setup, Agent
enforcement rules, templates) is too large to fold into an existing page —
added a new standalone stub, `learn/gitbook-ai/agent/style-guide.md`,
wired into `SUMMARY.md` under GitBook AI → Agent (see that section below).

### `learn/custom-components/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `integrations/install-an-integration.md` (intro) | |
| `install-and-manage.md` | ✅ `integrations/install-an-integration.md` | |
| `build-your-own.md` | N/A — router page | Stub explicitly says "canonical home of: nothing — this is a router page." No content to migrate; just needs a link to `custom-components/`. |

**Cut, confirmed:** `integrations/slack.md`, `integrations/visual-studio-code.md`,
`integrations/integrations-beta/*` (duplicate beta versions of Slack/VS
Code + `github-entities.md`) — old, per-integration detail pages,
`hidden`/`noIndex` in legacy. Not migrated. `integrations/git-sync/bi-directional-git-integration.md`
is misfiled under `integrations/` in legacy — its actual content is Git Sync,
already covered by `learn/git-sync/how-git-sync-works.md`.

### `learn/customization/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `docs-site/customization/README.md` | |
| `themes-colors-typography.md` | ✅ `docs-site/customization/icons-colors-and-themes.md` | |
| `layout-and-navigation.md` | ✅ `docs-site/customization/layout-and-structure.md` | |
| `social-sharing-and-custom-code.md` | ✅ `docs-site/customization/sharing-and-social.md`, `docs-site/customization/extra-configuration.md` | |
| `site-settings-reference.md` | ✅ `docs-site/site-settings.md` | Stub note says it "absorbs the old customization FAQ" — check `docs-site/site-settings.md` for an embedded FAQ section. |

### `learn/embed/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `docs-site/embedding/README.md` | |
| `what-the-docs-embed-is.md` | ✅ `docs-site/embedding/README.md` (concept portion) | |
| `install-the-embed.md` | ✅ `docs-site/embedding/implementation/README.md`, `script.md`, `nodejs.md`, `react.md` | Three implementation methods merge into one page. |
| `authenticate-the-embed.md` | ✅ `docs-site/embedding/using-with-authenticated-docs.md` | |
| `customize-the-embed/README.md` | ✅ `docs-site/embedding/configuration/README.md`, `customizing-docs-embed.md` | |
| `customize-the-embed/custom-tools-for-the-assistant.md` | ✅ `docs-site/embedding/configuration/creating-custom-tools.md` | |
| `embed-api-reference.md` | ✅ `docs-site/embedding/configuration/reference.md` | |

### `learn/git-sync/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `getting-started/git-sync/README.md` | |
| `how-git-sync-works.md` | ✅ `getting-started/git-sync/README.md` + `integrations/git-sync/bi-directional-git-integration.md` | |
| `enable-github-sync.md` | ✅ `getting-started/git-sync/enabling-github-sync.md` | |
| `enable-gitlab-sync.md` | ✅ `getting-started/git-sync/enabling-gitlab-sync.md` | |
| `gitbook-yaml-configuration.md` | ✅ `getting-started/git-sync/content-configuration.md` | |
| `preview-pull-requests.md` | ✅ `getting-started/git-sync/github-pull-request-preview.md` | |
| `troubleshoot-git-sync.md` | ✅ `getting-started/git-sync/troubleshooting.md` | |
| `work-with-monorepos.md` | ✅ `getting-started/git-sync/monorepos.md` | |
| `make-batch-changes.md` | ⚠️ partial — `getting-started/git-sync/monorepos.md` | No dedicated legacy page for batch changes; best partial fit. |

**Flag:** `getting-started/git-sync/commits.md` (Commit messages & Autolink)
has no explicit new stub — likely folds into `gitbook-yaml-configuration.md`
or `how-git-sync-works.md`, needs a decision.

### `learn/gitbook-ai/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `gitbook-agent/what-is-gitbook-agent.md` + `ai-and-search/gitbook-ai-assistant.md` (combined intro) | |
| `agent-vs-assistant.md` | ❌ none | No legacy page draws this distinction explicitly — net new orientation page. |
| `agent/README.md` | ✅ `gitbook-agent/what-is-gitbook-agent.md` | |
| `agent/write-and-edit.md` | ✅ `gitbook-agent/write-and-edit-with-ai.md` | |
| `agent/review-change-requests.md` | ✅ `gitbook-agent/review-change-requests-with-gitbook-agent.md` | |
| `agent/run-an-audit.md` | ⚠️ partial — `gitbook-agent/automatic-docs-improvements.md` | Shared source with `analytics/insights/fix-gaps-with-agent.md` — split needed. |
| `agent/style-guide.md` *(new)* | ✅ `creating-content/styleguide.md` | New stub page added — see decisions log. Large page; migrate in full, don't compress. |
| `agent/ai-translations.md` | ✅ `gitbook-agent/translations.md` | |
| `agent/channels.md` | ✅ `publishing-documentation/channels.md` | |
| `assistant/README.md` | ✅ `ai-and-search/gitbook-ai-assistant.md` | |
| `assistant/enable-assistant.md` | ✅ `ai-and-search/gitbook-ai-assistant.md` (setup section) | |
| `assistant/knowledge-sources.md` | ✅ `ai-and-search/connections/README.md`, `intercom.md`, `zendesk.md`, `pylon.md`, `github-discussions.md`, `github-issues.md` | Five connector pages merge into one; stub already lists Slack/Discord and "external doc sites" and "MCP as source" as placeholders with **no legacy source at all** for those three — genuinely net new. |
| `ai-search.md` | ✅ `docs-site/ai-search.md` | |
| `readers-ai/README.md` | ✅ `publishing-documentation/mcp-servers-for-published-docs.md` + `ai-and-search/llm-ready-docs.md` (combined intro) | |
| `readers-ai/make-your-docs-agent-ready.md` | ✅ `ai-and-search/llm-ready-docs.md` | |
| `readers-ai/mcp-server-for-published-docs.md` | ✅ `publishing-documentation/mcp-servers-for-published-docs.md` | |

### `learn/publishing/`

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `docs-site/publish-a-docs-site/README.md` | |
| `what-published-means.md` | ⚠️ partial — `docs-site/publish-a-docs-site/README.md` (concept portion) | |
| `publish-and-unpublish.md` | ✅ `docs-site/publish-a-docs-site/public-publishing.md`, `share-links.md` | |
| `seo-and-publishing-options.md` | ⚠️ partial — `docs-site/site-settings.md` (SEO section, if present) | Needs verification — SEO settings may live inside `site-settings.md` rather than a dedicated page. |
| `create-redirects.md` | ✅ `publishing-documentation/site-redirects.md` + FAQ note from `creating-content/broken-links.md` | Broken-links checker page says the feature is currently unavailable and points readers to redirects instead — fold that as a short FAQ ("what happened to broken link detection?") rather than migrating the disabled feature itself. Resolved, see decisions log. |
| `pdf-export.md` | ✅ `docs-site/pdf-export.md` | |
| `custom-domain/README.md` | ✅ `docs-site/custom-domain/README.md` | |
| `custom-domain/custom-subdirectories.md` | ✅ `docs-site/custom-domain/setting-a-custom-subdirectory/README.md`, `configuring-a-subdirectory-with-cloudflare.md`, `configuring-a-subdirectory-with-vercel.md`, `configuring-a-subdirectory-with-aws.md` | Three provider guides merge into one page. |
| `custom-domain/troubleshoot-custom-domains.md` | ❌ none | No legacy troubleshooting page for custom domains — net new. |
| `site-sections-and-variants/README.md` | ✅ `docs-site/site-structure/README.md`, `site-sections.md`, `variants.md` | |
| `site-sections-and-variants/multilingual-sections.md` | ✅ `docs-site/site-structure/multilingual-sections.md` | |

### `resources/`

| New page | Source | Notes |
|---|---|---|
| `get-support.md` | ✅ `help/support.md`, `help/faqs.md`, `help/report-bugs.md`, `help/connectivity-issues.md`, `help/hard-refresh.md` | The entire orphaned `help/` folder (not in legacy SUMMARY.md nav) converges here. |
| `glossary.md` | ✅ `resources/glossary.md`, `resources/concepts.md` | Stub note confirms this "absorbs the old concepts page." |
| `keyboard-shortcuts.md` | ✅ `resources/keyboard-shortcuts.md` | |
| `the-gitbook-interface.md` | ✅ `resources/gitbook-ui/README.md`, `resources/gitbook-ui/toolbar-on-published-sites-and-site-previews.md` + `creating-content/all-content.md`, `creating-content/searching-your-content/README.md`, `creating-content/searching-your-content/quick-find.md` | The "All content" screen and the Quick Find search palette are app-navigation/UI elements, not creating-content concepts — folded in here as part of the interface tour. Resolved, see decisions log. `searching-your-content/README.md`'s Ask AI mention is already covered by `ai-search.md`, don't re-migrate that part. |

---

## Build with AI (`ai/`)

Only `getting-started/ai-documentation/*` in legacy-content overlaps this
section (per `RESTRUCTURE.md`). Confirmed below.

| New page | Source | Notes |
|---|---|---|
| `README.md` | ✅ `getting-started/ai-documentation/README.md` | |
| `getting-started/quickstart.md` | Already drafted (tutorial) | Not sourced from legacy. |
| `getting-started/authenticate-your-agent.md` | ⚠️ partial — `getting-started/ai-documentation/gitbook-mcp.md` (auth mentions) | No dedicated legacy auth page; thin partial source. |
| `getting-started/no-mcp-use-skills-directly.md` | ❌ none | Net new — legacy has no "skills without MCP" fallback content. |
| `gitbook-mcp/overview.md` | ✅ `getting-started/ai-documentation/gitbook-mcp.md` | |
| `gitbook-mcp/connect-your-client.md` | ⚠️ partial — `getting-started/ai-documentation/gitbook-mcp.md` (endpoint section) | |
| `gitbook-mcp/common-workflows.md` | ❌ none | Net new — no legacy "recipes" content. |
| `gitbook-mcp/mcp-tools-reference.md` | ❌ none | Net new — no legacy tool-by-tool reference. |
| `gitbook-skills/overview.md` | ✅ `getting-started/ai-documentation/ai-coding-assistants-and-skillmd.md` | |
| `gitbook-skills/install-skills.md` | ⚠️ partial — `ai-coding-assistants-and-skillmd.md` (install section) | |
| `gitbook-skills/author-your-own-skills.md` | ❌ none | Net new — legacy only covers installing GitBook's own skill, not authoring custom ones. |
| `gitbook-skills/whats-inside-a-skill.md` | ❌ none | Net new. |
| `automate/cli-for-agents.md` | ⚠️ partial — `getting-started/ai-documentation/gitbook-cli.md` (agentic workflows section) | |
| `automate/validate-agent-content-in-ci.md` | ❌ none | Net new. |
| `extend/drop-to-the-api.md` | ⚠️ partial — `getting-started/ai-documentation/gitbook-api.md` | Legacy page is essentially empty (`hidden`/`noIndex`, no body) — treat as no real source. |
| `extend/build-your-own-agent-on-gitbook.md` | ❌ none | Net new. |
| `reference/faq.md` | ❌ none | Net new. |
| `reference/troubleshooting.md` | ❌ none | Net new. |
| `reference/which-mcp-server-do-i-need.md` | ⚠️ partial — cross-cutting concept implied by `gitbook-mcp.md`'s hint about the reader-side server, but never stated as its own disambiguation page. | Net-new framing, existing raw material. |
| `optimizing-for-ai.md` (legacy) | → maps outward | Legacy `getting-started/ai-documentation/optimizing-for-ai.md` doesn't map into `ai/` at all — it's reader-facing, and maps instead to `documentation/learn/gitbook-ai/readers-ai/make-your-docs-agent-ready.md` (already listed above). Flagging here so it isn't missed as "unmapped." |

---

## Custom components (`custom-components/`) — developer-facing half

Legacy source only covers install/manage (already mapped under
`documentation/learn/custom-components/` above). Everything about *building*
a component has no local source:

| New page | Source |
|---|---|
| `getting-started/build-your-first-integration.md` | Already drafted (tutorial) |
| `integration-concepts.md` | ❌ none |
| `contentkit/contentkit-overview.md` | ❌ none |
| `contentkit/contentkit-component-reference.md` | ❌ none |
| `integration-runtime-reference.md` | ❌ none |
| `development-guides.md` | ❌ none |
| `publishing-and-submitting-integrations.md` | ❌ none |
| `cli-reference.md` | N/A — router page, points to `cli/reference/cli-reference.md` |

---

## Sections with no local source at all

Per `RESTRUCTURE.md`'s open question — confirmed by inspection, not just
by folder name:

- **`api/`** (3 pages) — `getting-started/authentication.md`,
  `getting-started/make-your-first-api-call.md`, `reference/api-reference.md`
  are all empty/near-empty placeholders. No legacy page documents GitBook's
  own developer API.
- **`cli/`** (3 pages) — same pattern. `cli/reference/cli-reference.md` has
  a real, detailed stub note (command groups listed) but no legacy source —
  the legacy `getting-started/ai-documentation/gitbook-cli.md` covers *using*
  the CLI for agent workflows (→ already mapped to `ai/automate/cli-for-agents.md`),
  not the command reference itself.
- **`education/`** (2 pages) — `best-practices.md`, `workflow-guides.md`.
  Both are bare titles, no stub notes even. No legacy source.
- **`changelog/`** (0 content pages beyond README/SUMMARY) — no legacy
  source; likely a direct copy from another existing GitBook space per
  `RESTRUCTURE.md`.
- **`policies/`** (0 content pages beyond README/SUMMARY) — same.

---

## Unmapped legacy pages — all resolved in first review pass

All originally-unmapped legacy pages now have a destination (see the
Decisions log at the top and the section tables above for detail):

1. ~~`creating-content/all-content.md`~~ → `resources/the-gitbook-interface.md`. Resolved.
2. ~~`creating-content/styleguide.md`~~ → new standalone stub,
   `learn/gitbook-ai/agent/style-guide.md`. Resolved.
3. ~~`creating-content/broken-links.md`~~ → FAQ note in
   `learn/publishing/create-redirects.md`. Resolved.
4. ~~`creating-content/searching-your-content/README.md` + `quick-find.md`~~ →
   `resources/the-gitbook-interface.md`. Resolved.
5. ~~`creating-content/blocks/updates.md`, `mermaid-blocks.md`, `prompt.md`~~ →
   new standalone stub pages added. Resolved.
6. ~~`collaboration/notifications.md`~~ → `account-and-billing/personal-and-organization-settings.md`. Resolved.
7. ~~`integrations/slack.md`, `visual-studio-code.md`, `integrations-beta/*`~~ →
   cut, confirmed. Resolved.
8. ~~`account-management/billing-faq/cancelling-a-plan.md`~~ → confirmed split
   between `cancel-a-subscription.md` and `plans-and-billing-policy.md`. Resolved.
9. `docs-site/insights.md`'s Traffic / Pages & Feedback / Broken URLs /
   Search / Links / MCP / OpenAPI sections — **proposed split resolved**
   (see Analytics section flag above), but it's a three-way split across
   sections, worth a sanity check once Phase 1 actually reaches that content.

---

## Open items for Phase 1 planning

- No unresolved mapping decisions remain from this review pass. The one
  item below is a "sanity-check when you get there," not a blocker.
- When Phase 1 reaches Analytics/API-documentation/Readers'-AI, double-check
  the `docs-site/insights.md` three-way split (Traffic/Pages & Feedback/Broken
  URLs/Search/Links → `analytics/README.md`; OpenAPI →
  `how-gitbook-renders-openapi.md`; MCP → `mcp-server-for-published-docs.md`)
  still makes sense once that content is actually being written.
- When Phase 1 reaches `agent/run-an-audit.md` and
  `analytics/insights/fix-gaps-with-agent.md`, split
  `gitbook-agent/automatic-docs-improvements.md` per the divide suggested in
  the Analytics section above rather than duplicating it wholesale.
- The `inline.md` anchors for Icons/Expressions/Custom blocks (in Creating
  content) still don't have a confirmed new home — not addressed this pass.
