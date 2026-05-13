# Branding schema reference

The `SiteCustomizationSettings` schema is large. Read this file before composing any customization payload, and read `references/example-site/customization.json` for a real-world worked example showing how all the nested fields fit together. For ready-made payloads for common scenarios, see `customization-recipes.md`.

## Contents

- Fields that matter most for branding
- Deprecated fields (don't introduce on new sites)
- Required-but-vestigial fields (gotchas)
- Content references (the `to` field)
- Conditional links
- Plan-gated features

## Fields that matter most

- **`title`** — site title (the one shown in the header). Plus `localizedTitle: {en: ..., fr: ..., ...}` for translations.
- **`styling.theme`** — preset: `clean` (default-modern), `muted` (low-contrast), `bold` (high-contrast), or `gradient` (colorful)
- **`styling.primaryColor`** — `{light: "#xxxxxx", dark: "#xxxxxx"}` — the brand color, used for links, buttons, accents
- **`styling.tint`** — `{color: {light, dark}}` — a subtle tint applied across text, icons, and UI elements (search bar, etc.). Does **not** affect link/button colour (those keep `primaryColor`). This is the field most brand guides mean when they say "background tint" or "secondary surface colour".
- **`styling.infoColor` / `successColor` / `warningColor` / `dangerColor`** — semantic colors, each a themed pair
- **`styling.font` / `styling.monospaceFont`** — pick a preset (`Inter`, `IBMPlexMono`, etc.) or supply a custom font definition with hosted woff2 files
- **`styling.corners`** — `straight | rounded | circular`
- **`styling.depth`** — `subtle | flat`
- **`styling.icons`** — `regular | solid | duotone | light | thin`
- **`styling.sidebar.background`** — `default | filled`
- **`styling.sidebar.list`** — `default | pill | line`
- **`styling.codeTheme.default` / `styling.codeTheme.openapi`** — themed code-block colors
- **`styling.search`** — `prominent | subtle`
- **`favicon`** — `{icon: {light, dark}}` (themed URLs) or `{emoji: "📘"}`
- **`header.logo`** — `{light: <url-shown-in-light-mode>, dark: <url-shown-in-dark-mode>}` (Premium feature). The schema field name is the *mode the URL is shown in*, not the colour of the file. Brand guides often use ambiguous file names like `logo-dark.svg` (which can mean "the dark-coloured logo" — for light backgrounds — or "the logo for dark mode" — a light-coloured file). When in doubt, ask the user explicitly.
- **`header.links`** — top-nav items. Each item has `title`, `style` (`link | button-primary | button-secondary`), `to` (a `ContentRef` — see below), `links: []` (for sub-menus), and an optional `condition` for conditional visibility.
- **`footer.logo`** — same shape as header.logo (Premium)
- **`footer.groups`** — grouped link lists for the footer. Each group has `title` (with optional `localizedTitle`) and `links`.
- **`footer.copyright`** — string up to 300 chars
- **`themes.default`** — `light | dark | system`; `themes.toggeable` controls whether visitors can switch
- **`ai.mode`** — `none | search | assistant`; `ai.suggestions` for canned questions
- **`pageActions`** — booleans: `externalAI` (open-in-ChatGPT), `markdown` (copy as markdown), `mcp` (connect via MCP)
- **`pagination.enabled`** — prev/next page links at the bottom of pages
- **`feedback.enabled`** — page feedback widget
- **`pdf.enabled`** — PDF export button
- **`socialAccounts`** — list of `{handle, platform, display: {footer, header}}` for icons in header/footer
- **`git.showEditLink`** — whether the "Edit on GitHub" link appears on git-synced pages
- **`externalLinks.target`** — `self | blank` for outbound links
- **`insights.trackingCookie`** — whether GitBook places its analytics cookie
- **`advancedCustomization.enabled`** — whether advanced CSS/JS is allowed (Enterprise)
- **`announcement`** — site-wide banner: `{enabled, message, link?, style: info|warning|danger|success}`

## Deprecated fields (don't introduce on new sites)

A handful of fields are present in responses but **deprecated** and should not be set on new sites: `internationalization.locale`, `header.preset` (use `styling.theme`), `header.backgroundColor`, `header.linkColor`. Leave existing values alone when round-tripping a GET; just don't introduce them.

## Required-but-vestigial fields (gotchas)

- **`styling.background`** reads as deprecated in some docs, but the API rejects POST/PUT without it (`422 expected "background" to be defined`). Treat it as required-but-vestigial — set to `"plain"` on new sites, or echo whatever GET returns on round-trip updates. Modern theming runs through `styling.tint` instead.
- **`header.links[].links: []`** — every entry in `header.links[]` requires a `links: []` array even when there's no sub-menu. The API rejects link items without it.

## Content references (the `to` field)

Header links, footer links, and `header.primaryLink` all use a `ContentRef` to specify destination. Three forms:

- **External URL**: `{kind: "url", url: "https://..."}`
- **Whole space**: `{kind: "space", space: "<spaceId>"}`
- **Specific page**: `{kind: "page", page: "<pageId>", space: "<spaceId>"}` (use this to deep-link to e.g. the latest changelog entry)

## Conditional links

Header links can carry a `condition` field — a JS-like expression evaluated against `visitor.claims`. Pattern from the example site:

```json
{ "title": "Sign in",  "condition": "visitor.claims.unsigned.persona !== \"partner\"", ... }
{ "title": "Sign out", "condition": "visitor.claims.unsigned.persona === \"partner\"",  ... }
```

This is how the same site shows different navigation to logged-in vs. logged-out visitors. The conditions reference visitor claims that GitBook resolves at render time.

## Plan-gated features

A few features (custom logos, custom fonts, semantic colors, footer logo, advanced customization, disabling the GitBook trademark) require Premium or Ultimate site plans. The API will reject these on free sites with 400/403 — handle the error gracefully and tell the user.
