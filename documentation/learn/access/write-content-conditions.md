---
description: Write the conditions that show or hide content based on claims.
---

# Write content conditions

Once your authentication method is set up, use the data it provides to adapt your site's content for different visitors. You can hide or show:

* [Pages](../creating-content/content-structure.md)
* Site [variants](../publishing/site-sections-and-variants/README.md)
* Site [sections](../publishing/site-sections-and-variants/README.md)
* [Header links](../customization/layout-and-navigation.md#header)
* Personalized content in [inline expressions](../creating-content/reusable-content-and-variables.md)

### The condition editor

The condition editor is where you set the conditions for showing or hiding a page, variant, or section, writing your condition as an [expression](../creating-content/reusable-content-and-variables.md) that runs against visitor data.

The data passed through your users is attached to an object called `visitor.claims`. For example, to show a page only to users in a beta program:

```javascript
visitor.claims.isBetaUser == true
```

Any visitor matching this claim (`isBetaUser` is `true`) can see the page. Anyone who doesn't match — including visitors with no claims set — can't.

The condition editor autocompletes claims and attributes seen from previous visitors, and [variables](../creating-content/reusable-content-and-variables.md) you've defined are available alongside claims. For example, you could set a variable for your product's latest version, configure a claim showing which version a visitor is using, then write an expression that only shows certain pages when a visitor is on the latest version.

Expressions are valid JavaScript — combine multiple claims with `&&` or `||` (see [logical operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#binary_logical_operators)).

### Testing your conditions

[Segments](test-with-segments.md) represent mock visitor data you can use to test conditions before publishing — for example, simulating a developer on your enterprise plan, or a signed-in user on a free plan.

### Conditional pages

Open a page's Actions menu and click **Add condition** to launch the condition editor — or launch it from the page's [options](../../resources/the-gitbook-interface.md#page-options). A page condition icon shows next to any page with a condition set.

### Conditional blocks

To add a conditional block, start a new line in the editor, type `/`, then select **Conditional content**. Click the condition badge in the top-right of the block to edit its condition through the condition editor. Not all block types are supported inside conditional blocks.

**Example:** using a URL parameter to control which block is visible:

```markdown
{% if visitor.claims.unsigned.example_attribute_A %}
This block is only visible to users **with** attribute A.
{% endif %}

{% if !visitor.claims.unsigned.example_attribute_A %}
This block is only visible to users **without** attribute A.
{% endif %}
```

### Conditional variants and sections

Open the Actions menu next to a variant or section and click **Add condition**, the same way as for a page. A condition icon shows next to any variant or section with a condition set.

### Conditional page header links

Open the Actions menu next to a header link and click **Add condition**. A condition icon shows next to any link with a condition set.

### Inline expressions

Beyond controlling visibility, use claims inline with [expressions](../creating-content/reusable-content-and-variables.md), just like page and space variables. Type `/` in the editor, select **Expression**, and reference claims as properties on `visitor`.

### Working with Git Sync

Conditions set in GitBook sync through Git Sync and appear in the synced Markdown pages — blocks and pages with visibility conditions stay visible in your synced repo. Data passed through claims is never visible in Markdown, and is securely passed to GitBook directly.
