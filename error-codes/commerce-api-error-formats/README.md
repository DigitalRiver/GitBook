---
description: Understand the error code formats for the Commerce API.
---

# Commerce API error formats

The Commerce API uses the following format for errors:

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
