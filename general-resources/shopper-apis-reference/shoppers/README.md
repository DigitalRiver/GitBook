---
description: Learn more about the shoppers resource.
---

# Shoppers

## Shoppers query parameters

The following describes the query parameters for [shoppers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers).

### Apply email to subscriptions

When the value for the `applyEmailToSubscriptions` query parameter is `true`, and you provide the `emailAddress` in the request body, all active and inactive subscription shipping and billing email addresses will be updated when you update the shopper's subscription billing and shipping email addresses. This query parameter is only available when [updating the current shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post).

### Currency

The `currency` query parameter sets the shopper's preferred currency. You can use this query parameter to update the preferred currency in the cart for authenticated and anonymous shoppers. This query parameter is only available when [updating the current shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information and examples.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See the [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information and examples.

### IP address

The `ipAddress` is the shopper's IP address for the current session.

### Locale

The `locale` query parameter sets the shopper's preferred locale. You can use this query parameter to update the shopper's preferred locale for authenticated and anonymous shoppers. This query parameter is only available when [updating the current shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post).

### Token

The `token` is the authorized or anonymous token for the shopper.
