# Conditional content

Conditional content blocks let you control who can see a given block of content on your page based on user data and variables. These variables can be passed in via cookies, feature flags, authenticated access, or URL parameters.&#x20;

### Create conditional content

To add a conditional block, begin a new line in the editor, type <kbd>/</kbd>, then select  <picture><source srcset="../../.gitbook/assets/page-condition - dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/page-condition.svg" alt="The Page condition icon in GitBook"></picture> **Conditional content**.&#x20;

After inserting the block, click the red condition badge in the top right of the block.

Clicking this will allow you to add a condition through the [condition editor](../../publishing-documentation/adaptive-content/adapting-your-content.md#working-with-the-condition-editor). You’ll be able to write your condition as an [expression](https://gitbook.com/docs/creating-content/variables-and-expressions) that will run against data defined in your site. You can reference data from [variables](../variables-and-expressions.md), or data coming from visitors through their [claims](../../publishing-documentation/adaptive-content/enabling-adaptive-content/#set-your-visitor-schema).

See [adaptive content](../../publishing-documentation/adaptive-content/) for more details.

### Example

The examples below use a URL parameter linked from the button to control which conditional content block is visible.

{% if visitor.claims.unsigned.example_attribute_A %}
This block is only visible to users **with** attribute A.

<a href="https://gitbook.com/docs/creating-content/blocks/conditional-content?visitor.example_attribute_A=false" class="button primary">View without attribute A</a>
{% endif %}

{% if !visitor.claims.unsigned.example_attribute_A %}
This block is only visible to users **without** attribute A.

<a href="https://gitbook.com/docs/creating-content/blocks/conditional-content?visitor.example_attribute_A=true" class="button primary">View with attribute A</a>
{% endif %}

## Representation in Markdown

```markdown
## Example

{% if visitor.claims.unsigned.example_attribute_A %}
This block is only visible to users **with** attribute A.
<a href="https://gitbook.com/docs/creating-content/blocks/conditional-content?visitor.example_attribute_A=false" class="button primary">View without attribute A</a>
{% endif %}

{% if !visitor.claims.unsigned.example_attribute_A %}
This block is only visible to users **without** attribute A.
<a href="https://gitbook.com/docs/creating-content/blocks/conditional-content?visitor.example_attribute_A=true" class="button primary">View with attribute A</a>
{% endif %}
```
