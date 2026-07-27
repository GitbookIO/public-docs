---
description: Every ContentKit component you can use inside a custom block.
---

# ContentKit component reference

The components available to use inside `render()` fall into three categories: **Layout** (structuring your integration), **Display** (representing data and media), and **Interactive** (user input and actions).

## Layout

### `block`

The top-level component for a custom block.

```tsx
<block>
    ...
</block>
```

| Props | Type | Description |
|---|---|---|
| `children`\* | `Array<Block>` | Content to display in the block. |
| `controls` | `Array<BlockControl>` | Control menu items displayed for the block. |
| `controls.icon` | `'close' \| ...` | The icon to display with the control. |
| `controls.label` | `string` | The label for the control. |
| `controls.onPress` | `Action` | Action dispatched when the control is pressed. |
| `controls.confirm` | `object` | Modal to confirm the action before executing it. |
| `controls.confirm.title` | `string` | Title for the confirmation modal. |
| `controls.confirm.text` | `string` | Content for the confirmation modal. |
| `controls.confirm.confirm` | `string` | Label for the confirmation button. |
| `controls.confirm.style` | `"primary" \| "danger"` | Style for the confirmation button. |

### `vstack`

Flex layout element that renders a vertical stack of elements.

```tsx
<vstack>
    ...
</vstack>
```

| Props | Type | Description |
|---|---|---|
| `children`\* | `Array<Block>` | Content to display in the stack. |
| `align` | `'start' \| 'center' \| 'end'` | Horizontal alignment of the elements in the stack. |

### `hstack`

Flex layout element that renders a horizontal stack of elements.

```tsx
<hstack>
    ...
</hstack>
```

| Props | Type | Description |
|---|---|---|
| `children`\* | `Array<Block>` | Content to display in the stack. |
| `align` | `'start' \| 'center' \| 'end'` | Vertical alignment of the elements in the stack. |

### `divider`

A visual delimiter between two elements in a containing stack.

```tsx
<divider />
```

| Props | Type | Description |
|---|---|---|
| `style` | `"default" \| "line"` | Visual style for the divider. |
| `size` | `"medium" \| "small" \| "large"` | Spacing of the divider (default `medium`). |

## Display

### `box`

```tsx
<box style="card">
    ...
</box>
```

| Props | Type | Description |
|---|---|---|
| `children`\* | `Array<Block> \| Array<Inline>` | Content to display in the box. |
| `grow` | `number` | Portion of remaining space the element should take up. |

### `card`

```tsx
<card title="I am a card">
    ...
</card>
```

| Props | Type | Description |
|---|---|---|
| `children` | `Array<Block> \| Array<Inline>` | Content to display in the card. |
| `title` | `string` | Title for the card. |
| `hint` | `string` | Hint for the card. |
| `icon` | `'close' \| ...` | Icon or image displayed with the card. |
| `onPress` | `Action` | Action dispatched when pressed. |
| `buttons` | `Array<Button>` | Buttons shown in the top-right corner of the card. |

### `text`

```tsx
<text>
    Hello <text style="bold">World</text>
</text>
```

| Props | Type | Description |
|---|---|---|
| `children`\* | `Array<string \| Text>` | Text content. |
| `style`\* | `"bold" \| "italic" \| "strikethrough" \| "code"` | Formatting style. |

### `image`

```tsx
<image
    source={{ url: "https://example.com/image.png" }}
    aspectRatio={16 / 9}
/>
```

| Props | Type | Description |
|---|---|---|
| `source`\* | `object` | Image source. |
| `source.url`\* | `string` | URL of the image. |
| `aspectRatio`\* | `number` | Aspect ratio of the image. |

### `markdown`

```tsx
<markdown content="Hello **world**" />
```

| Props | Type | Description |
|---|---|---|
| `content`\* | `string` | Markdown content to display. |

## Interactive

### `modal`

```tsx
<modal>
    ...
</modal>
```

| Props | Type | Description |
|---|---|---|
| `children`\* | `Array<Block> \| Array<Inline>` | Modal content. |
| `title` | `string` | Modal title. |
| `subtitle` | `string` | Modal subtitle. |
| `size` | `'medium' \| 'xlarge' \| 'fullscreen'` | Modal size. |
| `returnValue` | `object` | Data returned when the modal is closed. |
| `submit` | `Button` | Submit button. |

### `button`

```tsx
<button label="Click me" onPress={{ type: 'something' }} />
```

| Props | Type | Description |
|---|---|---|
| `label`\* | `string` | Button text. |
| `onPress`\* | `Action` | Triggered action. |
| `style` | `'primary' \| 'secondary' \| 'danger'` | Button style. |
| `tooltip` | `string` | Hover tooltip. |
| `icon` | `'close' \| ...` | Icon to display. |
| `confirm` | `object` | Confirmation modal. |
| `confirm.title`\* | `string` | Confirmation modal title. |
| `confirm.text`\* | `string` | Confirmation text. |
| `confirm.confirm`\* | `string` | Confirmation button label. |
| `confirm.style`\* | `'primary' \| 'danger'` | Confirmation button style. |

### `textinput`

```tsx
<textinput
    id="name"
    label="Name"
    initialValue="John Doe"
    placeholder="Enter a name"
/>
```

| Props | Type | Description |
|---|---|---|
| `state`\* | `string` | State key for binding. |
| `initialValue` | `string` | Initial input value. |
| `label` | `string` | Input label. |
| `placeholder` | `string` | Placeholder text. |

### `codeblock`

```tsx
<codeblock content="const variable = 10" syntax="javascript" />
```

| Props | Type | Description |
|---|---|---|
| `content`\* | `string` | Code content. |
| `syntax` | `string` | Code syntax highlight. |
| `lineNumbers` | `boolean \| number` | Show line numbers. |
| `buttons` | `Array<Button>` | Overlay buttons. |
| `state` | `string` | Makes the block editable; value stored in state. |
| `onContentChange` | `Action` | Action fired on edit. |

`codeblock` is also the way to build a prompt-style block — it renders with the same visual treatment as a code block, which works well for prompts, commands, or other text a reader might want to reuse elsewhere. ContentKit doesn't expose a dedicated `prompt` component, and it doesn't define a built-in clipboard or "open in AI tool" action for `codeblock` — build the closest equivalent with overlay buttons and `@ui.url.open`:

```tsx
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
```

Here, `cursorUrl` is a URL or deeplink your integration generates for the target tool. Only add a copy button if your integration has a supported way to handle copy behavior — there's no built-in clipboard action to fall back on today.

### `webframe`

```tsx
<webframe
    source={{ url: 'https://www.gitbook.com' }}
    aspectRatio={16 / 9}
/>
```

| Props | Type | Description |
|---|---|---|
| `source`\* | `object` | URL source. |
| `source.url`\* | `string` | URL of the external site. |
| `aspectRatio`\* | `number` | Aspect ratio. |
| `buttons` | `Array<Button>` | Overlay buttons. |
| `data` | `Record<string, string>` | State dependencies. |

`data` values, along with GitBook-provided context, reach the frame through the `message` event as `event.data.state`. GitBook reserves two keys in `state`: `page` (`{ id, path, title }` of the current page, always available) and `visitor` (visitor claims, gated behind the `site:visitor:claims` scope). A webframe can also navigate the reader to another page in the site by posting a `@webframe.navigate` action with a `path`. See the [interactive blocks guide](../guides/interactivity.md#page-and-visitor-context).

### `select`

```tsx
<select state>
    ...
</select>
```

| Props | Type | Description |
|---|---|---|
| `state`\* | `string` | State key. |
| `initialValue` | `string \| string[]` | Initial selected value. |
| `placeholder` | `string` | Placeholder. |
| `multiple` | `boolean` | Allow multiple selection. |
| `options` | `Array<object>` | Selectable options. |
| `options.id` | `string` | Option ID. |
| `options.label` | `string` | Option label. |
| `options.url` | `string` | Option external link. |

### `switch`

```tsx
<switch />
```

| Props | Type | Description |
|---|---|---|
| `state`\* | `string` | State key. |
| `initialValue` | `boolean` | Initial value. |
| `confirm.title`\* | `string` | Confirmation title. |
| `confirm.text`\* | `string` | Confirmation text. |
| `confirm.confirm`\* | `string` | Confirmation button label. |
| `confirm.style`\* | `'primary' \| 'danger'` | Confirmation style. |

### `checkbox`

```tsx
<checkbox />
```

| Props | Type | Description |
|---|---|---|
| `state`\* | `string` | State key. |
| `value` | `string \| number` | Value when checked. |
| `confirm.title`\* | `string` | Confirmation title. |
| `confirm.text`\* | `string` | Confirmation text. |
| `confirm.confirm`\* | `string` | Confirmation button label. |
| `confirm.style`\* | `'primary' \| 'danger'` | Confirmation style. |

### `radio`

```tsx
<radio />
```

| Props | Type | Description |
|---|---|---|
| `state`\* | `string` | State key. |
| `value` | `string \| number` | Value when selected. |
| `confirm.title`\* | `string` | Confirmation title. |
| `confirm.text`\* | `string` | Confirmation text. |
| `confirm.confirm`\* | `string` | Confirmation button label. |
| `confirm.style`\* | `'primary' \| 'danger'` | Confirmation style. |

## Formatting a block as Markdown

For Git Sync, a block can be represented as a Markdown code block instead of raw HTML. Define a `markdown` property on the block in `gitbook-manifest.yaml`:

```yaml
blocks:
    - id: block-name
      title: My custom block
      markdown:
        codeblock: blocksyntax
        body: content
```

A block with the properties `{ "content": "something" }` is then formatted in Markdown as:

````markdown
```blocksyntax
something
```
````

Any other properties on the block are set on the code block too — for example, `{ "content": "something", "propA": "A" }` becomes:

````markdown
```blocksyntax propA="A"
something
```
````

{% hint style="info" %}
GitBook's native Mermaid block uses this pattern. If a page still has older Mermaid code blocks from a previous integration, GitBook converts them automatically the next time the page is edited.
{% endhint %}
