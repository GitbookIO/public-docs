---
description: Redirect old URLs to new pages when content moves.
---

# Create redirects

{% hint style="info" %}
Site redirects are available on Premium and Ultimate plans.
{% endhint %}

Redirects are especially useful when migrating documentation from another provider, or restructuring content — broken links can hurt SEO, so set up redirects wherever content moves. Beyond the [automatic redirects](#about-automatic-redirects) GitBook creates for you, you can create a redirect from any path in your site's domain.

Redirects can be **Live** or **Draft** — drafts let you prepare and review rules before they affect your live site.

### Managing redirects on your site

Open your site's **Settings**, under **General** in the site sidebar, then click **Redirects**.

#### Creating redirects

Click **Add redirect** → **Manual**. Fill in the **source path** (the URL slug to redirect) and the **destination** — any section, variant, or page on your site. Click **Enable redirect** to make it live immediately, or **Save as draft** to hold off — drafts appear in the **Draft** tab until enabled.

Add a **wildcard redirect** with `*` at the end of the source path — e.g. `/docs/*` matches everything under `/docs/`, `/changelog*` matches paths starting with `/changelog`. With a wildcard source, toggle **Replace wildcard with matched text**:

* **On** — the matched portion is appended to the destination. `/docs/*` → `/help` sends `/docs/install` to `/help/install`.
* **Off** — every matched URL redirects to the same fixed destination. `/docs/*` → `/help` sends `/docs/install` to `/help`.

Toggle **Add another redirect** before saving to keep the modal open (with the same destination pre-filled) for adding another source path quickly.

{% hint style="warning" %}
GitBook resolves published URLs case-insensitively, so two redirects differing only in capitalization are treated as the same path. If you're migrating from a platform with case-sensitive URLs, you may need to consolidate redirects before importing.
{% endhint %}

#### Editing redirects

Click the **Edit** icon next to a redirect, update it, and click **Enable redirect** to publish the change. If it's a draft, the edit modal also lets you publish it directly.

#### Enabling draft redirects

Draft redirects live in the **Draft** tab. Publish one either by opening it and clicking **Enable redirect**, or using the toggle directly in the table. Once enabled, it moves to the **Live** tab and starts routing visitors immediately.

#### Import redirects from a CSV

Click **Add redirect** → **Upload CSV**, with columns `source`, `destination`, and optional `intent`:

* `source` — the path to redirect, e.g. `/docs/site-redirects`.
* `destination` — a specific page (using its GitBook admin URL), an external URL, or empty depending on `intent`.
* `intent` — `live` (or blank/omitted) to create, update, or remove a live redirect; `draft` to create, update, or remove a draft redirect; `publish` to publish an existing draft to live (`destination` must be empty in this case).

| source | destination | intent | Result |
|---|---|---|---|
| /docs/site-redirects | https://example.com/page | blank | Create or update a live redirect |
| /docs/site-redirects | https://example.com/page | live | Create or update a live redirect |
| /docs/site-redirects | https://example.com/page | draft | Create or update a draft redirect |
| /docs/site-redirects | empty | blank | Remove the live redirect |
| /docs/site-redirects | empty | live | Remove the live redirect |
| /docs/site-redirects | empty | draft | Remove the draft redirect |
| /docs/site-redirects | empty | publish | Publish the existing draft redirect to live |

A maximum of 500 rows is supported per import. If your CSV has duplicate `source` values, only the first row processes — the import runs as an upsert, updating existing redirects with matching sources and creating new ones otherwise. If any rows fail, an error CSV is available from the bottom-right toast, with `source`, `destination`, and a short explanation per error, so you can fix and re-import.

### About automatic redirects

When pages move or get renamed, their canonical URL changes with them. To keep content accessible, GitBook automatically creates an [HTTP 307](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/307) redirect from the old URL to the new one.

Every time a URL loads, GitBook resolves it in this order:

1. Site content resolves to its canonical URL by following any automatically created redirects.
2. If unresolved, the URL is checked against [section-level redirects](../git-sync/gitbook-yaml-configuration.md#redirects) defined in your repository's `.gitbook.yaml`.
3. Finally, the URL is checked against site-level redirects created [above](#creating-redirects).

### What about broken internal links?

Broken-link detection for internal, relative links isn't a standalone feature — it isn't currently available. If a page you're linking to moves or is renamed, set up a redirect using the steps above so the old path keeps working.
