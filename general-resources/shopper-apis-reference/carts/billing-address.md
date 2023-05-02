---
description: Learn more about the billing address.
---

# Billing address

## Billing address resource

### Order identifier

The `orderId` is the order's identifier. This path parameter is required when you [get the billing address for the order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1billing-address/get).

## Billing address query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of billing addresses. The following topics describe the query parameters available for the [billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address). For more information on how to use query parameters, see [Fields and query parameters](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Country

The `country` is a two-digit [ISO 3166-2](https://en.wikipedia.org/wiki/ISO\_3166-2) country code. This query parameter is available when you [apply a billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-billing-address/post).&#x20;

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information. This query parameter is available when you [get the billing address for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1billing-address/get), [get the cart's billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/get), [add or update the cart's billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/put), or [apply a billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-billing-address/post).

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information. This query parameter is available when you [get the billing address for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1billing-address/get), [get the cart's billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/get), [add or update the cart's billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/put), or [apply a billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-billing-address/post).

### Postal code

The `postalCode` is the postal code. For United States addresses, Digital River supports ZIP+4 codes. They consist of the last four digits of a full nine-digit ZIP code. A nine-digit ZIP Code has two parts: the initial five digits of the zip code indicating the destination post office or delivery area, and the last four digits representing a specific delivery route within that overall delivery area. This query parameter is available when you [apply a billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-billing-address/post).&#x20;

### Suggestion identifier

The `suggestionId` is the identifier of the Billing Address Suggestion resource to apply to the cart's billing address. This query parameter is available when you [apply a billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-billing-address/post).&#x20;

### Token

The `token` is the authorized or anonymous token for the shopper. This query parameter is available when you [get the billing address for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1billing-address/get), [get the cart's billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/get), [add or update the cart's billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/put), or [apply a billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-billing-address/post).
