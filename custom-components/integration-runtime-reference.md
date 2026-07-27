---
description: Extend GitBook with custom components, event handling, OAuth flows, and HTTP
---

# Integration runtime reference

GitBook's integration runtime is the platform that lets you build and run integrations within GitBook. Integrations extend GitBook by providing custom UI components, handling events, managing OAuth authentication, and communicating over HTTP.

The main building blocks are:

* **Integration initialization** — `createIntegration()`, the entrypoint that registers your integration.
* **UI components** — `createComponent()`, for interactive ContentKit components.
* **OAuth handling** — `createOAuthHandler()`, for managing authentication flows.
* **Environment context** — access runtime and installation details.
* **HTTP communication** — `fetch` to talk to external services.
* **Actions & rendering** — define component behavior and display.
* **Event handling** — listen and respond to GitBook events.
* **Web APIs** — `fetch`, `Request`, `Response`, `URL`, and `URLSearchParams`, available out of the box.

## `createIntegration`

The entrypoint for your integration. Exported from the main script referenced by `script` in your [manifest](manifest-reference.md#script), it sets up the integration's runtime context — HTTP handling, UI components, and event handlers.

```javascript
export default createIntegration({
  fetch: async (request, context) => {
    return new Response(JSON.stringify({ message: "Hello World" }), {
      headers: { "Content-Type": "application/json" }
    });
  },
  components: [
    myComponent
  ],
  events: {
    space_view: async (event, context) => {
      console.log("Space viewed:", event);
    },
  },
});
```

| Argument | Type | Description |
|---|---|---|
| `fetch` | Async function | Handles incoming HTTP requests or action dispatches. See [Fetch](#fetch). |
| `components` | Array | UI component definitions created with `createComponent()`. |
| `events` | Object | Maps event names to handler functions. See [Event](#event). |

## `createComponent`

The main way to create UI components. Must be listed under `blocks` in your [manifest](manifest-reference.md#blocks) to appear in GitBook's quick insert menu (⌘ + /).

```javascript
const myComponent = createComponent({
  componentId: "unique-id",
  initialState: (props) => ({ message: "Click me" }),
  action: async (element, action, context) => {
    switch (action.action) {
      case "say":
        return { state: { message: "Hello World" } };
      default:
        return {};
    }
  },
  render: async (element, context) => {
    return (
      <block>
        <button label={element.state.message} onPress={{ action: "say" }} />
      </block>
    );
  },
});
```

| Argument | Type | Description |
|---|---|---|
| `componentId`\* | `string` | Unique identifier for the component in the integration. |
| `initialState` | Function (props) ⇒ object | Initializes the component's state from its props. |
| `action` | Async function | Handles a dispatched action. See [Action](#action). |
| `render` | Async function | Returns the component's UI as ContentKit markup. See [Render](#render) and the [component reference](contentkit/contentkit-component-reference.md). |

## `createOAuthHandler`

Sets up an OAuth authentication flow — redirection, token exchange, and credential extraction. Credentials returned from `extractCredentials` are stored in the installation configuration.

```javascript
const oauthHandler = createOAuthHandler({
  redirectURL: `${environment.integration.urls.publicEndpoint}/oauth`,
  clientId: environment.secrets.CLIENT_ID,
  clientSecret: environment.secrets.CLIENT_SECRET,
  authorizeURL: "https://linear.app/oauth/authorize",
  accessTokenURL: "https://api.linear.app/oauth/token",
  extractCredentials: (response) => {
    if (!response.ok) {
      throw new Error(`Failed to exchange code for access token ${JSON.stringify(response)}`);
    }
    return {
      configuration: {
        oauth_credentials: { access_token: response.access_token },
      },
    };
  },
});
```

| Argument | Type | Description |
|---|---|---|
| `clientId`\* | `string` | Client application ID from the OAuth provider. |
| `clientSecret`\* | `string` | Client secret from the OAuth provider. |
| `authorizeURL`\* | `string` | URL users are redirected to for authorization. |
| `accessTokenURL`\* | `string` | URL used to exchange the authorization code for an access token. |
| `redirectURL` | `string` | Static redirect URL, if the OAuth provider requires one. |
| `scopes` | `string[]` | Scopes to request during authentication. |
| `prompt` | `string` | Optional prompt configuration for the authentication flow. |
| `extractCredentials` | Function | Processes the OAuth response and returns credentials in the expected shape. |

This pairs with a `button`-type property in your manifest's [configurations](manifest-reference.md#configurations).

## `action`

The async callback passed to `createComponent()`'s `action` key. Handles a dispatched action and returns updated `state` and/or `props`.

```typescript
action: async (element, action, context) => {
    return {}
},
```

**`element`** — the component instance dispatching the action:

| Key | Description |
|---|---|
| `props` | Props attached to the current instance of the component. |
| `state` | The component's local state. |
| `context` | Info about the component's context — type, editable status, current theme. |
| `setCache` | Sets the cache max-age for this component's output. |
| `dynamicState` | Returns an identifier for a dynamic state binding. |

**`action`** — the action being dispatched:

| Key | Description |
|---|---|
| `action` | The name of the action — either a default GitBook action or a custom one. |

See [default and custom actions](contentkit/contentkit-overview.md#actions).

**`context`** — same shape as in [`render`](#render), below.

## `render`

The async callback passed to `createComponent()`'s `render` key. Returns the component's UI as ContentKit markup.

```typescript
render: async (element, context) => {
    return (
        <block></block>
    )
},
```

**`element`** and **`context`** have the same shape as in [`action`](#action), above.

## `environment`

An object describing the runtime context your integration is executing in — API endpoints, integration configuration, installation details, and secrets. Access it via `context.environment` in `render`, `action`, and `fetch`.

```javascript
const { apiEndpoint, integration, secrets } = context.environment;
console.log("API endpoint:", apiEndpoint);
```

#### API information

| Key | Type | Description |
|---|---|---|
| `apiEndpoint` | string | URL of the HTTP API. |
| `apiTokens` | object | Authentication tokens for the API. |

#### Integration information

| Key | Type | Description |
|---|---|---|
| `integration` | object | Details about the integration itself. |

#### Site installation (if applicable)

| Key | Type | Description |
|---|---|---|
| `space` | string | ID of the space where the integration is installed. |
| `status` | object | Installation status: Active, Pending, or Paused. |
| `configuration` | object | Custom configuration variables for the space. |
| `externalIds` | any | External identifiers. |
| `urls` | object | URLs associated with the installation (e.g. `publicEndpoint`). |

#### Organization installation (if applicable)

| Key | Type | Description |
|---|---|---|
| `id` | string | Installation ID. |
| `space_selection` | object | Whether all spaces or a selection is used. |
| `configuration` | object | Custom configuration at the organization level. |
| `urls` | object | Organization-related URLs. |
| `externalIds` | string[] | External IDs assigned by the integration. |
| `target` | string | Target of the integration installation. |

#### Runtime secrets

| Key | Type | Description |
|---|---|---|
| `secrets` | object | Secrets stored on the integration for runtime use. Defined in [manifest configurations](manifest-reference.md#secrets). |

Prefer `spaceInstallation` when reading information about your integration.

## `event`

GitBook fires events when specific actions occur — viewing a page, updating content, and so on. Declare handlers under `events` in `createIntegration()`; each may need the [scope permissions](manifest-reference.md#scopes) relevant to that event.

```javascript
export default createIntegration({
    events: {
        space_view: async (event, context) => {
            // Handle event when the space your integration is installed in is viewed
        },
    },
});
```

| Event | Description |
|---|---|
| `installation_setup` | The integration was installed or updated globally. Payload: `eventId`, `type`, `installationId`, `status`. |
| `space_installation_setup` | The integration was installed or updated on a specific space. Payload: `eventId`, `type`, `installationId`, `spaceId`, `status`. |
| `space_view` | A page was visited. Payload: `eventId`, `type`, `pageId`, `visitor` (`anonymousId`, `cookies`, `userAgent`, `ip`), `url`, `referrer`. |
| `ui_render` | The integration's UI component was rendered. Payload: `eventId`, `type`, `auth.userId`, `componentId`, `props`, `state`, `context`, `action`. |
| `space_content_updated` | Content in a space was changed or updated. |
| `space_visibility_updated` | A space's visibility settings changed. Payload includes `visibility` and `previousVisibility`. |
| `space_gitsync_started` | A Git Sync process began for a space. Payload includes `revisionId`, `commitId`. |
| `space_gitsync_completed` | A Git Sync process completed for a space. Payload includes `state`, `revisionId`, `commitId`. |

## `fetch`

Handles incoming HTTP requests to your integration, passed as the `fetch` key to `createIntegration()`. Should return a valid [`Response`](#response).

```javascript
fetch: async (request, context) => {
  const data = { message: "Hello World" };
  return new Response(JSON.stringify(data), {
    headers: {
      "Content-Type": "application/json",
    },
  });
}
```

* **`request`** — the incoming [`Request`](#request).
* **`context`** — same shape as in [`action`](#action) and [`render`](#render): `context.environment` (see [Environment](#environment)) and `context.api`, an authenticated client to the GitBook API (see Developers → API).

For the shape of what actually arrives over HTTP — and when you'd need to handle it directly instead of through this callback — see [Work with HTTP requests](guides/receiving-requests.md).

## Web APIs

The runtime provides a few standard Web APIs out of the box, on top of the SDK.

### `fetch()`

Send outbound HTTP requests. See the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

```typescript
const resp = await fetch(
    `https://example.com/api/endpoint`,
    {
        headers: {
            Authorization: `<example-auth>`,
            Accept: 'application/json',
        },
    }
);
```

### `Request`

Represents a resource request. See the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/Request).

```typescript
const request = new Request("https://example.com", {
  method: "POST",
  body: '{"message": "Hello World"}',
});
```

### `Response`

Represents the response to a request. See the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/Response).

```typescript
const handleFetchEvent = async (request, context) => {
    return new Response(JSON.stringify({ message: "Hello World" }), {
      headers: { "Content-Type": "application/json" }
    });
};
```

### `URL`

Constructs a `URL` object from its parameters. See the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/URL/URL).

```typescript
let baseUrl = "https://gitbook.com/";
let integrations = new URL("/integrations", baseUrl);
// => 'https://gitbook.com/integrations'
```

### `URLSearchParams`

Utility methods for working with a URL's query string. See the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams).
