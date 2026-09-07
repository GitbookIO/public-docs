---
description: ContentKit button component
---

# Button

```tsx
<button label="Update text" onPress={{ action: 'update-message' }} />
```

| Props               | Type                                   | Description         |
| ------------------- | -------------------------------------- | ------------------- |
| `label`\*           | `string`                               | Button text.        |
| `onPress`\*         | `Action`                               | Triggered action.   |
| `style`             | `'primary' \| 'secondary' \| 'danger'` | Button style.       |
| `tooltip`           | `string`                               | Hover tooltip.      |
| `icon`              | `'close' \| ...`                       | Icon.               |
| `confirm`           | `object`                               | Confirmation modal. |
| `confirm.title`\*   | `string`                               | Confirmation title. |
| `confirm.text`\*    | `string`                               | Confirmation text.  |
| `confirm.confirm`\* | `string`                               | Confirmation label. |
| `confirm.style`\*   | `'primary' \| 'danger'`                | Confirmation style. |

Use `onPress` for custom actions. Use `@ui.url.open` for external URLs. Follow [interactivity.md](../../../guides/interactivity.md "mention") for an example.
