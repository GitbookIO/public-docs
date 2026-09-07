---
description: Reference for built-in and custom ContentKit actions
---

# Actions

ContentKit actions handle events in your component. GitBook provides built-in actions, and your component can define custom actions.

### Built-in actions

#### `@editor.node.updateProps`

Updates properties stored on the editor node bound to the current component. GitBook dispatches this action when component props change:

```json
{
  "action": "@editor.node.updateProps",
  "props": {}
}
```

#### `@ui.url.open`

Opens a URL:

```json
{
  "action": "@ui.url.open",
  "url": "https://www.gitbook.com"
}
```

#### `@ui.modal.open`

Opens `componentId` as an overlay modal with `props`:

```json
{
  "action": "@ui.modal.open",
  "componentId": "myModal",
  "props": {}
}
```

#### `@ui.modal.close`

Closes the current modal. Call this action from a modal component. It can include return data from the modal:

```json
{
  "action": "@ui.modal.close"
}
```

#### `@webframe.ready`

Signals that a webframe is ready to receive messages and updates:

```json
{
  "action": "@webframe.ready"
}
```

#### `@webframe.resize`

Resizes a webframe container:

```json
{
  "action": "@webframe.resize",
  "aspectRatio": 1.7,
  "maxHeight": 400,
  "maxWidth": 300
}
```

#### `@link.unfurl`

GitBook sends this action to a block when someone pastes a matching URL:

```json
{
  "action": "@link.unfurl",
  "url": "https://myapp.com/"
}
```

Configure URL patterns in your integration manifest:

```yaml
blocks:
  - id: helloworld
    title: Hello world
    urlUnfurl:
      - https://myapp.com/
```

Follow [create-a-custom-unfurl-action-for-your-integration.md](../../guides/create-a-custom-unfurl-action-for-your-integration.md "mention") for a complete example.

### Custom actions

Define custom action names in your component. The action name is available on the `action` object:

```typescript
action: async (previous, action) => {
  switch (action.action) {
    case 'custom-action':
      return {};
    default:
  }
}
```
