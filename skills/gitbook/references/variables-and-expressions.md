# Variables and expressions

GitBook supports variables that can be dynamically displayed in your content using expressions. Variables can be defined at the space level or page level.

## Contents

- Variable storage (space-level vs page-level)
- Using variables with expressions
- Examples
- Variable references quick chart
- Variable scope decision table

## Variable storage

### Space-level variables

Stored in `/.gitbook/vars.yaml` at the root of your documentation:

```yaml
# .gitbook/vars.yaml
food: apple
latest_version: v3.0.4
company_name: Acme Corp
```

### Page-level variables

Stored in the page's frontmatter under `vars:`:

```markdown
---
vars:
  page_food: orange
  page_version: v2.1.0
---
```

See `page-frontmatter.md` for full frontmatter details.

## Using variables with expressions

Expressions allow you to reference and display variable values dynamically in your content. Expressions use JavaScript syntax and are wrapped in `<code class="expression">` tags.

### Syntax

```markdown
<code class="expression">JavaScript expression here</code>
```

### Examples

```markdown
<!-- Simple expression -->
<code class="expression">1 + 1</code>

<!-- Reference a space-level variable -->
<code class="expression">space.vars.latest_version</code>

<!-- String concatenation with variable -->
<code class="expression">"My favorite food is " + space.vars.food</code>

<!-- Reference a page-level variable -->
<code class="expression">page.vars.page_food</code>

<!-- Conditional logic -->
<code class="expression">space.vars.latest_version === "v3.0.4" ? "Latest" : "Outdated"</code>
```

## Variable references quick chart

- `space.vars.variableName` — Access space-level variables defined in `/.gitbook/vars.yaml`
- `page.vars.variableName` — Access page-level variables defined in the page's frontmatter

## Variable scope decision table

| If variable is...          | Define it as...                      | Access with...            |
| -------------------------- | ------------------------------------ | ------------------------- |
| Used across multiple pages | Space-level in `/.gitbook/vars.yaml` | `space.vars.variableName` |
| Specific to one page       | Page-level in frontmatter `vars:`    | `page.vars.variableName`  |

## Notes

- Variable definitions (the actual variable storage) are managed through `/.gitbook/vars.yaml` for space-level variables, or page frontmatter `vars:` for page-level variables.
- Expressions can contain any valid JavaScript code and are evaluated when the page is rendered.
- When editing locally, you can create space variables by editing `/.gitbook/vars.yaml` and page variables by adding them to frontmatter.
- The GitBook UI provides a visual editor for managing variables, but they are fully editable in markdown files.
