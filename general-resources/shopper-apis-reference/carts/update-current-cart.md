# Update current cart

## Update current cart query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of carts. The following topics describe the query parameters available for [carts/active](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts). For more information on how to use query parameters, see [Fields and query parameters](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### External reference identifier (ERID)

The [`externalReferenceId`](../../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) is a company's internal identifier for a product.&#x20;

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Offer identifier

The `offerId` is the offer's identifier.

### Parent line item identifier

The `parentLineItemId` is the line item identifier of the parent product. While adding a child product to the cart, provide the line item identifier of the parent product along with the offer identifier to specify the child product should be associated with which parent product line item.

### Product identifier

A `productId` is your unique [product identifier](update-current-cart.md#product-identifier) or unique stock keeping unit (SKU) for a product. A product's unique identifier is represented by an `id`.&#x20;

### Promotional code

The `promoCode` is the promotional code the shopper wants to apply to the cart.

### Quantity

The `quantity` is the number of products added to the cart. The value must be a valid integer. If the quantity is not explicitly specified, the default is 1.

### Suppress order confirmation email

A real order uses `suppressorderconfirmationemail` to suppress the order confirmation email. If you want to use this feature, contact your Customer Success Manager.

### Term identifier

The `termId` is the finance term identifier associated with the cart. You must pass the `termId` with the `productId` or `externalReferenceId`.

### Token

The `token` is the authorized or anonymous token for the shopper.'
