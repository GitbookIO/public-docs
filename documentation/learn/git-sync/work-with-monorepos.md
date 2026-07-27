---
description: Sync multiple spaces from a single repository.
---

# Work with monorepos

GitBook supports monorepos — a repository containing more than one logical project (for example, an iOS client and a web application).

GitBook can synchronize multiple directories from the same repository with multiple sections. When enabling Git Sync on a section, configure a **Project directory** — GitBook uses it to look up the `.gitbook.yaml` file for the directory to synchronize with that section.

Example repository structure:

```
/
  package.json
  packages/
     styleguide/
        .gitbook.yaml
        README.md
        SUMMARY.md
     app/
        README.md
        SUMMARY.md
     api/
        .gitbook.yaml
        README.md
        SUMMARY.md
```

Here, three sections can be created on GitBook, each configured with a different Project directory: `packages/styleguide`, `packages/app`, `packages/api`.

The Project directory (a Git Sync setting) differs from the [`root` option](gitbook-yaml-configuration.md#root) in `.gitbook.yaml`: the Project directory is used to look up `.gitbook.yaml` itself, then both are combined to look up the rest of the files in the directory. If no `.gitbook.yaml` exists in the Project directory, sync uses the default configuration scoped to that directory.

### How directories and assets work in multi-section repos

Each synced section has its own Project directory. GitBook reads that section's `.gitbook.yaml` from the configured Project directory, then resolves `root`, `README.md`, `SUMMARY.md`, Markdown files, and asset paths from that section's synced scope.

A section synced from one directory doesn't inherit or reuse files from elsewhere in the repository automatically — this applies to assets too. A repository-level `.gitbook/assets` folder isn't shared across sections that use different Project directories.

If multiple sections need the same files, either:

* place the assets inside each section's directory, or
* reorganize the repository so each section's synced scope contains the assets it references.

When setting up a new section in a monorepo, create the directory structure you want in the repository first — GitBook doesn't infer a shared multi-section layout or create a shared asset area for you.

Concrete example:

```
/
  packages/
    docs-en/
      .gitbook.yaml
      README.md
      SUMMARY.md
      .gitbook/
        assets/
          logo.png
    docs-fr/
      .gitbook.yaml
      README.md
      SUMMARY.md
      .gitbook/
        assets/
          logo.png
```

`packages/docs-en` and `packages/docs-fr` are two separate synced sections here — a file referenced from `packages/docs-en/.gitbook/assets/logo.png` isn't automatically available to the section synced from `packages/docs-fr`.

### Updating the Project directory

{% hint style="info" %}
In most cases, we recommend:

1. Disable the existing Git Sync.
2. Move the files in the Git repository to the new Project directory.
3. Reconfigure Git Sync with the new Project directory.
{% endhint %}

You might need this if you started with a typical single-section repository and later transitioned to a monorepo with multiple synced sections, or if you're renaming the Project directory.

Changing the Project directory on an existing Git Sync can affect content unexpectedly — the change only propagates during the next sync (an edit made on GitBook, or a new commit in the repository). GitBook expects all of that section's GitBook-related files — Markdown files, `README.md`, `SUMMARY.md`, and assets — to exist inside the configured Project directory.

**If the next operation is an import from the Git repository:** GitBook expects to find the pages and files in the Project directory. If they haven't already been moved there, the sync result is an empty section with no content. We recommend making the next operation a commit that moves all GitBook-related files (Markdown, README/SUMMARY, and assets) to their correct new location first. If assets remain outside the new Project directory, they won't resolve for that section.

**If the next operation is an export from GitBook to the Git repository:** GitBook generates or updates files in the new Project directory, moving previously-synced files there on a best-effort basis. This can have side effects if other parts of your system depend on the old file locations.
