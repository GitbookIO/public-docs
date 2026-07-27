---
description: Learn about errors the GitBook API might return.
---

# Errors

GitBook uses conventional HTTP response codes to indicate success or failure:

* Codes in the **`2xx`** range indicate success.
* Codes in the **`4xx`** range indicate incorrect or incomplete parameters (e.g. a required parameter was omitted, or an operation failed with a third party).
* Codes in the **`5xx`** range indicate an error with GitBook's servers.

Errors are also returned as a JSON body with a code and message:

```json
{
    "error": {
        "code": 404,
        "message": "Page not found in this space"
    }
}
```
