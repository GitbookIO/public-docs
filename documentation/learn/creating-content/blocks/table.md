---
description: "The Table block: what it does and how to use it."
---

# Table

Add tables to organize information on a page.

### Table block options

Open the block's Options menu for:

* **Table/Cards** — switch between displaying the same data as a table or as [cards](cards.md).
* **Add column** — add one to the right; choose its type, or click **Add column** for a plain text column.
* **Insert row** — add a new row at the bottom.
* **Show header** — toggle the top title row.
* **Freeze header** — keep the top row visible while scrolling, useful for tall tables.
* **Freeze first column** — keep the leftmost column visible while scrolling horizontally, useful for wide tables.
* **Reset column sizing** — reset all columns back to equal widths.
* **Visible columns** — choose which columns are shown or hidden.
* **Delete** — deletes the table and its content.

### Column types

Set a data type per column to add formatting, embellishments, or restrictions to every cell:

* **Text** — standard text with formatting support.
* **Number** — with or without floating digits.
* **Checkbox** — checkable on each row.
* **Select** — single- or multi-choice from options you define via **Column options → Manage options**.
* **Users** — a member's name and avatar, single- or multi-choice.
* **Files** — references a file in the section, uploadable from the cell.
* **Rating** — a star rating, with a configurable max via **Column options → Max**.

Change a column's type from the **Column options** menu — you'll be asked to confirm, since data can be deleted or broken by the change.

### Resizing columns

Hover a column's edge and drag — a pixel count appears above the cursor to help you match sizes. GitBook stores column sizes as a percentage of the overall width.

### Scrolling tables

Tables wider than the editor scroll horizontally.

### Column and row options

**Columns** — drag the handle at the top of a column to reorder it. Add a new column via the **+** on the table's right edge. The **Column options** menu also toggles automatic sizing, adds a column to the right, hides, or deletes the column.

**Rows** — hover a row and click its options button for: **Open row** (view/edit all its data in a modal, including hidden columns), **Insert above/below**, **Add column**, or **Delete row**.

### Images in tables

Click into a cell and hit `/` to insert an image — not supported in the header row.

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

Not currently. To keep documents easy to write, reliable to render, and accessible, GitBook keeps tables flat — a table nested inside a cell becomes difficult to edit, resize, or navigate consistently, and introduces complexity that can break clean semantics and features like Git Sync.

</details>
