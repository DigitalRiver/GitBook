---
description: Understand async error objects.
---

# Async error objects

When Admin API detects an asynchronous error, it returns the `errors` object in the response. This object will return the [code ](broken-reference)and description.

{% code title="Errors response example" overflow="wrap" %}
```json
"errors": [
    {
        "code": "PRODUCT_NOT_FOUND",
        "description": "Cannot find the product, produtId1, productId2. The specified product IDs could not be found. Provide the correct product ID and try again."
    },
    {
        "code": "LOCALE_NOT_PROVIDED",
        "description": "A locale is required. Provide the locale and try again."
    }
]
```
{% endcode %}
