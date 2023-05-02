---
description: Learn more about the returns resource.
---

# Returns

## Returns resource

The following describes some of the key attributes for [line item returns](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Returns/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1returns/posthttps://www.digitalriver.com/docs/commerce-shopper-api/#tag/Returns/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1returns/post).

### Return

The `return` object contains the return information.

### Reason

The `reason` provides the reason for the return.

### Comments

The `comments` provides any additional information regarding the return.

### Accept ELOD

An electronic letter of destruction (ELOD) is the agreement a shopper accepts when they return a digital product. When `acceptELOD` is `true`, the customer must complete the ELOD and destroy all copies of the product before they can return the product.

### Return line items

The `returnLineItems` is an array of objects containing the returned line items.

### Line item quantity identifiers

The `lineItemQuantityIdentifiers` is an array of integers.

### Line item

The `lineItem` object contains the line item identifier and product quantity.

* **`id`**: The `id` is the line item identifier.
* **`quantity`**: The `quantity` is the number of products.

## Returns query parameters

The following describes the query parameters for [returns](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Returns).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information and examples.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See the [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information and examples.

### Format

The format overrides the XML default format for the Authorize Shopper API. The valid values are `XML` and `JSON`.

### Token

The `token` is the authorized or anonymous token for the shopper.
