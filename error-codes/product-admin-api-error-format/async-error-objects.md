---
description: Understand async error objects.
---

# Async error objects

When Product Admin API detects an asynchronous error, it returns the `errors` object in the response. This object will return the [code](../product-admin-api-error-codes/asynchronous-response-error-codes.md) and description.

{% code title="Errors response example" overflow="wrap" %}
```json
"errors": [
    {
        "code": "PRODUCT_NOT_FOUND",
        "description": "Cannot find the product, produtId1, productId2. The specified product IDs could not be found. provide the correct product ID and try again."
    },
    {
        "code": "LOCALE_NOT_PROVIDED",
        "description": "A locale is required. Provide the locale and try again."
    }
]
```
{% endcode %}
