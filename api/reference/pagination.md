---
description: Learn how to view and navigate paginated results from the GitBook API.
---

# Pagination

Some endpoints return paginated results, always in this shape:

```json
{
    "items": [
        ...
    ],
    "next": {
        "page": "..."
    },
    "previous": {
        "page": "..."
    }
}
```

`previous` and `next` are omitted when there's no previous or next page. Take the `next.page` or `previous.page` value and pass it back as the `page` query parameter to get that page.

### Example

A GET request to a paginated endpoint returns:

```json
{
  "items": [],
  "next": {
    "page": "next-page-id"
  }
}
```

To get the next page, add that ID as the `page` query parameter:

```
https://api.example.com/foo/bar?page=next-page-id
```
