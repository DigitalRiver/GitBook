---
description: Learn more about tax registrations.
---

# Tax registrations

## Tax registration resource

The following describes some of the key attributes for [updating a tax registration](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations/post).

### Key

The `key` is the tax registration key.

### Value

The `value` is the tax identifier.

## Tax registrations query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of applied offers. The following topics describe the query parameters available for [applied-offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers/get). For more information on how to use query parameters, see [Fields and query parameters](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### API key

The `apiKey` is your account's [API key](../../../resources/API-structure/) used to authenticate your API requests. You must specify either an `apiKey` or `token`. This query parameter is available when you [get the cart tax registration schema](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations\~1schema/get).

### Token

The `token` is the authorized or anonymous token for the shopper. You must specify either an `apiKey` or `token`. This query parameter is available when you [get the cart tax registration schema](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations\~1schema/get), [update the tax registration data on the customer's cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations/post), or [remove the tax registration from the customer's cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations/delete).
