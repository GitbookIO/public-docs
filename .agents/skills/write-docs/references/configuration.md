# Configuration files

## .gitbook.yaml

The `.gitbook.yaml` file configures your GitBook space. It should be placed at the root of your documentation directory (or in a subdirectory if using monorepos).

**Basic structure:**

```yaml
root: ./

structure:
  readme: ./README.md
  summary: ./SUMMARY.md

redirects:
  old-page: new-page.md
  help: support.md
```

**Configuration options:**

* `root`: The root directory for your documentation (default: `./`)
* `structure.readme`: Path to your homepage (default: `./README.md`)
* `structure.summary`: Path to your table of contents (default: `./SUMMARY.md`)
* `redirects`: Key-value pairs mapping old URLs to new page paths

**Monorepo support:**

For repositories with multiple documentation projects:

```
/
  packages/
    docs/
      .gitbook.yaml
      README.md
      SUMMARY.md
    api/
      .gitbook.yaml
      README.md
      SUMMARY.md
```

When setting up Git Sync, configure the "Project directory" to point to the subdirectory containing the `.gitbook.yaml` file.

**Important notes:**

* Paths in `.gitbook.yaml` are relative to the `root` option
* Redirects defined here are space-specific (apply only to this space)
* For site-wide redirects across multiple spaces, use the GitBook UI instead
* When using Git Sync, manage the README file only through your repository to avoid conflicts

## The .gitbook Directory

When using Git Sync, GitBook creates a `.gitbook` directory in your repository to store assets, variables, and generated content.

**Directory structure:**

```
.gitbook/
  assets/          # Uploaded images and files
  includes/        # Reusable content blocks (exported as individual .md files)
  vars.yaml        # Space-level variables
  tags.yaml        # Update tags (for {% updates %} blocks)
```

**Important notes about .gitbook:**

* **Assets**: Images and files uploaded through the GitBook UI are stored in `.gitbook/assets/`
* **Reusable content**: Each reusable content block is exported as a separate markdown file in `.gitbook/includes/`
* **Variables**: Space-level variables are stored in `.gitbook/vars.yaml` as key-value pairs
* **References**: Pages reference reusable content using `{% include "/reusable-content/rc12345" %}`
* **Images**: Markdown pages reference images like `![alt](../.gitbook/assets/image-name.svg)`
* **Table of contents**: The `.gitbook/includes` folder and its files may appear in your space's table of contents. You may need to manually hide them from the TOC if this happens.
* **Location**: In monorepos, the `.gitbook` directory is created in the root of each synced space (not necessarily the repository root)

## SUMMARY.md

The `SUMMARY.md` file defines your table of contents and navigation structure. It's a markdown file with a specific format that mirrors the sidebar navigation in GitBook.

**Basic structure:**

```markdown
# Summary

## Use headings to create page groups like this one

* [First page's title](page1/README.md)
    * [Some child page](page1/page1-1.md)
    * [Some other child page](page1/page1-2.md)
* [Second page's title](page2/README.md)
    * [Some child page](page2/page2-1.md)
    * [Some other child page](page2/page2-2.md)

## A second page group

* [Another page](another-page.md)
```

**Key rules:**

* Use `#` for the main title (commonly "Table of contents" or "Summary")
* Use `##` headings to create page groups (section headers in the sidebar)
* Use `*` for unordered lists to define pages and subpages
* Indent with spaces (not tabs) to create nested/child pages
* Each list item should be a markdown link: `[Link text](path/to/file.md)`
* Paths are relative to the location specified in `.gitbook.yaml` (typically the root)

**Page link titles (optional):**

You can define a different title for the sidebar navigation versus the page itself:

```markdown
# Summary

* [Page main title](page.md "Page link title")
```

The text in quotes ("Page link title") will be used in:

* The table of contents sidebar
* Pagination buttons at the bottom of pages
* Any relative links to that page

**Important notes:**

* SUMMARY.md is optional. If not provided, GitBook infers structure from your folder hierarchy
* You cannot reference the same markdown file twice in SUMMARY.md (each page has only one URL)
* GitBook updates SUMMARY.md automatically when you edit through the GitBook UI
* The file structure reflects exactly what users see in the navigation sidebar
