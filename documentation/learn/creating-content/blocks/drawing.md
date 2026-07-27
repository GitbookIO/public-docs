---
description: "The Drawing block: what it does and how to use it."
---

# Drawing

Create a drawing or sketch directly in GitBook using the integrated [Excalidraw](https://excalidraw.com/) editor.

Press `/` on an empty line to open the insert palette and choose **Drawing** — this opens an Excalidraw popover. Close it when you're done, and your diagram appears on the page.

GitBook stores drawings as SVG files in the section, with a `drawing.svg` extension.

### Draw with GitBook AI

{% hint style="info" %}
Available on Premium and Ultimate plans.
{% endhint %}

In a drawing block, type a prompt and click **Generate** — or pick a suggested prompt — to have GitBook AI generate an illustration. Double-click the result to open the full drawing palette and edit it however you like. While editing, click **Use AI to generate** to bring the prompt editor back up and generate a new drawing.

### Representation in Markdown

```markdown
<img src="https://example.com/file.svg" alt="Example diagram description" class="gitbook-drawing">
```
