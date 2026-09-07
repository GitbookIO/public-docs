---
description: Learn how to build components with GitBook’s UI kit
---

# ContentKit

ContentKit is a UI framework allows you to build integrations that work from directly within GitBook. It is used to define interactive layouts for Custom Blocks, Configurations flows and more.

### Creating components

Components are created using the `createComponent` method, which uses a few different options to customize it's behavior. A component represents an element of the UI rendered with specific `props` and updated through actions impacting its local `state`.

In addition to creating components, there are a few concepts related specifically to ContentKit and Custom Blocks that will let your integration interact with the rest of GitBook.

The following example displays a button, that when clicked, will return a message in the component's local state that says "Hello world".

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

Blocks must defined in the [integration's manifest](../../configurations.md#blocks) file:

```yaml
blocks:
  - id: hello-world
    title: Hello World Block
```

All blocks defined in an installed integrations will be listed in the insertion palette for all editors of the space.

### Props

Props in ContentKit components are accessed in the render function of your integration. They work similarly to [props in React](https://react.dev/learn/passing-props-to-a-component), and help describe the way your component should render.

Props are bound to your component block for all instances.

```typescript
{
    action: "@editor.node.updateProps",
    props: {
        propMessage: "Props Updated!",
    },
};
```

### State

State in a ContentKit component is a way to keep track of data and information as it changes over time. State is bound locally to a component block, and can be updated by setting the state through an action. It's scoped to only be accessible by the component it's defined in, and works similarly to [state in React](https://react.dev/learn/state-a-components-memory).

```typescript
{ 
    state: { 
        stateMessage: "State Updated !" 
    } 
};
```

### Actions

Actions handle events in your component and update its state. See [actions.md](actions.md "mention") for built-in actions, including `@webframe.ready` and `@webframe.resize`, and custom action handling.

{% hint style="success" %}
Follow [interactivity.md](../../guides/interactivity.md "mention") to handle an event in your integration.
{% endhint %}

### Component reference

ContentKit provides layout, display, and interactive blocks. Browse the [component-reference](component-reference/ "mention") to find each block’s props and examples.
