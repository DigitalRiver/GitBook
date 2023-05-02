---
description: Understand the error code format for the Shopper APIs.
---

# Error format for Shopper APIs

When encountering an error, a basic error message should contain the following details: a category parameter that distinguishes different types of failures that lead to the same issue, an optional parameter that provides additional system information, and a concise description of the error.

The Shopper APIs use the following format for errors:

{% code overflow="wrap" %}
```json
"errors": {
  "error": [
    {
      "relation": "https://api.digitalriver.com/v1/shoppers/SubmitCartResource",
      "code": "{error-code}",
      "subcode": "{error-subcode}",
      "description": "{error-description}"
    }
  ]
}
```
{% endcode %}
