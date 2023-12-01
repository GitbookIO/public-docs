---
description: Add a file to a page
---

# Files

You can upload file assets to your GitBook space and include them in your spaces for download.

### Example of file

{% file src="../../.gitbook/assets/hello-world.pdf" %}
Hello world
{% endfile %}

## Uploading a file

Files are managed in the files panel of your space. To access the files panel, click on files in the [space sub-navigation](https://docs.gitbook.com/getting-started/overview#space-sub-navigation).

To upload a file, select **browse files** and use your system file dialog to select the file you want to upload.

{% hint style="warning" %}
**GitBook allows to upload up to 100MB per file.**
{% endhint %}

Files can also be uploaded as part of the [image block](insert-images.md) setup flow, and the [OpenAPI block](openapi.md) setup flow. Upon creation, each of these blocks will open the files panel and have you either select or upload a new file.

{% hint style="info" %}
You can drag images from your file system directly into the editor, or paste a copied image into your content, and they will also appear in the files menu for the respective space.
{% endhint %}

## Managing files

You can search for, rename, or delete files in your space in the files panel of your space. Below the file upload section, you’ll find the file listing. Each file has an action menu that lets you download, replace, rename, or delete your file. At the top of the file listing section, there is a search box, where you can search for your file by its name, and a sort toggle, which will let you sort your files by the date they were last modified, or their size.

<figure><img src="../../.gitbook/assets/file-menu.png" alt="A screenshot of a GitBook space with the files panel open. The triple dot icon to the right side of a file has been clicked on to reveal a menu with the following options: download, replace, edit, and delete."><figcaption><p>Upload, filter, download, replace, edit, and delete files.</p></figcaption></figure>

### Renaming a file

To rename a file, open the action menu for the file, and click **edit**. In the dialog prompt, enter the new name of your file.

### Deleting a file

To delete a file, open the action menu for the file and click **delete**. After confirming in the dialog that you’re sure you want to delete the file, your file will be deleted. Be sure to update your documents that referred to your now deleted file! Otherwise, you may end up with some empty blocks.

### Replacing a file

GitBook supports replacing an existing file. This will swap out the old file and put the new file in its place. Any blocks that previously referred to the old file will now refer to the new file after replacement.

This can be helpful if you have, for example, a screenshot of your UI used throughout your space and want to change it in every case after a major product redesign. Replacing the file would cause it to be replaced everywhere it is used in the space, so you don’t have to manually update each instance of the screenshot.

{% hint style="info" %}
Once you’ve uploaded an image or a file, you can reference it anywhere in your space by using an image or a file block. It’s recommended you do this rather than dragging and dropping or pasting an image into the editor every time you want to include it.
{% endhint %}

To replace a file, open the action menu for the file and click **replace**. You’ll be presented with a file replacement dialog. Select the new file, and wait for the upload indicator to complete. Your new file will be displayed wherever your previous one was.

### Related

If you are looking to embed external content into your pages, take a look at how to [embed a URL](embed-a-url.md).
