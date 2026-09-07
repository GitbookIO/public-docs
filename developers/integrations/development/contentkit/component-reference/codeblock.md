---
description: ContentKit code block component
---

# CodeBlock

```tsx
<codeblock content="const variable = 10" syntax="javascript" />
```

| Props             | Type                | Description          |
| ----------------- | ------------------- | -------------------- |
| `content`\*       | `string`            | Code content.        |
| `syntax`          | `string`            | Syntax highlighting. |
| `lineNumbers`     | `boolean \| number` | Shows line numbers.  |
| `buttons`         | `Array<Button>`     | Overlay buttons.     |
| `state`           | `string`            | Editable state key.  |
| `onContentChange` | `Action`            | Edit action.         |

Use `codeblock` for prompts, commands, and reusable text. ContentKit doesn't expose a dedicated `prompt` component or clipboard action. Use an overlay button with `@ui.url.open` to open a target URL.
