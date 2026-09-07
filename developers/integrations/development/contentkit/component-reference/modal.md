---
description: ContentKit modal component
---

# Modal

```tsx
<modal>...</modal>
```

| Props         | Type                                   | Description             |
| ------------- | -------------------------------------- | ----------------------- |
| `children`\*  | `Array<Block> \| Array<Inline>`        | Modal content.          |
| `title`       | `string`                               | Modal title.            |
| `subtitle`    | `string`                               | Modal subtitle.         |
| `size`        | `'medium' \| 'xlarge' \| 'fullscreen'` | Modal size.             |
| `returnValue` | `object`                               | Data returned on close. |
| `submit`      | `Button`                               | Submit button.          |

Open it with `@ui.modal.open`, then dispatch `@ui.modal.close` from the modal. See [actions.md](../actions.md "mention").
