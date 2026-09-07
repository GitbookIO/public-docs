---
description: ContentKit webframe component and frame communication
---

# Webframe

`webframe` embeds external content:

```tsx
<webframe source={{ url: 'https://www.gitbook.com' }} aspectRatio={16 / 9} />
```

| Props           | Type                     | Description         |
| --------------- | ------------------------ | ------------------- |
| `source`\*      | `object`                 | URL source.         |
| `source.url`\*  | `string`                 | External site URL.  |
| `aspectRatio`\* | `number`                 | Aspect ratio.       |
| `buttons`       | `Array<Button>`          | Overlay buttons.    |
| `data`          | `Record<string, string>` | State dependencies. |

### Receive data

Pass state through `data` with `element.dynamicState('content')`. The frame receives data and context through `message`:

```javascript
window.addEventListener('message', (event) => {
  const state = event.data?.state;
  if (!state) return;
  const content = state.content;
  const page = state.page;
});
```

GitBook provides `state.page` as `{ id, path, title }`. GitBook provides `state.visitor` with the `site:visitor:claims` scope.

### Send actions

Send a custom action to the integration with `postMessage`:

```javascript
window.parent.postMessage({ action: { type: 'doSomething' } }, '*');
```

Resize the container when frame content changes size:

```javascript
window.parent.postMessage({
  action: {
    action: '@webframe.resize',
    aspectRatio: 1.7,
    maxHeight: 400,
    maxWidth: 300
  }
}, '*');
```

Send `@webframe.ready` when the frame can receive updates. See [actions.md](../actions.md "mention").

For requests that don't need frame messaging, use your integration’s public HTTP endpoint. Follow [receiving-requests.md](../../../guides/receiving-requests.md "mention").

The frame can navigate a published site with `@webframe.navigate`. Send `path` after the site’s base URL and an optional `anchor`.

Follow [send-data-to-a-webframe.md](../../../guides/send-data-to-a-webframe.md "mention") for a complete example.
