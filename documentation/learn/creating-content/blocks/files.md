---
description: "The Files block: what it does and how to use it."
---

# Files

Upload files to your section and add them to a page for people to view or download. Some files (images, OpenAPI files) show inline on the page; others (like PDFs) need a click to view or download. Optionally add a caption below any file.

### Example

```
{% file src="path/to/example.pdf" %}
This is a caption on a file.
{% endfile %}
```

### Uploading a file

Manage uploaded files in the **Library** tab, beside **Pages** at the top of the table of contents. Drag and drop a file into **Drop your file or browse**, or select it via your system dialog.

{% hint style="warning" %}
GitBook allows uploads up to 100MB per file.
{% endhint %}

Files can also be added when you insert an image or OpenAPI block — the Library tab opens so you can select or upload a file.

{% hint style="info" %}
Drag and drop images directly into the editor, or paste a copied image — GitBook adds them to the section's Library automatically.
{% endhint %}

### Renaming a file

Open the file's Actions menu, click **Edit**, and enter the new name.

### Deleting a file

Open the file's Actions menu, click **Delete**, and confirm.

{% hint style="warning" %}
Update any pages that reference the deleted file — blocks referencing it will show empty, or a "Could not load" error.
{% endhint %}

### Replacing a file

Swap an old file for a new one, and every block referencing it updates automatically — useful for something like updating outdated UI screenshots used across multiple pages. Open the file's Actions menu, click **Replace**, choose the new file, and wait for the upload to complete.

{% hint style="info" %}
Reference an uploaded file wherever you need it, rather than re-uploading it each time — this makes it easier to replace later and avoids duplicate filenames.
{% endhint %}

### Representation in Markdown

```markdown
{% file src="https://example.com/example.pdf" %}
    This is a caption for the example file.
{% endfile %}
```
