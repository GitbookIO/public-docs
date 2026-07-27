# API Reference

The GitBook API is RESTful and supports standard HTTP methods (`GET`, `POST`, `PATCH`, `DELETE`) for:

* **Content management** — create, update, and retrieve documents and pages.
* **Collaboration** — manage users, organizations, and permissions.
* **Integration** — connect GitBook with external tools and services.

### OpenAPI spec

GitBook's hosted OpenAPI spec, used to generate this reference, is available at [api.gitbook.com/openapi.json](https://api.gitbook.com/openapi.json).

{% openapi src="https://api.gitbook.com/openapi.json" %}
[api.gitbook.com/openapi.json](https://api.gitbook.com/openapi.json)
{% endopenapi %}

### Concepts

A few identifiers you'll use across almost every endpoint:

| Term | Description | Where to find it |
|---|---|---|
| `organizationId` | A unique identifier for an organization. | In the URL of any space (`https://app.gitbook.com/o/<organizationId>/s/<spaceId>`), or via **Copy org ID** in organization settings. |
| `spaceId` | A unique identifier for a space. | In the URL of any space (`https://app.gitbook.com/o/<organizationId>/s/<spaceId>`), or via **Copy space ID** in the dropdown at the top-right of a space. |
| `userId` | A unique identifier for a user. | From the "Get current user" endpoint, or via **Copy user ID** in organization settings. |

