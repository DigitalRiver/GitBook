---
description: Learn more about the apply shopper resource.
---

# Apply shopper

## Apply shopper query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of shopper information. The following topics describe the query parameters available for the [apply-shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post). For more information on how to use query parameters, see [Fields and query parameters](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Billing address identifier

The `billingAddressId` identifies the shopper's address resource. Digital River uses the shopper's default address if no value is provided.

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Payment option identifier

The `paymentOptionId` is the payment option identifier for a specific payment method. Digital River uses this value when a shopper selects a payment method and applies it to their cart. If the shopper does not select a payment method, Digital River uses the shopper's default payment option.

### Shipping address identifier

The `shippingAddressId` is the identifier of a shopper address resource to use as the shipping address. If neither shipping nor a billing address is provided, the default address for the shopper is used. Otherwise, the billing address ID (if provided) is applied as the default shipping address.

### Token

The `token` is the authorized token for the shopper.
