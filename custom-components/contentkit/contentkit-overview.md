---
description: Learn how to build components with GitBook's UI kit
---

# ContentKit overview

ContentKit is a UI framework that lets integrations build interactive layouts directly inside GitBook — for custom blocks, configuration flows, and more. It solves one problem: how to let external developers build UI in GitBook while keeping things secure, visually consistent, and platform-agnostic (it needs to run in every browser, and eventually mobile apps).

It takes inspiration from a few existing systems:

* [Slack Block Kit](https://api.slack.com/block-kit) and [Intercom Canvas Kit](https://developers.intercom.com/building-apps/docs/canvas-kit) for the overall concept.
* React, for UI definition and its declarative approach.
* React Native, for component naming.
* SwiftUI, for layout primitives (`spacer`, `divider`, stacks).

### Creating components

Components are created with `createComponent()`. A component represents a piece of UI, rendered with specific `props` and updated through actions that change its local `state`.

```tsx
import { createIntegration, createComponent } from '@gitbook/runtime';

const helloWorldBlock = createComponent({
    componentId: 'hello-world',
    initialState: {
        message: 'Say hello!'
    },
    action: async (previous, action) => {
        switch (action.action) {
            case 'say':
                return { state: { message: 'Hello world' } };
        }
    },
    render: async ({ props, state }) => {
        return (
            <block>
                <button label={state.message} onPress={{ action: 'say' }} />
            </block>
        );
    }
});

export default createIntegration({
    components: [helloWorldBlock]
});
```

#### Define a custom block

Blocks must be declared in the integration's [manifest](../manifest-reference.md#blocks):

```yaml
blocks:
  - id: hello-world
    title: Hello World Block
```

All blocks defined by installed integrations are listed in the insertion palette (⌘ + /) for every editor in the space.

### Props

Props are accessed in a component's `render` function, and work like [props in React](https://react.dev/learn/passing-props-to-a-component) — they describe how the component should render, and are bound to the block for all its instances.

```typescript
{
    action: "@editor.node.updateProps",
    props: {
        propMessage: "Props Updated!",
    },
};
```

### State

State tracks data that changes over time. It's local to a single component block, updated by setting state through an action, and scoped so only the component that defines it can access it — similar to [state in React](https://react.dev/learn/state-a-components-memory).

```typescript
{
    state: {
        stateMessage: "State Updated!"
    }
};
```

### Actions

{% hint style="success" %}
See the [interactive blocks guide](../guides/interactivity.md) for a full walkthrough of handling events in your integration.
{% endhint %}

Actions are how components handle or respond to UI events, and how they update their own state. GitBook provides a set of default actions, and you can define your own custom ones.

#### `@editor.node.updateProps`

Updates the properties stored on the editor node bound to the current component. Dispatched when a component's props are updated.

```json
{ "action": "@editor.node.updateProps", "props": {} }
```

#### `@ui.url.open`

Opens a URL.

```json
{ "action": "@ui.url.open", "url": "https://www.gitbook.com" }
```

#### `@ui.modal.open`

Opens a component (by `componentId`) with the given `props` as an overlay modal.

```json
{ "action": "@ui.modal.open", "componentId": "myModal", "props": {} }
```

#### `@ui.modal.close`

Closes the current modal. Can be called from within a modal component, and can carry return data back to the component that opened it.

```json
{ "action": "@ui.modal.close" }
```

#### `@webframe.ready`

Sent from a webframe to indicate it's ready to receive messages and updates.

```json
{ "action": "@webframe.ready" }
```

#### `@webframe.resize`

Sent from a webframe to resize its container.

```json
{ "action": "@webframe.resize", "aspectRatio": 1.7, "maxHeight": 400 }
```

#### `@link.unfurl`

Dispatched to a block when a user pastes a URL matching one of its configured unfurl patterns. See the [link unfurling guide](../guides/link-unfurling.md).

```json
{ "action": "@link.unfurl", "url": "https://myapp.com/" }
```

#### Custom actions

You can also define your own actions, referenced by name and handled in the component's `action` callback:

```typescript
action: async (previous, action) => {
    switch (action.action) {
        case 'custom-action':
            return {};
        default:
    }
}
```
