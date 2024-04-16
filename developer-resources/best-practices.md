---
description: Understand the best practices when integrating with the Digital River API.
---

# Best practices

## API keys

When integrating with the Digital River API, you should be aware of how to [use API keys](api-structure.md#api-keys) and [how they work with versioning](best-practices.md#versioning-and-keys).

## Versioning and keys

You should understand how your account's [API version](../general-resources/versioning.md) determines the requests allowed by an API and the responses generated. The version also determines the structure of events generated by API requests.

You should always ensure that your [API keys](api-structure.md#api-keys) are configured for the version expected by your code. In other words, when your code is deployed from test to production, the version on the keys should match the code version.

## Robustness

Digital River often makes [non-breaking changes](../general-resources/versioning.md#non-breaking-changes) to our API request and response content. As a result, we recommend your integration conform to the [tolerant reader](https://java-design-patterns.com/patterns/tolerant-reader/) principle. Specifically, this means that you should:

* Be aware that new elements can be added to responses at any time.
* Build your code to extract only the attributes needed when reading responses and ignore everything else.
* Avoid coding with a specific order of fields in mind.
* Assume that ids are alphanumeric strings, which potentially contain special characters, and they have variable lengths.
* Expect changes to the length and value of error messages and other strings that don’t represent an enumeration, type, or code.
* Anticipate the addition of new optional request and query parameters.

## Dates and times

You should be aware of how [dates and times in the Digital River API](api-structure.md#dates-and-times) are represented and ensure they are properly formatted in your requests.

## Fraud detection

To improve fraud detection, you should [provide an IP address](broken-reference) when creating a checkout, invoice, or order.

## Call debugging and troubleshooting <a href="#call-debugging" id="call-debugging"></a>

To make call debugging easier, you should use specific [HTTP request headers](api-structure.md#headers-for-troubleshooting).

## Validation and conflict errors

Attempt to minimize HTTP `400 Bad Request` and `409 Conflict` [error types](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes/Error-types) by adding appropriate validation checks before a request is submitted.

## Rate limiting

The [request rate limits](rate-limiting.md) we maintain help ensure that the Digital River APIs are efficient, secure, and reliable. So, when building your integration, you should be aware of [the rate limits we impose](rate-limiting.md#how-we-rate-limit) and then implement automatic retry mechanisms that [handle rate limiting](rate-limiting.md#handling-rate-limiting). To avoid hitting the request ceiling entirely, you should also follow our [rate limiting best practices](rate-limiting.md#rate-limiting-best-practices).

## Transaction Speeds

* For HTTP `GET` requests, we encourage making concurrent calls.
* Avoid making changes to the same resource in multiple calls. Instead, bundle changes in a single call.
* Avoid making concurrent mutation calls to the same resource.

## Test Mode

You can use the `liveMode` flag contained in API responses to determine whether you're pointing to the correct [environment](api-structure.md#test-and-production-environments).

```javascript
}
   ...
   "liveMode": false
}
```

## Webhooks

* When using [webhooks](../order-management/events-and-webhooks-1/webhooks/), check the [Digital River signature](../order-management/events-and-webhooks-1/webhooks/digital-river-signature.md) to ensure callback requests have not been tampered with.
* The webhook end point _must_ be able to handle concurrent webhook callback requests.
* Webhook events may be delivered multiple times. So be sure you can process the delivery of duplicate events.
* Your webhook endpoint must respond to callback requests in a timely manner. A response time greater than 3000 milliseconds is considered a timeout. We expect you to immediately acknowledge the callback request by sending an appropriate HTTP `2XX` response code. Once this acknowledgment is sent, you can then asynchronously process the webhook event on your end.