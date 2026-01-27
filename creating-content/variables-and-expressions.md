---
description: Create reusable variables that can be referenced in pages and spaces
icon: icons
---

# Variables and expressions

With variables you can create reusable text that can be conditionally referenced in [expressions](formatting/inline.md#expressions) and [conditions for adaptive content](../publishing-documentation/adaptive-content/adapting-your-content.md#working-with-the-condition-editor).

If you repeat the same name, phrase or version number multiple times within your content, you can create a **variable** to help keep all those instances in sync and accurate — which is useful if you ever need to update them, or they’re complex and often mistyped.

You can create variables that are scoped to a single page, or a single space.

### Create a new variable

To create a new variable, click the **Library** in your Table of Contents when editing an open [change request](../collaboration/change-requests/). Then, click **Variables**.

You can use the toggle at the top to view and create variables scoped either to the current page you’re on, or all pages within the current space.

Clicking **Create a variable** will launch a modal where you can give your variable a name and a value.

Click **Add variable** to save your variable.

<figure><img src="../.gitbook/assets/25_12_10_add_variable@2x.png" alt="A GitBook screenshot showing the Add variables screen. The variable Name box has been filled with the text ‘latest_version’ and the Value box has been filled with the text ‘v3.04.1’"><figcaption><p>You can add variables to a single page or an entire space. When you update the value of a variable, every instance of it will update.</p></figcaption></figure>

{% hint style="info" %}
Variable names must start with a letter, and can contain letters, numbers and underscores.
{% endhint %}

### Use variables in your content

Variables can be referenced and used within an [expression](formatting/inline.md#expressions) — which you can insert into your content inline. After inserting an expression, double click it to open the expression editor.

Variables defined under your page are accessible under the `page.vars` object. Similarly, variables defined across your entire space are accessible under the `space.vars` object.

<figure><img src="../.gitbook/assets/25_12_10_add_variable@2x_1.png" alt="A GitBook screenshot showing an expression block within the editor. The expression editor is open below it and the ‘space.vars.latest_version’ variable has been selected"><figcaption><p>You can add variables to your content within expresions. The expression editor offers autocomplete options to help you find the variable you need.</p></figcaption></figure>

### Update a variable

You can update a variable at any point when within a change request. Updating its value will update the value across any expression blocks referencing it. The changed variable will go live to any published site once the change request is merged.
