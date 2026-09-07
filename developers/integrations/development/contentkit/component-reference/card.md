---
description: ContentKit card display component
---

# Card

```tsx
<card title="I am a card">...</card>
```

| Props      | Type                            | Description        |
| ---------- | ------------------------------- | ------------------ |
| `children` | `Array<Block> \| Array<Inline>` | Card content.      |
| `title`    | `string`                        | Card title.        |
| `hint`     | `string`                        | Card hint.         |
| `icon`     | `'close' \| ...`                | Icon or image.     |
| `onPress`  | `Action`                        | Pressed action.    |
| `buttons`  | `Array<Button>`                 | Top-right buttons. |
