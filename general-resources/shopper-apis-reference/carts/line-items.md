---
description: Learn more about line items.
---

# Line items

## Line items resource

The following describes some of the key attributes of line items.

### Order identifier

The `orderIdentifier` is the order's identifier. This path parameter is required when you [get the line items for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items/get), [get a line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items\~1%7BlineItemId%7D/get), or [get line items for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items/get), or [get a line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items\~1%7BlineItemId%7D/get).

### Line items identifier

The lineItemsId is the line item's identifier. This path parameter is required when you [get a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/get), [update a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post), [delete a line item in a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/delete), [get a line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items\~1%7BlineItemId%7D/get), [get a line item from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/get), [update a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post), [delete a line item in a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/delete), or [get a line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items\~1%7BlineItemId%7D/get).

## Line items query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of line items. The following topics describe the query parameters available for [line-items](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/get). For more information on how to use query parameters, see [Fields and query parameters](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Action

The `action` parameter modifies the POST behavior. The action parameter determines the method behavior for handling the quantity associated with a posted line item. Valid values are: `add`, `update`, and `subtract`. The default `action` for the[ `POST /v1/shoppers/me/carts/active/line-items/{lineItemsId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post) resource method is `update`. The default `action` for the [`POST /v1/shoppers/me/carts/active/line-items`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post) resource method is `add`. To override the default method behavior for handling quantity, explicitly specify the value of the action query parameter. This query parameter is available when you [update a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post).

### Company Identifier

The `companyId` is the company's identifier. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post)

### Expand

Use the [`expand` query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post), [get line items for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items/get), [update a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post), or [get a line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items\~1%7BlineItemId%7D/get).

### External reference identifier (ERID)

The [externalReferenceId](broken-reference) is a company's internal identifier for a product. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post) and [get a line item from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/get)

### Fields

Use the [`fields` query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post), [get line items for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items/get), [get a line item from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/get), [update a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post), or [get a line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items\~1%7BlineItemId%7D/get).

### Offer identifier

The `offerId` is the offer's identifier. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post)

### Line item identifier

A comma-separated list of one or more line item identifiers. This query parameter is available when you [delete line items from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/delete).

### Parent line item identifier

The `parentLineItemId` is the line item identifier of the parent product. While adding a child product to the cart, provide the line item identifier of the parent product along with the offer identifier to specify the child product should be associated with which parent product line item. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post).

### Product identifier

A `productId` is the unique [product identifier](line-items.md#product-identifier) or unique stock keeping unit (SKU) for a product. A product's unique identifier is represented by an `id`. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post).

### Token

The `token` is the authorized or anonymous token for the shopper. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post), [delete line items from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/delete), [get line items for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items/get), [get a line item from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/get), [update a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post), [delete a line item in a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/delete), or [get a line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items\~1%7BlineItemId%7D/get).

### Quantity

The `quantity` is the number of products added to the cart. The value must be a valid integer. If the quantity is not explicitly specified, the default is 1. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post), or [update a line item for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post).

### Suppress order confirmation email

A real order uses `suppressorderconfirmationemail` to suppress the order confirmation e-mail. If you want to use this feature, contact your Customer Success Manager. This query parameter is available when you [add line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post)&#x20;
