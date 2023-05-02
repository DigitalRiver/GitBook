---
description: Learn more about the payment-options resource.
---

# Payment options

## Payment options query parameters

The following describes the query parameters for [payment-options](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information and examples.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See the [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information and examples. This query parameter is not available when [updating the shopper payment options](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options\~1%7BpaymentOptionId%7D/post).

### Token

The `token` is the authorized or anonymous token for the shopper.
