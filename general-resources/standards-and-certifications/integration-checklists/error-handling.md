---
description: >-
  Learn more about the standards related to logging requests, responses, and
  errors.
---

# Error handling

The [checklist items](error-handling.md#integration-checklist) and [standards](error-handling.md#integration-standards) in this section cover logging requests, responses, and errors. This helps ensure you can provide adequate technical details when seeking support from Digital River or upstream platforms. We also cover the types of error messages you should and should not display to your customers.

## Integration checklist

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] [Depending on the capabilities of your commerce system, do you log all appropriate API requests and responses?](error-handling.md#log-appropriate-api-requests-and-responses)
* [ ] [Do you provide a framework for passing failure responses (in other words, non-200 responses) back to your commerce system so that they can be acted upon?](error-handling.md#pass-failure-responses-to-your-commerce-system)
* [ ] [Do you display simple, but meaningful, messages so that customers can effectively respond to the error?](error-handling.md#display-errors-to-customers)

## Integration standards

These integration standards relate to error handling and logging:

### Log appropriate API requests and responses

It's good practice, especially during the development and testing phases, to log all of your platform's successful and failed API calls. When you're making a large number of calls, however, this can quickly become overwhelming.

You may decide you want to add a toggle to your tool that allows you to enable or disable debug logging. This would then permit each client site that implements the tool to turn off logging when necessary.

### Pass failure responses to your commerce system

All the Digital River APIs respond with [standardized HTTP status codes](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes). In case they are needed for support purposes, your platform should log the error responses in the `4xx` and `5xx` range. We recommend you do this regardless of whether you have a setting to disable bug logging. Your error logs should include a timestamp, HTTP code, the URL of the API, and the API request and response payloads.

### Display errors to customers

When customers [encounter errors](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes/Error-types) during the checkout process, or any time while interacting with your tool, you should provide them simple, but meaningful messages. You should not, however, share [specific error codes](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes/Error-codes). Doing so increases the probability that attempts to commit fraud and other malicious attacks will eventually succeed.
