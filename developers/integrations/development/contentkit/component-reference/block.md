---
description: ContentKit block layout component
---

# Block

`block` is the top-level component:

```tsx
<block>...</block>
```

| Props                      | Type                    | Description         |
| -------------------------- | ----------------------- | ------------------- |
| `children`\*               | `Array<Block>`          | Block content.      |
| `controls`                 | `Array<BlockControl>`   | Block menu items.   |
| `controls.icon`            | `'close' \| ...`        | Control icon.       |
| `controls.label`           | `string`                | Control label.      |
| `controls.onPress`         | `Action`                | Pressed action.     |
| `controls.confirm`         | `object`                | Confirmation modal. |
| `controls.confirm.title`   | `string`                | Confirmation title. |
| `controls.confirm.text`    | `string`                | Confirmation text.  |
| `controls.confirm.confirm` | `string`                | Confirmation label. |
| `controls.confirm.style`   | `"primary" \| "danger"` | Confirmation style. |
