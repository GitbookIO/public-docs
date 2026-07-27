---
description: Learn about the rate limits the GitBook API enforces.
---

# Rate limiting

Different API methods are subject to different rate limits. The response's HTTP headers are the authoritative source for your current rate limit status:

| Header | Description |
|---|---|
| `X-RateLimit-Limit` | The maximum number of requests you're permitted to make in the current rate limit window. |
| `X-RateLimit-Remaining` | The number of requests remaining in the current window. |
| `X-RateLimit-Reset` | The time the current window resets, in [UTC epoch seconds](http://en.wikipedia.org/wiki/Unix_time). |

If you exceed the rate limit, you get a `429` response:

```
> HTTP/2 429
> X-RateLimit-Limit: 60
> X-RateLimit-Remaining: 0
> X-RateLimit-Reset: 1377013266

> {
>    "error": {
>        "code": 429
>        "message": "API rate limit exceeded. Please try again in 60 seconds"
>    }
> }
```
