# Customization recipes

Worked examples of `SiteCustomizationSettings` payloads for the most common branding scenarios. The single most useful reference here is **`example-site/customization.json`** — a real export from a production-style site. Read it before attempting any customization payload; it shows how all the nested fields fit together far better than any abstract example.

The pattern in every recipe: **GET current settings, modify the fields you care about with a small script, PUT the result back.** Don't construct payloads from scratch — required nested structures evolve and the GET response is your safest starting point.

```bash
ORG_ID=...
SITE_ID=...
GET_URL="https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/customization"
PUT_URL="$GET_URL"

CURRENT=$(curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" "$GET_URL")
NEW=$(echo "$CURRENT" | jq '<your modifications>')
curl -s -X PUT -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" -d "$NEW" "$PUT_URL"
```

## Scenario 0 — Ultimate defaults (apply once, then layer brand on top)

When you've created a site on the Ultimate plan, several feature flags should be turned **on by default** because they're what the user paid for. Apply this recipe first, then layer Scenario 1 or 2 on top for the actual brand.

```jq
.ai.mode = "assistant"                                     # AI Assistant (Ultimate exclusive in full mode)
| .ai.suggestions = []                                     # populate with 3-5 starter prompts during structure design
| .pdf.enabled = true                                      # PDF export per page
| .advancedCustomization.enabled = true                    # custom CSS/JS, custom fonts, etc.
| .trademark.enabled = false                               # hide "Powered by GitBook" footer (paid plans only)
| .pageActions.externalAI = true                           # "Open in ChatGPT" / "Open in Claude" buttons
| .pageActions.markdown = true                             # "Copy as markdown"
| .pageActions.mcp = true                                  # "Connect via MCP"
| .git.showEditLink = true                                 # "Edit on GitHub" / "Edit on GitLab" link on git-synced pages
```

Notes:

- The AI assistant needs `ai.suggestions` populated to be useful — empty starts cold. Three to five short questions visitors are likely to ask: *"How do I authenticate?"*, *"What are the rate limits?"*, *"How do I set up webhooks?"*. Gather these from the user during structure design.
- `trademark.enabled = false` is the typical Ultimate choice — paying for an Ultimate plan and leaving "Powered by GitBook" up is the unusual option, not the default.
- `pageActions` defaults to all-true on new Ultimate sites in some org configurations and all-false in others. Setting them explicitly removes the variance.
- Don't set Ultimate-only fields on a `basic` site — the API will accept the PUT and silently drop them, but the result looks broken. If the user is on free, skip this scenario entirely.

## Scenario 1 — Minimal brand pass

Goal: just change the site title, primary color, and favicon emoji. No paid features.

```jq
.title = "Acme Docs"
| .styling.theme = "clean"
| .styling.primaryColor = {"light": "#0E5BFF", "dark": "#5B8CFF"}
| .favicon = {"emoji": "📘"}
```

Notes:

- Colors are themed pairs — always supply both `light` and `dark` even if they're identical. Format is `#xxxxxx`.
- **Picking a dark-mode counterpart when the user gives only one color.** Brand colors usually look right on white but disappear (or burn) against a dark background. Two safe defaults: (a) ask the user for a dark variant and offer to derive one, or (b) lighten the brand color until it has roughly 4.5:1 contrast against `#0F172A` — typically pulling lightness up by 25–35% in HSL space. For a deep brand color like `#2D6A4F` (forest green), a paired light variant is around `#74C69D`; for `#534AB7` (deep indigo), around `#B2A5FF`. If unsure, set `light` and `dark` to the same value as a fallback — flat but legible.
- `favicon` accepts `{emoji: "📘"}` for an emoji or `{icon: {light: "...", dark: "..."}}` for hosted SVG/PNG URLs (themed).
- `styling.theme` choices: `clean`, `muted`, `bold`, `gradient`.

This works on free sites.

## Scenario 2 — Full brand with logos, fonts, semantic colors, footer

Goal: custom logo (light + dark), Inter font with IBM Plex Mono for code, semantic colors aligned with brand, branded footer with link groups and copyright. Requires Premium or Ultimate.

This recipe mirrors the example-site export — read `example-site/customization.json` for the exact shape of every nested field.

### A note on `header.logo.light` vs `header.logo.dark`

The schema field name describes **which mode the logo is shown in**, not the colour of the logo file. When a brand provides two logo files, ask explicitly which goes where if it isn't obvious — file names like `logo-dark.svg` ambiguously mean either "the dark-coloured logo" (intended for light backgrounds) or "the logo for dark mode" (a light-coloured logo). The schema is unambiguous:

- `header.logo.light` = the URL shown on light-mode pages → typically a dark-coloured logo
- `header.logo.dark` = the URL shown on dark-mode pages → typically a light-coloured logo

Same convention for `footer.logo` and `favicon.icon`.

```jq
.title = "Acme Platform Documentation"
| .styling.theme = "clean"
| .styling.primaryColor = {"light": "#534AB7", "dark": "#B2A5FF"}
| .styling.tint        = {"color": {"light": "#F5F3FF", "dark": "#1E1B2E"}}
| .styling.infoColor = {"light": "#534AB7", "dark": "#534AB7"}
| .styling.warningColor = {"light": "#FE9A00", "dark": "#FE9A00"}
| .styling.dangerColor = {"light": "#FB2C36", "dark": "#FB2C36"}
| .styling.font = "Inter"
| .styling.monospaceFont = "IBMPlexMono"
| .styling.corners = "rounded"
| .styling.depth = "flat"
| .styling.icons = "duotone"
| .styling.sidebar = {"background": "filled", "list": "default"}
| .styling.search = "prominent"
| .header.logo = {"light": "https://acme.com/logo-light.svg", "dark": "https://acme.com/logo-dark.svg"}
| .header.links = [
    {
      "title": "Dashboard",
      "style": "link",
      "to": {"kind": "url", "url": "https://app.acme.com"},
      "links": [],
      "localizedTitle": {}
    },
    {
      "title": "Get a demo",
      "style": "button-primary",
      "to": {"kind": "url", "url": "https://acme.com/demo"},
      "links": [],
      "localizedTitle": {}
    }
  ]
| .footer.logo = {"light": "https://acme.com/logo-mono.svg", "dark": "https://acme.com/logo-mono-dark.svg"}
| .footer.copyright = "© 2026 Acme, Inc."
| .footer.groups = [
    {
      "title": "Product",
      "localizedTitle": {},
      "links": [
        {"title": "Features", "localizedTitle": {}, "to": {"kind": "url", "url": "https://acme.com/features"}},
        {"title": "Pricing",  "localizedTitle": {}, "to": {"kind": "url", "url": "https://acme.com/pricing"}}
      ]
    },
    {
      "title": "Company",
      "localizedTitle": {},
      "links": [
        {"title": "About",   "localizedTitle": {}, "to": {"kind": "url", "url": "https://acme.com/about"}},
        {"title": "Careers", "localizedTitle": {}, "to": {"kind": "url", "url": "https://acme.com/careers"}}
      ]
    }
  ]
| .favicon = {"icon": {"light": "https://acme.com/favicon.svg", "dark": "https://acme.com/favicon-dark.svg"}}
```

Notes:

- `font` and `monospaceFont` accept presets (`Inter`, `Roboto`, `IBMPlexMono`, `JetBrainsMono`, etc.) or full `CustomizationFontDefinitionInput` objects with hosted woff2 files. Use a preset unless the brand demands a specific custom font.
- Each header link needs `links: []` even if there's no submenu, and `localizedTitle: {}` even if there are no translations — the schema requires the keys.
- `header.preset = "default"` is also part of the response — leave it as-is.
- If a PUT with custom logos returns 400 or 403, the site is on a tier that doesn't permit custom logos. Either upgrade or fall back to the minimal recipe.

## Scenario 3 — Localized titles for a multi-language site

When auto-translation is enabled on a site, header and footer link titles can be localized so each language sees the right label. The `localizedTitle` map keys are language codes; English typically lives in the top-level `title` field, with translations in `localizedTitle`.

```jq
.footer.groups[0] = {
  "title": "Products",
  "localizedTitle": {"de": "Produkte", "es": "Productos", "fr": "Produits", "zh": "产品"},
  "links": [
    {
      "title": "Payments",
      "localizedTitle": {"de": "Zahlungen", "es": "Pagos", "fr": "Paiements", "zh": "支付"},
      "to": {"kind": "space", "space": "<paymentsSpaceId>"}
    }
  ]
}
```

The site title itself accepts `localizedTitle` too — set it for any user-facing string the site exposes per language.

## Scenario 4 — Conditional header links (gated by visitor claims)

Goal: show "Sign in" to logged-out visitors and "Sign out" to logged-in visitors. Both buttons live in the same `header.links` array, differentiated by their `condition` strings.

```jq
.header.links += [
  {
    "title": "Sign in",
    "style": "button-secondary",
    "to": {"kind": "url", "url": "https://app.acme.com/login"},
    "links": [],
    "localizedTitle": {},
    "condition": "visitor.claims.unsigned.persona !== \"customer\""
  },
  {
    "title": "Sign out",
    "style": "button-secondary",
    "to": {"kind": "url", "url": "https://app.acme.com/logout"},
    "links": [],
    "localizedTitle": {},
    "condition": "visitor.claims.unsigned.persona === \"customer\""
  }
]
```

The condition language is JS-like and references `visitor.claims` resolved at render time. Common patterns:

- **Persona switching**: `visitor.claims.unsigned.persona === "partner"`
- **Plan gating**: `visitor.claims.signed.plan === "enterprise"`
- **Logged-in check**: `visitor.claims.signed`

Use `unsigned` claims for hints from URL params (e.g. `?visitor.persona=prospect`); use `signed` claims for verified ones from authenticated sessions.

## Scenario 5 — Link to a space or specific page

Header and footer links can target a whole space or a specific page in a space, not just URLs:

```jq
# Link a footer item to the changelog space
.footer.groups[0].links += [{
  "title": "Changelog",
  "localizedTitle": {},
  "to": {"kind": "space", "space": "<changelogSpaceId>"}
}]

# Link to a specific page inside a space
.footer.groups[0].links += [{
  "title": "Latest release",
  "localizedTitle": {},
  "to": {"kind": "page", "page": "<pageId>", "space": "<spaceId>"}
}]
```

Get space and page IDs from the structure response or by looking them up in the space API.

## Scenario 6 — Theme mode default and toggle

```jq
.themes.default = "system"  # follow the visitor's OS preference; alternatives: "light", "dark"
| .themes.toggeable = true  # visitors can override
```

### True-black dark mode via `styling.tint`

For a dark mode that's actually dark — a true `#000000` page background instead of GitBook's default soft-dark-gray (`~#0F1419`) — set `styling.tint.color.dark` to pure black. The rest of the dark palette (cards, sidebars, code blocks) is calculated against the tint, so this anchors everything else to true black.

```jq
.styling.tint = {
    "color": {
      "light": "#FFFFFF",   # pure white in light mode (rare; default off-white usually reads better)
      "dark":  "#000000"    # true black in dark mode — OLED-friendly, high-contrast
    }
  }
```

Pair with a dark-by-default theme for the cleanest effect:

```jq
.themes.default = "dark"
| .themes.toggeable = true
| .styling.tint.color.dark = "#000000"
```

This is the single highest-impact knob for dark-mode aesthetics — without it, dark mode looks washed out compared to the user's brand expectations.

## Scenario 7 — AI assistant and page actions

```jq
.ai.mode = "assistant"
| .ai.suggestions = [
    "How do I authenticate with the API?",
    "What pricing tier supports SSO?",
    "How do I set up webhooks?"
  ]
| .pageActions.externalAI = true   # show "Open in ChatGPT" menu
| .pageActions.markdown = true     # show "Copy as markdown"
| .pageActions.mcp = true          # show "Connect via MCP"
```

`ai.mode` choices: `none`, `search` (search-only), `assistant` (full chat). Up to 5 suggestions, each 3–64 chars. `pageActions` are independent toggles — leave any unset to keep the current value.

## Scenario 8 — Social accounts in header / footer

```jq
.socialAccounts = [
  {"platform": "twitter",  "handle": "acme",         "display": {"footer": true,  "header": false}},
  {"platform": "github",   "handle": "acmeinc/docs", "display": {"footer": true,  "header": true}},
  {"platform": "linkedin", "handle": "company/acme", "display": {"footer": true,  "header": false}}
]
```

`platform` choices include `twitter`, `github`, `linkedin`, `youtube`, `discord`, `facebook`, `instagram`, `mastodon`, `bluesky`. The `handle` format is platform-specific — twitter is just the username, github accepts `user` or `user/repo`, linkedin uses `company/<slug>`.

## Scenario 9 — Per-site-space override

When a multi-space site has one space that needs different branding (e.g. an internal docs space with no AI and a different logo), set the overrides on the site-space:

```bash
SITE_SPACE_ID=...
SS_GET_URL="https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/site-spaces/$SITE_SPACE_ID/customization"

SS_CURRENT=$(curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" "$SS_GET_URL")

# Disable AI just for this space
SS_NEW=$(echo "$SS_CURRENT" | jq '.ai.mode = "none"')

curl -s -X PUT -H "Authorization: Bearer $GITBOOK_TOKEN" \
  -H "Content-Type: application/json" -d "$SS_NEW" "$SS_GET_URL"
```

To reset the override and fall back to site-wide settings:

```bash
curl -s -X DELETE -H "Authorization: Bearer $GITBOOK_TOKEN" \
  "https://api.gitbook.com/v1/orgs/$ORG_ID/sites/$SITE_ID/site-spaces/$SITE_SPACE_ID/customization"
```

## Field cheatsheet

A quick reference for the customization fields most often touched. For the full nested schema, look at the response of a GET — every field present there is settable. The bundled `example-site/customization.json` shows realistic values for nearly all of them.

| Field path | Purpose | Notes |
|---|---|---|
| `title` / `localizedTitle` | Site title in header | 2–128 chars; localizedTitle is `{en, fr, ...}` |
| `internationalization.locale` | Default locale | **Deprecated** — kept for read compatibility only |
| `styling.theme` | Visual preset | `clean | muted | bold | gradient` |
| `styling.primaryColor` | Brand color | Themed `{light, dark}` |
| `styling.tint` | Subtle site-wide tint applied to text/icons/UI | `{color: {light, dark}}` — does **not** affect links/buttons (those use primaryColor) |
| `styling.infoColor`, `successColor`, `warningColor`, `dangerColor` | Semantic colors | Themed pairs (Premium for full control) |
| `styling.font` | Body font | Preset name or font definition |
| `styling.monospaceFont` | Code font | Preset name or font definition |
| `styling.corners` | Border radius style | `straight | rounded | circular` |
| `styling.depth` | Shadow style | `subtle | flat` |
| `styling.icons` | Icon weight | `regular | solid | duotone | light | thin` |
| `styling.background` | Page background | **Required by API** despite older docs marking it deprecated. Set to `"plain"` on new sites, or echo whatever GET returns on round-trip updates. POSTing without it returns `422 expected "background" to be defined`. |
| `styling.links` | Link style | `default | accent` |
| `styling.sidebar.background` | Sidebar bg | `default | filled` |
| `styling.sidebar.list` | Sidebar list style | `default | pill | line` |
| `styling.codeTheme.default` | Default code-block theme | `{light, dark}` strings like `default-light` |
| `styling.codeTheme.openapi` | OpenAPI block theme | Same shape as `.default` |
| `styling.search` | Search bar prominence | `prominent | subtle` |
| `favicon` | Site favicon | `{emoji}` or `{icon: {light, dark}}` |
| `header.preset` | Header layout preset | **Deprecated** — use `styling.theme` instead |
| `header.logo` | Themed logos in header | `{light: <url-for-light-mode>, dark: <url-for-dark-mode>}` (Premium). Schema field name = which mode shows it, not the colour of the file. |
| `header.backgroundColor`, `header.linkColor` | Header colours | **Deprecated** — use theming colours |
| `header.links[]` | Top-nav items | `{title, style, to, links, localizedTitle, condition?}`. **`links: []` is required** even when the item has no sub-menu — POSTing without it returns `422 expected "links" to be defined`. |
| `header.primaryLink` | Where the logo links to | A `ContentRef` (see Content references section) |
| `footer.logo` | Themed footer logo | Same shape as `header.logo` (Premium) |
| `footer.groups[]` | Footer link groups | Each: `{title, localizedTitle, links}` |
| `footer.copyright` | Copyright line | Up to 300 chars |
| `themes.default` | Default mode | `light | dark | system` |
| `themes.toggeable` | Allow visitor toggle | bool |
| `ai.mode` | AI feature level | `none | search | assistant` |
| `ai.suggestions` | Starter prompts | Up to 5, 3–64 chars each |
| `pdf.enabled` | PDF export button | bool |
| `feedback.enabled` | Page feedback widget | bool |
| `pagination.enabled` | Prev/next page links | bool |
| `pageActions.externalAI` | "Open in ChatGPT" | bool |
| `pageActions.markdown` | "Copy as markdown" | bool |
| `pageActions.mcp` | "Connect via MCP" | bool |
| `externalLinks.target` | Outbound link target | `self | blank` |
| `trademark.enabled` | "Powered by GitBook" | bool — paid plans can disable |
| `socialPreview.url` | OG image URL | string URL |
| `socialAccounts[]` | Social icons | `{platform, handle, display: {footer, header}}` |
| `git.showEditLink` | "Edit on GitHub" link | bool |
| `insights.trackingCookie` | GitBook analytics cookie | bool |
| `advancedCustomization.enabled` | Allow custom CSS/JS | bool (Enterprise) |
| `privacyPolicy.url` | Footer privacy link | string URL |
| `announcement` | Site-wide banner | `{enabled, message, link?, style: info|warning|danger|success}` |

## Things that look like customization but aren't

A few related settings live elsewhere in the API:

- **Custom domain** — set on the *site* itself (`Site.hostname`), not in customization. PATCH the site object.
- **Site visibility** (public, share-link, etc.) — also on the site object.
- **Per-page layout** (cover, table of contents visibility) — set in page frontmatter; see the `write-gitbook` skill.
- **Auto-translation enablement** — UI-only today (Site → Sections → Translations).

Don't try to put any of these in the customization payload; the API will reject them.
