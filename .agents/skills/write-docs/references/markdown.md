# Markdown formatting

GitBook uses GitHub Flavored Markdown with custom extensions.

## Standard markdown

```markdown
# Heading 1
## Heading 2
### Heading 3

**bold text**
*italic text*
`inline code`

- Bullet list item
- Another item
  - Nested item

1. Numbered list
2. Second item

[Link text](https://example.com)
[Internal link](getting-started.md)
```

## Code blocks

````markdown
```javascript
const foo = 'bar';
console.log(foo);
```
````

**Code blocks with titles:**

````markdown
{% code title="index.js" %}
```javascript
const foo = 'bar';
console.log(foo);
```
{% endcode %}
````

## Inline links

* External links: `[text](https://example.com)`
* Internal pages: Use relative file paths like `[text](page.md)`, `[text](../folder/page.md)`, or `[text](subfolder/page.md)`
* Email: `[text](mailto:email@example.com)`

## Math/TeX

```markdown
Inline formula: $$E = mc^2$$

Block formula:

$$
E = mc^2
$$
```

## Mermaid diagrams

Any fenced code block with `mermaid` as the language renders as a diagram. Use Mermaid any time you'd otherwise reach for ASCII art or describe a relationship in prose where a picture would help.

````markdown
```mermaid
flowchart LR
    Pending --> Authorized --> Captured
    Pending -.->|declined| Failed
    Authorized -.->|voided| Voided
    Captured -.->|refund| Refunded
```

```mermaid
sequenceDiagram
    Client->>Auth: POST /token
    Auth-->>Client: access_token
```

```mermaid
stateDiagram-v2
    [*] --> Draft
    Draft --> Review
    Review --> Published
    Review --> Draft
```

```mermaid
erDiagram
    USER ||--o{ ORDER : places
    ORDER ||--|{ LINE_ITEM : contains
```
````

Common types: `flowchart LR`/`TD` (flows, decision trees), `sequenceDiagram` (request/response, multi-actor), `stateDiagram-v2` (formal state machines), `erDiagram` (data models), `gantt` (timelines). Standard Mermaid syntax — no GitBook-specific extensions.

## SVG handling

Two pitfalls affect SVGs referenced via `<img>` or `<picture>`:

* **`currentColor` doesn't resolve in referenced SVGs.** `currentColor` only works when SVG markup is inlined directly into the page. Via `<img src="...">` the SVG renders standalone and `currentColor` falls back to black regardless of theme. For theme-aware icons, either inline the SVG or ship two variants and swap with `<picture>`:

  ```html
  <picture>
    <source srcset=".gitbook/assets/icon-dark.svg" media="(prefers-color-scheme: dark)"/>
    <img src=".gitbook/assets/icon-light.svg" alt="" data-size="line"/>
  </picture>
  ```

* **Keep `xmlns` on standalone SVG files.** Some tools strip `xmlns="http://www.w3.org/2000/svg"` because it's redundant when SVG is inlined into HTML. But when the file is referenced via `<img>` or `<picture>`, a missing `xmlns` causes the browser to parse it as plain XML and render nothing. The xmlns is only safely removable when SVGs are inlined. Keep it by default.
