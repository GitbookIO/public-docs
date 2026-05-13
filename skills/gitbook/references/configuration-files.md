# Configuration files

This file documents the `.gitbook.yaml` configuration file and the `.gitbook/` directory that Git-synced GitBook spaces use for assets, variables, and reusable content.

For SUMMARY.md, see `summary-md-grammar.md`. For broader repo scaffolding context, see `repo-scaffolding.md`.

## Contents

- `.gitbook.yaml` — basic structure and options
- `.gitbook.yaml` — monorepo support
- `.gitbook.yaml` — important notes
- The `.gitbook/` directory — structure
- The `.gitbook/` directory — notes and gotchas
- Working with Git Sync — sync direction, best practices

## `.gitbook.yaml` — basic structure

The `.gitbook.yaml` file configures your GitBook space. It should be placed at the root of your documentation directory (or in a subdirectory if using monorepos).

```yaml
root: ./

structure:
  readme: ./README.md
  summary: ./SUMMARY.md

redirects:
  old-page: new-page.md
  help: support.md
```

## `.gitbook.yaml` — options

- `root` — The root directory for your documentation (default: `./`)
- `structure.readme` — Path to your homepage (default: `./README.md`)
- `structure.summary` — Path to your table of contents (default: `./SUMMARY.md`)
- `redirects` — Key-value pairs mapping old URLs to new page paths

## `.gitbook.yaml` — monorepo support

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

## `.gitbook.yaml` — important notes

- Paths in `.gitbook.yaml` are relative to the `root` option
- Redirects defined here are space-specific (apply only to this space)
- For site-wide redirects across multiple spaces, use the GitBook UI instead
- When using Git Sync, manage the README file only through your repository to avoid conflicts
- `.gitbook.yaml` is **optional**. GitBook works fine on the default convention of `README.md` + `SUMMARY.md` per space. Only add a `.gitbook.yaml` when you need to override the root, define redirects, or do something else non-default.

## The `.gitbook/` directory — structure

When using Git Sync, GitBook creates a `.gitbook` directory in your repository to store assets, variables, and generated content.

```
.gitbook/
  assets/          # Uploaded images and files
  includes/        # Reusable content blocks (exported as individual .md files)
  vars.yaml        # Space-level variables
  tags.yaml        # Update-block tags (optional)
```

## The `.gitbook/` directory — notes and gotchas

- **Assets**: Images and files uploaded through the GitBook UI are stored in `.gitbook/assets/`
- **Reusable content**: Each reusable content block is exported as a separate markdown file in `.gitbook/includes/`. Reference them from pages using `{% include "/reusable-content/rc12345" %}` or by path (see `custom-blocks.md`).
- **Variables**: Space-level variables are stored in `.gitbook/vars.yaml` as key-value pairs (see `variables-and-expressions.md`).
- **Tags**: For the Updates (changelog) block, `.gitbook/tags.yaml` declares the tag slugs/labels/icons used by `{% update tags="..." %}` entries (see `custom-blocks.md`).
- **Image references in pages**: Markdown pages reference images like `![alt](../.gitbook/assets/image-name.svg)`.
- **Table of contents**: The `.gitbook/includes` folder and its files may appear in your space's table of contents. You may need to manually hide them from the TOC if this happens.
- **Location in monorepos**: In monorepos, the `.gitbook` directory is created in the root of each synced space (not necessarily the repository root).

## Working with Git Sync

When GitBook is synced with Git:

1. Changes in Git automatically update GitBook
2. Changes in GitBook automatically commit to Git
3. GitBook maintains SUMMARY.md based on UI edits
4. Merge conflicts should be resolved in Git

### Best practices

- Make structural changes (navigation) through SUMMARY.md in Git
- Make content changes either in Git or GitBook UI (be consistent)
- Review auto-generated commits from GitBook
- Use branch-based workflows for significant updates
- Test changes in a preview before merging to main

### Working with existing content (orientation)

When working with an existing GitBook space that's synced to Git, follow this workflow to understand the structure:

1. **Read SUMMARY.md first.** Shows the complete table of contents, page hierarchy, page groups, and the relative paths to each markdown file.
2. **If SUMMARY.md doesn't exist** — GitBook has inferred the structure from your directory layout. Browse the directory structure.
3. **Check .gitbook.yaml** — Where the root documentation directory is located, any custom paths for README.md or SUMMARY.md, existing redirects.
4. **Explore .gitbook/assets/** — All uploaded images and files referenced in the documentation.
5. **Check .gitbook/vars.yaml** — Space-level variables, if any.

This approach ensures you understand the existing structure before making changes, helping maintain consistency and avoid breaking internal links.
