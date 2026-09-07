---
description: ContentKit text input component
---

# TextInput

```tsx
<textinput id="name" label="Name" initialValue="John Doe" placeholder="Enter a name" />
```

| Props          | Type     | Description        |
| -------------- | -------- | ------------------ |
| `state`\*      | `string` | Binding state key. |
| `initialValue` | `string` | Initial value.     |
| `label`        | `string` | Input label.       |
| `placeholder`  | `string` | Placeholder.       |

Use `@editor.node.updateProps` to save `element.dynamicState('content')` as a block property. Follow [create-an-interactive-text-input.md](../../../guides/create-an-interactive-text-input.md "mention") for an example.
