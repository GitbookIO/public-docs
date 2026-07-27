---
description: Add interactivity to custom blocks in GitBook integrations using inputs, buttons, and more
---

# Create interactive blocks

GitBook lets you create custom, interactive blocks using ContentKit. Components can be interactive — visitors can type or click in them — because different components expose different action handlers, like buttons exposing an `onPress` event.

When creating a component through `createComponent()`, you specify how to handle each action through the `action` prop.

### Buttons and actions

The most common interactive elements are buttons, used to trigger an asynchronous action.

```tsx
<button
    label="Click me"
    onPress={{
        action: 'update-state',
        anotherProperty: 'something'
    }}
/>
```

When the user presses the button, the action is dispatched to the integration and handled in the `action` callback:

```tsx
const helloWorldBlock = createComponent({
    ...
    async action(previous, action) {
        switch (action.action) {
            case 'update-state':
                return { state: { content: action.anotherProperty } };
            default:
        }
    },
    ...
});
```

### Text and other inputs

Collect user input with `textinput`:

```tsx
<textinput state="content" />
```

When an action is next dispatched (for example, pressing a button), the input's value is available as `state.content`.

### Dynamic binding

Actions are asynchronous — pressing a button re-runs your integration's code and re-renders the component. Some interactions, though, need synchronous binding for a good user experience (a live preview while typing, for instance). ContentKit's dynamic binding connects multiple elements to a shared dynamic state.

For example, bind a webframe directly to a text input:

```tsx
createComponent({
    componentId: 'demo',
    initialState: {
        content: ''
    },
    async render(element) {
        return (
            <block>
                <hstack>
                    <textinput state="content" />
                    <divider />
                    <webframe
                        source={{ uri: '/iframe.html' }}
                        data={{
                            content: element.dynamicState('content')
                        }}
                        />
                </hstack>
            </block>
        )
    }
})
```

Inside `iframe.html`, handle incoming events with the `message` listener:

```js
window.addEventListener("message", (event) => {
    if (event.data) {
        const content = event.data.state.content;
    }
});
```

### Page and visitor context

GitBook injects contextual information about the current site into the webframe's `state`, alongside anything you bind through `data`:

* `state.page` — the current page as `{ id, path, title }`. Always available.
* `state.visitor` — the visitor's claims, when the integration has the `site:visitor:claims` [scope](../manifest-reference.md#scopes).

This context arrives client-side through the same `message` event as your bound `data`, so it doesn't change how the block is cached:

```js
window.addEventListener("message", (event) => {
    const state = event.data?.state;
    if (!state) return;

    if (state.page) {
        const { id, path, title } = state.page;
        // e.g. build a link to a sibling page from `path`
    }
});
```

### Navigating to another page

A webframe can navigate the reader to another page in the site by posting a `@webframe.navigate` action. `path` resolves relative to the site root (the part after the site's base URL), so it can point to any page in any section or space of the site — navigation always stays within it. Pass an optional `anchor` to scroll to a heading on the target page:

```js
window.parent.postMessage({
    action: {
        action: '@webframe.navigate',
        path: 'guides/getting-started',
        anchor: 'installation',
    },
}, '*');
```

### Editable blocks

Most blocks — as opposed to static ones, or ones only generated from link unfurling — are designed to be editable by the user. Update a block's properties with an `@editor.node.updateProps` action:

```jsx
<block>
    <textinput state="content" />
    <button
        label="Edit"
        onPress={{
            action: '@editor.node.updateProps',
            props: {
                content: element.dynamicState('content')
            }
        }}
        />
</block>
```

### Webframes and actions

Webframes integrate external applications or complete UIs into GitBook. Pass data in with the `data` prop; to send data back out to the parent component, use `window.postMessage`:

```js
window.parent.postMessage({
    action: {
        type: 'doSomething',
    }
}, '*');
```

### Modals

Open an overlay modal to show extra information or prompt the user, by dispatching `@ui.modal.open`:

```typescript
const block = createComponent({
    componentId: 'block',
    async render(element) {
        return (
            <block>
                <button
                    label="Open modal"
                    onPress={{
                        action: '@ui.modal.open',
                        componentId: 'custommodal',
                        props: {
                            message: 'Hello world'
                        }
                    }}
                />
            </block>
        )
    }
});
```

This renders the `custommodal` component with the given props:

```typescript
const custommodal = createComponent({
    componentId: 'custommodal',
    async render(element) {
        return (
            <modal title="Hello world">
                <button
                    label="Close the modal"
                    onPress={{
                        action: '@ui.modal.close',
                        returnValue: {}
                    }}
                />
            </modal>
        )
    }
});
```

Closing a modal can pass `returnValue` data back to the parent component's action handler.

### Opening URLs

Open a URL as a webpage with the built-in action:

```typescript
<button
    onPress={{
        action: '@ui.url.open',
        url: 'https://www.gitbook.com'
    }}
/>
```

### Build a prompt-style block

To show a reusable prompt, use `codeblock` with overlay buttons — it renders like a code block, so readers can read the prompt in place and act on it without leaving the block. ContentKit doesn't expose a dedicated prompt component or a built-in action for opening a prompt in an AI tool or copying it to the clipboard. The supported pattern today is:

* Render the prompt with `codeblock`.
* Add overlay buttons for supported actions.
* Use `@ui.url.open` to open an external tool such as Cursor.

```tsx
const promptBlock = createComponent({
    componentId: 'prompt-block',
    async render() {
        const prompt = [
            'Summarize this API response.',
            'Highlight breaking changes.',
            'Return three migration steps.'
        ].join('\n');

        const cursorUrl =
            'https://example.com/open-in-cursor?prompt=' +
            encodeURIComponent(prompt);

        return (
            <block>
                <codeblock
                    content={prompt}
                    buttons={[
                        {
                            icon: 'arrow-up-right-from-square',
                            tooltip: 'Open in Cursor',
                            onPress: {
                                action: '@ui.url.open',
                                url: cursorUrl
                            }
                        }
                    ]}
                />
            </block>
        );
    }
});
```

`cursorUrl` stands for any URL or deeplink your integration supports for opening the prompt in the target tool. If you also want a copy button, treat it as an integration-specific enhancement — there's no built-in clipboard action for `codeblock` buttons today.
