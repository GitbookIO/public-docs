# Cross-space links

Cross-space links are the connective tissue of a multi-space GitBook site — they're how the API reference points back to conceptual guides, how the changelog references the migration tutorial, how a card-table on the home page surfaces deep links into product docs. Without them, a multi-space site reads as a stack of disconnected manuals.

This reference covers: the URL pattern, the sentinel-and-resolve workflow for scaffolding, all the variants (space root, page, anchor, file), and a working resolution script.

## The URL pattern

Every cross-space link in markdown is a regular link to a `https://app.gitbook.com/s/<spaceId>/<path>` URL. GitBook's renderer resolves these at runtime — visitors land on the appropriate published URL whether the site is on a `*.gitbook.io` subdomain, a custom domain, or share-link visibility.

```markdown
[The whole space](https://app.gitbook.com/s/<spaceId>/)
[A specific page](https://app.gitbook.com/s/<spaceId>/concepts/authentication)
[A page with anchor](https://app.gitbook.com/s/<spaceId>/concepts/authentication#rotation)
```

The path after the space ID is the page's path inside the space, derived from the file structure (folder names + file slugs). Trailing slash works for the space root.

You'll also see a fully-qualified form in some content: `https://app.gitbook.com/o/<orgId>/s/<spaceId>/...`. Both work; the org-qualified form is slightly more robust against potential future URL changes but the shorter form is what GitBook itself emits in most places.

## When to use this vs. relative links

- **Within a space** — use plain relative paths: `[Quickstart](quickstart.md)`, `[Concepts](../concepts/data-model.md)`. These resolve at the markdown level, no IDs needed.
- **Across spaces** — use the `app.gitbook.com/s/<spaceId>/...` form. Relative paths can't cross space boundaries.
- **External URLs** — just the URL: `[Status](https://status.example.com)`.

## The sentinel-and-resolve workflow

### Step 1 — agree on space keys during the structure plan

Each space in the plan gets a stable key — short, uppercase, descriptive. Use the same key everywhere:

```
guides     → XSPACE_GUIDES
api-reference → XSPACE_API
changelog  → XSPACE_CHANGELOG
```

These keys are *internal to the scaffolding step* and disappear once resolution runs.

### Step 2 — write cross-space links in markdown using sentinels

Anywhere a link crosses spaces:

```markdown
For the operational details — exact error codes, rate limits, header format — see
[Authentication in the API reference](https://app.gitbook.com/s/XSPACE_API/authentication).

Need a model of the data?
[Data model](https://app.gitbook.com/s/XSPACE_GUIDES/concepts/data-model) covers it.
```

The sentinels are valid URLs to non-existent spaces. Markdown parsers don't care, Git tracks them cleanly, and they grep with no false positives.

### Step 3 — after space creation, get real IDs and resolve

The API returns each space's `id` in the `POST /v1/orgs/{orgId}/spaces` response. Build a mapping and apply it:

```bash
# After space creation, you have a mapping like:
declare -A SPACE_IDS=(
  [XSPACE_GUIDES]="V2euUoapjerbu1hCxVIv"
  [XSPACE_API]="Si95BtOt1VRLWjT7A67V"
  [XSPACE_CHANGELOG]="ErQsbFsgm6eg9BApdmPl"
)

# Apply substitutions across all markdown
for key in "${!SPACE_IDS[@]}"; do
  find . -name '*.md' -not -path './.git/*' -print0 \
    | xargs -0 sed -i "s|${key}|${SPACE_IDS[$key]}|g"
done

git add -u
git commit -m "Resolve cross-space link IDs"
git push
```

### Step 4 — keep a record

Before discarding the mapping, dump it to `cross-space-links.yaml` in the repo root:

```yaml
# Maps sentinel keys to GitBook space IDs.
# Used during initial scaffold to resolve XSPACE_<KEY> placeholders to real
# https://app.gitbook.com/s/<id>/ URLs across the markdown.
# After resolution there are no XSPACE_ placeholders left in the repo, but
# this file stays as a record of which key meant which space.
spaces:
  XSPACE_GUIDES:    V2euUoapjerbu1hCxVIv
  XSPACE_API:       Si95BtOt1VRLWjT7A67V
  XSPACE_CHANGELOG: ErQsbFsgm6eg9BApdmPl
```

This makes the substitution reproducible if you ever need to add a new space later (you'd add a new `XSPACE_<NEW>` row to the mapping and re-run the resolver across files that reference it).

## Variants

### Link to a specific page in another space

The path after the space ID matches the file path inside that space, with `.md` dropped:

```markdown
[Webhooks reference](https://app.gitbook.com/s/XSPACE_API/webhooks)
[Verifying signatures](https://app.gitbook.com/s/XSPACE_API/webhooks/verifying-signatures)
```

### Link with an anchor (deep link to a heading)

Append `#<heading-slug>` like a regular markdown anchor:

```markdown
[Rate limit headers](https://app.gitbook.com/s/XSPACE_API/authentication#rate-limits)
```

GitBook generates heading slugs from heading text (lowercase, hyphenated). Confirm with the rendered page if a heading has unusual characters.

### Link to the space root (homepage)

Trailing slash, nothing else:

```markdown
[Open the API reference](https://app.gitbook.com/s/XSPACE_API/)
```

### Buttons, card-tables, and other rich blocks

Card-tables and inline buttons use the same URL pattern in their `href` attributes:

```html
<a href="https://app.gitbook.com/s/XSPACE_API/" class="button primary">API Reference</a>
```

Tables with `data-view="cards"` and a `content-ref` column accept the same URL in the column value.

### In SUMMARY.md

Cross-space links work in `SUMMARY.md` too — useful for cross-referencing related spaces from the table of contents itself. The same URL pattern applies, with **no `.md` suffix** on the target path:

```markdown
# Table of contents

* [Guides homepage](README.md)
* [Quickstart](getting-started/quickstart.md)
* [Concepts](concepts/README.md)

## See also

* [API Reference](https://app.gitbook.com/s/XSPACE_API/)
* [Changelog](https://app.gitbook.com/s/XSPACE_CHANGELOG/)
```

These render as outbound nav entries that route to the appropriate space. Resolution works the same way as for body content — the sentinel `XSPACE_<KEY>` gets replaced with the real space ID after creation. The resolver script in this file walks `*.md` files indiscriminately, so SUMMARY.md links are picked up automatically.

## When the substitution should be programmatic vs. manual

For 1–3 spaces with maybe a dozen cross-space links total, sed is fine. For larger sites with hundreds of cross-space links, write a small Python script:

```python
import re
import yaml
from pathlib import Path

mapping = yaml.safe_load(Path("cross-space-links.yaml").read_text())["spaces"]

for md in Path(".").rglob("*.md"):
    if ".git" in md.parts:
        continue
    text = md.read_text()
    new = text
    for key, space_id in mapping.items():
        new = new.replace(key, space_id)
    if new != text:
        md.write_text(new)
        print(f"Resolved: {md}")
```

The script is idempotent — running it twice doesn't break anything, since after the first run there are no XSPACE_ placeholders left to substitute.

## Common mistakes

- **Don't try to guess space IDs ahead of time.** They come from the API response after `POST /spaces`. Even a stable-looking ID format is opaque.
- **Don't use `<published-domain>/...` URLs across spaces** unless you've actually configured that domain. Sites without a custom domain live at `<orghostname>.gitbook.io/<sitehostname>/<sectionpath>/<spacepath>/<page>`, and that URL changes if anyone moves the site or section.
- **Don't strip the sentinel prefix from `XSPACE_<KEY>`.** Keep the `XSPACE_` prefix in case some future content has unrelated IDs that happen to match a key like `GUIDES`.
- **Don't forget to commit and push** after resolution — Git Sync needs the resolved content to render the links correctly.
- **Don't paraphrase to avoid a cross-space link.** A docs site that says "see the API reference" without linking is a worse docs site than one that links cleanly. Use the sentinel pattern and resolve.

## A note on what `write-gitbook` should know

The companion skill `write-gitbook` covers the markdown syntax for links in general. It should be aware that **cross-space links require resolved space IDs and won't work as relative paths**, and should produce them using the sentinel pattern when generating content for a multi-space site. The actual sentinel→ID resolution belongs to this skill (`manage-gitbook-site`), since this skill is the one with API access to fetch the IDs after space creation.

If `write-gitbook` is being used standalone (without `manage-gitbook-site` orchestrating), the user is responsible for replacing the sentinels themselves once they know the space IDs.
