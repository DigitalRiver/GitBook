---
description: Understand the error code format for the Shopper APIs.
---

# Error format for Shopper APIs

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

A basic error message (`error`) includes the following information:

* `code`–This parameter categorizes the failure reasons that look different but point to the same issue.
* `subcode`–This optional parameter appears when the system has more information about the error.
* `description`–A brief description of the error.
