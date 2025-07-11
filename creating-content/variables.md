---
description: Create reusable variables that can be referenced in pages and spaces.
icon: icons
---

# Variables

Variables allow you to create reusable text that can be conditionally referenced in [expression blocks](formatting/inline.md#expressions). This is useful if you need to update similarly named things across your content at the same time - like product names or versions.

You can create variables that are scoped to a single page, or a single space.

### Create a new variable

To create a new variable, head to the variables panel  in the upper right corner when editing an open [change request](../collaboration/change-requests.md).

Use the toggle at the top to create variables either scoped to the current page you’re on, or all pages within the space you’re in.

Clicking the “**+ Create a variable**” button will launch a modal, where you can give your variable a name and a value.

Click “Add variable” to save your variable.

{% hint style="info" %}
Variable names must start with a letter, and can contain letters, numbers and underscores.
{% endhint %}

### Use variables in your content

Variables can be referenced and used within an [expression block](formatting/inline.md#expressions). The expression block can be inserted inline into your content. After inserting an expression block, double click the expression block to open the expression editor.

Variables defined under your page are accessible under the `page.vars` object. Similarly, variables defined across your entire space are accessible under the `space.vars` object.

### Update a variable

You can update a variable at any point when within a change request. Updating it’s value will update the value across any expression blocks referencing it. The changed variable will go live to any published site once the change request is merged.
