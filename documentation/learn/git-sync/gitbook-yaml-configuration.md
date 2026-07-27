---
description: Reference for the .gitbook.yaml configuration file.
---

# .gitbook.yaml configuration

To configure Git Sync further, add a `.gitbook.yaml` file at the root of the content synced for a section, telling GitBook how to parse your Git repository. In a monorepo, this file lives in the section's configured [Project directory](work-with-monorepos.md).

{% code title=".gitbook.yaml" %}
```yaml
root: ./

structure:
  readme: README.md
  summary: SUMMARY.md

redirects:
  previous/page: new-folder/page.md
```
{% endcode %}

### Root

The path GitBook looks up for your documentation defaults to the repository root. To point it at a `./docs` folder instead:

{% code title=".gitbook.yaml" %}
```yaml
root: ./docs/
```
{% endcode %}

{% hint style="warning" %}
All other path-based options are relative to this root folder. If you set `root` to `./docs/` and `structure.summary` to `./product/SUMMARY.md`, GitBook looks for `./docs/product/SUMMARY.md`.
{% endhint %}

{% hint style="info" %}
In a monorepo, `root` is resolved relative to the synced section's Project directory, not the repository root — path-based configuration only applies inside that section's synced scope, and doesn't expose sibling or repository-level folders to other sections automatically. See [Work with monorepos](work-with-monorepos.md).
{% endhint %}

### Structure

The `structure` key accepts two properties:

* **`readme`** — your documentation's first page. Defaults to `./README.md`.
* **`summary`** — your documentation's table of contents. Defaults to `./SUMMARY.md`.

Both values are paths relative to `root`. For example, to look in a `./product` folder for both:

{% code title=".gitbook.yaml" %}
```yaml
structure:
  readme: ./product/README.md
  summary: ./product/SUMMARY.md
```
{% endcode %}

{% hint style="warning" %}
When Git Sync is enabled, don't create or modify readme files through GitBook's UI — manage the readme exclusively in your GitHub/GitLab repository to avoid conflicts and duplication.
{% endhint %}

### Summary

The `summary` file is a Markdown file that follows this structure:

{% code title="./SUMMARY.md" %}
```markdown
# Summary

## Use headings to create page groups like this one

* [First page's title](page1/README.md)
    * [Some child page](page1/page1-1.md)
    * [Some other child page](part1/page1-2.md)

* [Second page's title](page2/README.md)
    * [Some child page](page2/page2-1.md)
    * [Some other child page](part2/page2-2.md)

## A second page group

* [Another page](another-page.md)
```
{% endcode %}

A custom summary file is optional — by default, GitBook looks for `SUMMARY.md` in your `root` folder (or the repository root if `root` isn't set). If no summary exists and GitBook can't find one, it infers the table of contents from the folder structure and Markdown files below.

{% hint style="info" %}
The summary file mirrors your section's table of contents. Even if none is provided on initial import, GitBook creates and updates one as you edit content in the GitBook editor.

Because of this, you can't reference the same Markdown file twice in `SUMMARY.md` — that would mean one page lives at two different URLs in your section.
{% endhint %}

#### Table of contents (sidebar) titles

To give a page a different title in the sidebar than on the page itself, set an optional page link title in `SUMMARY.md`:

{% code title="./SUMMARY.md" %}
```markdown
# Summary

* [Page main title](page.md "Page link title")
```
{% endcode %}

The text in quotes is used in the sidebar, in pagination buttons, and in any relative links you add to that page. It's optional — without one, GitBook uses the page's standard title everywhere.

### Redirects

The `redirects` key maps old paths to new files, so moved or renamed pages keep working:

{% code title=".gitbook.yaml" %}
```yaml
redirects:
  previous/page: new-folder/page.md
```
{% endcode %}

The YAML must be valid for redirects to work — indentation or whitespace errors can silently break them. [Validate your YAML](https://www.yamllint.com/) if a redirect isn't working. Don't add leading slashes to redirect paths (`./misc/support.md`, not `/misc/support.md`).

As long as a page exists at a given path, GitBook won't look for a redirect there — if you're redirecting an old page to a new one, remove the old page for the redirect to take effect.
