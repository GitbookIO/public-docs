---
icon: repeat
---

# Overview

{% hint style="info" %}
This feature is available as part of the Pro plan and Enterprise plan. To find out more, [visit our pricing page](https://www.gitbook.com/pricing).
{% endhint %}

Reusable content lets you sync content across multiple pages in a GitBook space, so you can edit all instances of the block at the same time.

{% hint style="warning" %}
Reusable content is currently scoped to a single space. We are working on an improvement to allow access to reusable content across your organization. Duplicating a space will not duplicate its reusable content.
{% endhint %}

### **How to create reusable content**

To create reusable content, [select one or more blocks](../content-editor/blocks/#selecting-blocks-and-interacting-with-selected-blocks), then open the **Action menu** <img src="../.gitbook/assets/Actions menu.png" alt="" data-size="line"> and choose **Turn into reusable content**. You can also give your block a name to make it easier to find and reuse later.

Alternatively, you can select one or more blocks and then hit **Cmd+C** to open a prompt asking if you want to create reusable content.

<figure><img src="../.gitbook/assets/create-reusable-block.png" alt=""><figcaption></figcaption></figure>

### **Inserting reusable content**

You can insert reusable content as you would with any other block. Hit `/` on an empty line to open the **Insert palette** and search for your content by its name or simply searching "reusable". Alternatively, click the `+` on the left of any block or empty line.&#x20;

You can choose the content you want to add from the list, or search for the one you need.

You will also find the reusable content panel in the pages sidebar, where you can find a list of previously created content blocks.

### **Editing reusable content**

Reusable content is like any other content - you can edit it directly or through change requests. Your edits will be synced everywhere the content is used.

If you're making changes inside a change request, the content will be synced everywhere once that change request is merged.

### **Detach reusable content**

You can detach reusable content by opening the **Action menu** <img src="../.gitbook/assets/Actions menu.png" alt="" data-size="line"> and selecting **Detach**. Detaching will convert the content back to regular blocks.

Once detached, any changes you make to the block(s) will not be reflected across the other instances, and changes you make in those instances will not be reflected in the detached block(s). Other instances of the reusable content remain synced together.

### Delete reusable content

You can delete reusable content from the page's table of contents. Select the **Action menu** <img src="../.gitbook/assets/Actions menu.png" alt="" data-size="line"> next to the content you’d like to delete, and select **Delete**.

Deleting reusable content will **delete it from all pages it is used in**. This action cannot be undone.

<figure><img src="../.gitbook/assets/rename-reusable-block.png" alt=""><figcaption></figcaption></figure>

## Reusable content and syncing with GitHub & GitLab

Reusable content is fully supported when syncing to GitHub & GitLab. Your reusable content will be exported to a dedicated `includes` folder, each content being a separate Markdown file.

Your content is then referenced in your other pages using the `include` directive.

