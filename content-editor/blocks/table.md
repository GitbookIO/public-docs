---
description: Add a table to a page
---

# Tables

You can add tables to better organize your information.

<table data-full-width="false"><thead><tr><th>Company</th><th data-type="select">Status</th><th>Contact</th><th>MRR</th></tr></thead><tbody><tr><td><strong>Ace AI</strong> – Design</td><td></td><td><a href="mailto:noreply@gitbook.com">rena@ace.ai</a></td><td>$420</td></tr><tr><td><strong>Discrete Data</strong> – API</td><td></td><td><a href="mailto:noreply@gitbook.com">dave@dd.inc</a></td><td>$69</td></tr></tbody></table>

Table columns can have the following data types, which apply restrictions or embellishments to every cell in the column:

- **Text**: standard text. Can be formatted.
- **Number:** a number, with or without floating digits.
- **Checkbox:** a checkbox that can be checked or unchecked.
- **Select:** data can be selected from a pre-defined list of options. Can be single-choice or multiple-choice.
- **Users:** data can be selected from a list of the organization’s members. Can be single-choice or multiple-choice.
- **Files:** data is a reference to a file in the space. New files can be uploaded when populating cells in the column.
- **Rating:** A star rating, with a configurable maximum.

### Changing a column type

You can use the column dropdown menu to change a column’s type. Select the new type and click **save**. You’ll be prompted to confirm this change, as column data could be deleted or malformed by this action.

### Resizing columns

You can drag from a column’s edge to resize it. Column resizing is stored as a percentage of the overall width, which allows for relative sizing based on the overall width of the table.

### Scrolling tables

Tables that are wider than the editor container will be horizontally scrollable.

{% hint style="info" %}
You can drag and drop columns and rows to reorder them, and delete columns or rows using their respective context menus.
{% endhint %}

### Representation in Markdown

```
# Table

|   |   |   |
| - | - | - |
|   |   |   |
|   |   |   |
|   |   |   |
```
