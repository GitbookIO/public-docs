---
description: Keep information organized and make documenting data easier with tables
---

# Tables

You can add tables to better organize your information in a GitBook page.

<table data-full-width="false"><thead><tr><th>Company</th><th>Status<select><option value="36bef47f343d4588bc43db3e5c701796" label="In progress" color="blue"></option></select></th><th>Contact</th><th>MRR</th><th data-hidden>Contact</th><th data-hidden>MRR</th><th data-hidden>Status<select><option value="3e7a52c673ec4a01992566d18271f7a5" label="In progress" color="blue"></option><option value="2362fd3eafc7476fb8646ac754f34b72" label="Done" color="blue"></option></select></th></tr></thead><tbody><tr><td><strong>Ace AI</strong> – Design</td><td><span data-option="36bef47f343d4588bc43db3e5c701796">In progress</span></td><td><a href="mailto:noreply@gitbook.com">rena@ace.ai</a></td><td>$450</td><td><a href="mailto:noreply@gitbook.com">rena@ace.ai</a></td><td>$420</td><td><span data-option="3e7a52c673ec4a01992566d18271f7a5">In progress</span></td></tr><tr><td><strong>Discrete Data</strong> – API</td><td></td><td><a href="mailto:noreply@gitbook.com">dave@dd.inc</a></td><td>$100</td><td><a href="mailto:noreply@gitbook.com">dave@dd.inc</a></td><td>$69</td><td></td></tr></tbody></table>

### Table block options

When you open the Options menu to the left of a table block, you’ll have a number of options to change the appearance and manage the data inside the table:

* **Table/Cards:** Choose to display your data as either a table block or [a cards block](cards.md). GitBook populates both these blocks using the same data, so you can switch between them depending on the look and design you want.
* **Add column:** Add a new column to the right of your table. You can choose column type using the menu, or just click **Add column** to add a text column.
* **Insert row:** Add a new row to the bottom of your table.
* **Show header:** Hide or show the top totle row of your table. Depending on the data you’re display, you may not need a title row in your table, so you can disable it here.
* **Reset column sizing:** If you’ve changed the column widths, this will reset them all to be equal again.
* **Visible columns:** Choose which columns are visible and which are hidden. If you have hidden columns in your table, this menu is where you can make them visible again.
* **Full width:** Make your table span the full width of your window. This is great for tables with lots of columns.
* **Delete:** Deletes the table block and all of it’s content.

### Changing a column type

Depending on the data you want to display, you can set table columns can have different data types. These add formatting, embellishments or restrictions to every cell in the column:

* **Text:** A standard text column, with standard formatting support.
* **Number:** A number column, with or without floating digits.
* **Checkbox:** A checkbox on each line that can be checked or unchecked.
* **Select:** You can select data from a list of options that you can define by opening the **Columns options** menu and choosing **Manage options**. This can be single-choice or multiple-choice.
* **Users:** You can add the name and avatar of a member of your organization. This can be single-choice or multiple-choice.
* **Files:** You can reference a file in the space. You can upload new files when populating cells in the column.
* **Rating:** A star rating. You can configure the maximum rating by opening the **Column options** menu and choosing **Max**.

Use the **Column options** menu to change a column’s type. When you change a column type, you’ll see a prompt asking you to confirm the change, as column data could be deleted or broken by this action.

### Resizing columns

Hover over a column’s edge and drag to resize it. A pixel count appears above the cursor to help you set consistent column sizes.

GitBook stores column sizes as a percentage of the overall width, which allows for relative sizing based on the overall width of the table.

### Scrolling tables

Tables that are wider than the editor container will be horizontally scrollable.

### Column options

To reorder columns, click and drag on the drag handle <picture><source srcset="../../.gitbook/assets/actions-horizontal - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions-horizontal.svg" alt="The table drag handle icon in GitBook"></picture> at the top of the column you want to move.

You can add new columns by clicking the **Add column** button that appears when you hover over the right edge of the table.

Inside the **Column options** menu you can also switch automatic sizing on and off, add a new column to the right, hide the column, or delete the column.

### Row options

Hover over the row and click the **Row options** <picture><source srcset="../../.gitbook/assets/actions_icon_dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/actions_icon_light.svg" alt="The Row options menu icon in GitBook"></picture> button that appears on the left of it to open the **Row options** menu. You’ll see a number of options:

* **Open row:** Open the row in a modal that shows all of its data. Here you can quickly change row types, edit data, and see data in hidden columns.
* **Insert above/below:** Add a new row above or below the currently-selected row.
* **Add column:** Add a new column on the right of the table.
* **Delete row:** Permanently remove all the data in the row from your table.

### Images in tables

When you click into a table cell, you can hit the / key to insert images. Images cannot be added to the header row of a table.

### Representation in Markdown

```markdown
# Table

|   |   |   |
| - | - | - |
|   |   |   |
|   |   |   |
|   |   |   |
```

<details>

<summary>Can I create nested tables in GitBook?</summary>

It's not possible to nest tables in GitBook. To ensure documents remain easy to write, reliable to render, and accessible for all users, GitBook keeps tables flat.

Once a table sits inside another table cell, it becomes difficult to edit, resize, navigate, or maintain consistent formatting across devices.

Nested tables also introduce significant complexity in the underlying document structure, often breaking clean semantics and leading to unpredictability in features such as Git Sync.

</details>
