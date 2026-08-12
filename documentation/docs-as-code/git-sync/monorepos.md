# Monorepos

GitBook supports monorepos. A monorepo is a repository that contains more than one logical project (e.g. an iOS client and a web application).

GitBook can synchronize multiple directories from the same repository with multiple sections. When enabling Git Sync on a section, you can configure a "Project directory". It will be used to lookup the `.gitbook.yaml` file for the directory to synchronize with this section.

Example of a repository structure:

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

In this example, three sections can be created on GitBook and configured with different Project directories:

* `packages/styleguide`
* `packages/app`
* `packages/api`

The "Project directory" option at the Git Sync level differs from the [`root` option](content-configuration.md#root) in the `.gitbook.yaml` configuration file. The first is used to lookup `.gitbook.yaml` itself, then both are combined to lookup the rest of the files in the directory. If no `.gitbook.yaml` exists in the "Project directory", the synchronization will use the default configuration scoped to this directory.

### How directories and assets work in multi-section repos

Each synced section has its own **Project directory**. GitBook reads that section’s `.gitbook.yaml` from the configured Project directory. It then resolves `root`, `README.md`, `SUMMARY.md`, Markdown files, and asset paths from that section’s synced scope.

In a monorepo, each synced section is scoped to its own directory and files. A different section synced from another directory doesn’t inherit or reuse files from elsewhere in the repository automatically.

Assets follow the same rule. A repository-level `.gitbook/assets` folder isn’t shared automatically across sections if those sections use different Project directories.

If multiple sections need the same files, use one of these patterns:

* Place the assets inside each section’s directory.
* Reorganize the repository so each section’s synced scope contains the assets it references.

When you set up a new section in a monorepo, create the directory structure you want in the repository first. GitBook doesn’t infer a shared multi-section layout or create a shared asset area for you.

For more detail on how `root` is resolved inside a section’s synced scope, see [Content configuration](content-configuration.md#root).

Here’s a concrete example:

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

In this repository, `packages/docs-en` and `packages/docs-fr` are two separate synced sections. A file referenced from `packages/docs-en/.gitbook/assets/logo.png` isn’t automatically available to the section synced from `packages/docs-fr`.

## Updating the Project directory <a href="#updating" id="updating"></a>

{% hint style="info" %}
In most cases, we recommend the following step to update the Project directory:

1. Disable the existing Git Sync
2. Move the files in the Git repository to the Project directory
3. Reconfigure the Git Sync with the new Project directory
{% endhint %}

In some cases, you might have started with a typical repository synchronizing with only one section, but then decided to transition into a monorepo with multiple sections synchronizing with it; or might have to rename the Project directory.

Changing the Project directory on an existing Git Sync can have an unexpected impact on the content, the change will only be propagated during the next synchronization (edit made on GitBook or new commit in the Git repository).

GitBook expects all GitBook-related files for that section to exist inside the configured Project directory. This includes Markdown files, `README.md`, `SUMMARY.md`, and any assets used by that section.

#### **If the next operation is an import from the Git repository**:

GitBook will expect to find the pages and files in the Project directory. If the files have not already been moved into the repository’s Project directory, the result of the synchronization would be an empty section with no content.

We recommend having the next operation to be a commit moving all GitBook-related files (markdown files, README/SUMMARY, and assets) in the repository to their correct new location, in the Project directory. If assets remain outside the new Project directory, don’t expect them to resolve for that section.

**If the next operation is an export from GitBook to the Git repository**:

GitBook will generate or update new files in the new Project directory. Files synchronized with GitBook will be moved to the new Project directory (with the best attempt); it might cause side effects if other parts of your system depend on these files.
