---
description: Understand sync error objects.
---

# Sync error objects

When Commerce API detects a synchronous error, it returns an `errors` object in the response. This object will return the [code](broken-reference), subcode, description, and message.

{% code title="Errors response example" overflow="wrap" %}
```json
{
    "errors": [
        {
            "code": "invalid-request",
            "subcode": "invalid-task-status",
            "description": null,
            "message": "The value(s):[ABC, DEF] of taskStatus is invalid, expected value(s) is:[COMPLETED, FAILED, PROCESSING, PUBLISHED]"
        },
        {
            "code": "invalid-request",
            "subcode": "startingAfter-and-endingBefore-cannot-be-both-provided",
            "description": null,
            "message": "[startingAfter] and [endingBefore] can not both be provided."
        }
    ]
}
```
{% endcode %}
