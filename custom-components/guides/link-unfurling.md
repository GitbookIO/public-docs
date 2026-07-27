---
description: Build an integration that unfurls and displays embedded links on a page
---

# Create a custom unfurl action

Link unfurling is the automatic previewing of a link shared in an online platform. Paste a link, and the platform fetches information from the page and shows a preview instead of the bare URL.

{% hint style="info" %}
#### Most links unfurl automatically in GitBook

GitBook uses [iFramely](https://iframely.com/domains) to unpack and unfurl pasted links. If iFramely doesn't support your link out of the box, GitBook falls back to displaying it as plain text — that's when you need an integration to handle the unfurling yourself.
{% endhint %}

### Create an integration

Start with [Build your first integration](../getting-started/build-your-first-integration.md) to get the boilerplate set up, then add a component like this:

```tsx
import {
    createIntegration,
    createComponent,
} from '@gitbook/runtime';

const UnfurlExample = createComponent<{
    url?: string;
}>({
    componentId: 'unfurl-example',

    async action(element, action) {
        switch (action.action) {
            case '@link.unfurl': {
                // The pasted URL
                const { url } = action;

                return {
                    props: {
                        url,
                    },
                };
            }
        }

        return element;
    },

    async render(element, context) {
        const { url } = element.props;

        return (
            <block>
                <webframe
                    source={{
                        url: url
                    }}
                />
            </block>
        );
    },
});

export default createIntegration({
    components: [UnfurlExample],
});
```

### Configure the block to unfurl URLs

GitBook needs to know which integration handles which URLs. Configure the block with the URL patterns it should unfurl:

```yaml
blocks:
    - id: unfurl-example
      title: Unfurl Block
      urlUnfurl:
        - https://example.com
```

### How it works

After the integration is installed, unfurling a matching link works like this:

1. The user finds and launches your integration.
2. A modal prompts them to paste a link.
3. Pasting a link that matches the configured pattern runs the `@link.unfurl` action, which returns props to the component.
4. The component renders with those props — in the example above, a [`webframe`](../contentkit/contentkit-component-reference.md#webframe) embedding the pasted link.

Because `@link.unfurl` runs before the component renders, you can add logic to extract more information from the URL — an `id`, [`URLSearchParams`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams), or anything else your integration needs — before deciding what to display. You can also use [dynamic binding](../guides/interactivity.md#dynamic-binding) to connect the webframe to other components, or post messages to the page as a whole. In `render`, control what's shown when data isn't found or a link is private.
