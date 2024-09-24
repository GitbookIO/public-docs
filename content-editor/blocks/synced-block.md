---
description: >-
  Turn a set of blocks into a single reusable block that you can add to multiple
  pages and update all at once
hidden: true
---

# Synced Block

Synced blocks let you sync content across multiple pages in GitBook, so you can edit all the instances of the block at the same time.

### **How to create a synced block**

To create a synced block, [select one or more blocks](./#selecting-blocks-and-interacting-with-selected-blocks), then open the **Action menu** <img src="../../.gitbook/assets/Actions menu.png" alt="" data-size="line"> and choose **Turn into a synced block**. You can then give your synced block a name to make it easier to find and reuse later.

If your synced block has instances on other pages, you can click the drop-down menu in the top-right corner of a synced block to see those locations.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FNkEGS7hzeqa35sMXQZ4X%2Fuploads%2FjDTSw2VfScUwXuPa0iZb%2Fimage.png?alt=media&#x26;token=45680b8c-213e-4112-a3d1-a177110334f4" alt=""><figcaption></figcaption></figure>

### **How insert a synced block**

You can insert a synced block as you would with any other block. You can hit `/` on an empty line to open the **Insert palette** and choose **Synced block**. Alternatively, click the **+** on the left of any block or empty line.&#x20;

You can choose the synced block you want to add from the list, or search for the one you need.

### **Editing a synced block**

You can edit a synced block from any instance your synced block appears by selecting the block and clicking **Edit**.

{% hint style="warning" %}
Changes you make to synced blocks that appear in published content will **automatically update in the published site**. Keep this in mind as you update synced blocks across your instances.
{% endhint %}

#### **In unpublished spaces**

Edits you make to a synced block in unpublished space will go live across its instances when you click **Done**. A modal will appear asking for confirmation of your changes before they updates appear.

#### **In change requests**

Editing a synced block inside of a change request will not update any of its instances until the change request is merged.&#x20;

### **Detach a synced block**

You can detach a synced block by opening the **Action menu** <img src="../../.gitbook/assets/Actions menu.png" alt="" data-size="line"> and selecting **Detach instance**. Detaching an instance of a synced block will only detach it in the current page.

Once detached, any changes you make to the block(s) will not be reflected across the other instances, and changes you make in those instances will not be reflected in the detached block(s).

{% hint style="info" %}
**Note:** Right now, there is no way to completely remove a synced block from the list of synced blocks — we’re working on this improvement and will have something to share soon.
{% endhint %}
