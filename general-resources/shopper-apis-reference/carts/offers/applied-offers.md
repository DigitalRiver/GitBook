---
description: Learn more about applied offers.
---

# Applied offers

## Applied offers resource

The following describes some of the key attributes for [applied-offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers\~1%7BofferId%7D/delete).

### Offer identifier

The `offerId` is the offer's identifier. This path parameter is only available when you [delete an applied offer](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers\~1%7BofferId%7D/delete).

## Applied offers query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of applied offers. The following topics describe the query parameters available for [applied-offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers/get). For more information on how to use query parameters, see [Fields and query parameters](../../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### API key

The `apiKey` is your account's [API key](../../../../resources/API-structure/) used to authenticate your API requests. You must specify either an `apiKey` or `token`. This query parameter is not available when you [delete an applied offer](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers\~1%7BofferId%7D/delete).

### Token

The `token` is the authorized or anonymous token for the shopper. You must specify either an `apiKey` or `token`.
