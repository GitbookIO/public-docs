---
description: Configure Git Sync through code
---

# Content configuration

Git Sync uses three files. Choose the file that controls the part of Git Sync you need:

* `docs.yaml` configures the site and maps spaces to repository directories.
* `.gitbook.yaml` configures how GitBook reads one space’s content.
* `SUMMARY.md` defines a space’s navigation.

### Configure the site with docs.yaml

`docs.yaml` configures the entire site. It lives in the Git Sync Project directory. GitBook uses the repository root when you don't set a **Project directory**.

Use `docs.yaml` to define your site structure and map each space to a directory. Each item in `site.structure` has a stable `key`. A space’s `content.directory` sets its repository directory.

#### Keys identify your spaces

Git Sync recognizes each space and section by its `key`, not by its title, path, or directory. The key is how GitBook matches an entry in `docs.yaml` to existing content from one sync to the next.

{% hint style="danger" %}
**Changing a space’s `key` destroys that space.** GitBook treats the old key as removed and the new key as a new space. It deletes the original space and creates an empty one with a new space ID. Links, cards, and API calls that reference the old space ID return 404.
{% endhint %}

Keys are safe to choose freely when you first create an entry, and GitBook generates them for you when it saves the site content mapping. Once a space is live, treat its key as permanent:

* To rename a space, change its `title`. The key stays the same.
* To change a space’s URL, change its `path`. The key stays the same.
* To move a space’s content to another directory, change its `content.directory`. The key stays the same. See [Move a mapped directory](monorepos.md#move-a-mapped-directory).

Changing `content.directory` on its own doesn’t affect the space. GitBook keeps the space and reads its content from the new location.

This example maps English and French spaces to separate directories:

{% code title="docs.yaml" expandable="true" %}
```yaml
$schema: https://api.gitbook.com/openapi.yaml#/components/schemas/GitSyncSiteConfig
site:
  title: Documentation
  structure:
    - type: section
      key: documentation
      title: Documentation
      path: documentation
      children:
        - type: space
          key: docs-en
          title: English
          path: docs
          default: true
          content:
            directory: ./docs/en
            language: en
        - type: space
          key: docs-fr
          title: Français
          path: fr
          content:
            directory: ./docs/fr
            language: fr
```
{% endcode %}

<details>

<summary>Configure additional site properties</summary>

Use these optional properties to refine your site structure:

| Property               | Use it for                                                |
| ---------------------- | --------------------------------------------------------- |
| `type: section-group`  | Group related sections under a shared navigation heading. |
| `description`          | Add a description to a section.                           |
| `icon`                 | Add an icon to a section or section group.                |
| `localizedTitle`       | Translate a section, section group, or space title.       |
| `localizedDescription` | Translate a section description.                          |
| `hidden`               | Hide a space from site navigation.                        |

GitBook creates or updates `docs.yaml` when it saves the site content mapping.

</details>

### Configure a space with .gitbook.yaml

`.gitbook.yaml` configures one space. It lives in that space’s mapped directory. Use it to set the content root, first page, navigation file, and redirects.

The main settings are:

* `root` sets the directory GitBook reads. It defaults to `./`.
* `structure.readme` sets the first page. It defaults to `README.md`.
* `structure.summary` sets the navigation file. It defaults to `SUMMARY.md`.
* `redirects` maps old paths to new paths within the space.

Here is a typical configuration:

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

#### Set the content root

Set `root` when a space’s content lives inside a subdirectory:

{% code title=".gitbook.yaml" %}
```yaml
root: ./docs/
```
{% endcode %}

{% hint style="warning" %}
Paths in `.gitbook.yaml` are relative to `root`. With `root: ./docs/`, `structure.summary: ./product/SUMMARY.md` resolves to `./docs/product/SUMMARY.md`.
{% endhint %}

In a monorepo, `root` only applies inside the mapped space directory. It doesn’t make sibling directories available. For multi-space repository setups, see [Monorepos](monorepos.md).

#### Set the first page and navigation file

Use `structure.readme` and `structure.summary` to set custom file paths:

{% code title=".gitbook.yaml" %}
```yaml
structure:
  readme: ./product/README.md
  summary: ./product/SUMMARY.md
```
{% endcode %}

{% hint style="warning" %}
When Git Sync is enabled, manage `README.md` files in your repository. Editing them in GitBook can create conflicts or duplicate pages.
{% endhint %}

#### Configure redirects

Configure space-level redirects in `.gitbook.yaml`. Redirect paths only apply within that space.

You can also manage site-level redirects in the GitBook app. See [Site redirects](../../publish/site-redirects.md).

### Configure navigation with SUMMARY.md

`SUMMARY.md` defines a space’s table of contents. GitBook looks for it in the configured `root` directory.

If GitBook doesn't find `SUMMARY.md`, it infers navigation from your folders and Markdown files. GitBook creates or updates `SUMMARY.md` when you change navigation in GitBook.

Use headings for page groups and nested links for child pages:

{% code title="SUMMARY.md" %}
```markdown
# Summary

## Product

* [Overview](README.md)
  * [Getting started](getting-started.md)
  * [Configuration](configuration.md)

## Reference

* [API reference](api.md)
```
{% endcode %}

Each Markdown file can appear once in `SUMMARY.md`. A page can only have one URL in a space.

#### Set navigation labels

Add a page link title when the navigation label differs from the page title:

{% code title="SUMMARY.md" %}
```markdown
# Summary

* [Page main title](page.md "Navigation label")
```
{% endcode %}

GitBook uses the page link title in the sidebar, pagination, and relative links. Without one, GitBook uses the page title.
