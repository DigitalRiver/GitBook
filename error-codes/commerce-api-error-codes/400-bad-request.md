---
description: Understand the 400 Bad Request error codes.
---

# 400 Bad Request

## `dr_limited_token_invalid`

The limited token is invalid, expired, or revoked. Provide a valid token and try again.

* `invalid-keyword-expression`–Invalid keyword expression \[expression entered]. Provide a valid keyword expression and try again.
*   `invalid-request`–

    Cannot validate the request for one of the following reasons:

    * A comment is missing. Provide the comment and try again.
    * Invalid page size. Must be positive, non-zero, and less than 100000.
    * Invalid payment method type for this request. Provide a valid payment method type and try again.
    * The Return object is missing. Provide the Return object and try again.
    * The return reason is missing. Provide the reason for the return and try again.
    * The line items to return are missing. Provide the line items to return and try again.
    * The line-item quantity IDs are missing. Provide the line-item quantity IDs and try again.
    * The specified quantity to return is invalid. The number must be greater than zero and less than or equal to the number of items eligible for return. Specify a valid quantity to return and try again.
    * The system cannot parse the request because the request is not valid. Provide a valid request and try again.
    * The line-item ID is missing. Provide the line-item ID and try again.
    * The value in the input field contains sensitive data (for example, a credit card number). The subcode for this error is `sensitive-data-detected`. Remove the sensitive data and try again.

    The possible error descriptions are as follows:

    * `The request was invalid and could not be parsed by the system.`\
      The request format was invalid. Correct the request format and try again.
    * `Invalid or Missing Request Content`\
      There is a missing parameter or property in the request. Provide the missing parameter or property and try again.
    * `The specified subscription information is invalid and cannot be parsed.`\
      The `subscriptionInfo` block in the `lineItem` block is invalid. Correct the `subscriptionInfo` block and try again.
    * `Terms cannot exceed a length of 4000 characters.`\
      The length of `terms` in the `subscriptionInfo` block cannot exceed 4000 characters. Correct the length of the `term` and try again.
    * `The specified chargeType is invalid, the accepted values are customer_initiated, merchant_initiated and moto.`\
      The `chargeType` attribute is invalid. The accepted values are `customer_initiated`, `merchant_initiated`, and `moto`.
    * `perpetualUnitPrice must be provided for product id: {productId}`\
      The `perpetualUnitPrice` is required in the request.
    * `{property_name} cannot exceed a length of {length_consttraint} characters.`\
      The property names cannot exceed the maximum length. Correct the property and try again.
    * `The quantity must be a valid integer value.`\
      The quantity is not a valid integer value. Provide an integer value and try again.
    * `Use either salePrice or itemPrice.`\
      Either the `salePrice` or `itemPrice` is required.
    * `Overriding item-price is not enabled.`\
      Overriding the item price is not allowed for this site.
    * `The price override currency must be identical to the user session currency.`\
      The price override currency must be the same as the user session `currency`.
    * `The specified custom attributes are invalid and cannot be parsed.`\
      The format of the custom attributes is invalid. Correct the format of the custom attributes and try again.
    * `The subscription overrides expiration date is not valid.`\
      The `expirationDate` format is invalid. The format should be `yyyy-MM-dd'T'HH:m:ss.SSS'Z'`.
    * `The subscription overrides activation date is not valid.`\
      The `activationDate` format is invalid. The format should be `yyyy-MM-dd'T'HH:m:ss.SSS'Z'`.
    * `The subscription overrides perpetual unit price is not valid.`\
      The field `perpetualUnitPrice` should contain both `currencyCode` and `amount`.
    * `Perpetual unit price currency [{perpetual unit price currency}] is different from user currency [{user currency}].`\
      The perpetual unit price currency cannot be different from the user's currency.
    * `Perpetual unit price cannot be less than or equal to 0.`\
      The perpetual unit price cannot be less than or equal to 0. Correct the value for the perpetual unit price and try again.
    * `Subscription expiration date [{expiration date}] should be 24 hours later than the order submission date.`\
      The subscription expiration date should be 24 hours later than the order submission date.
    * `Subscription expiration date [{expiration date}] should be later than the subscription activation date [{activation date}].`\
      The expiration date of the subscription should be later than the activation date of the subscription.
    * `Attribute name or the value is missing.`\
      Some attribute names or values are missing. Provide the missing attributes or values and try again.
    * `Invalid input value for (field name).`\
      The input value for the specified field is invalid because it contains sensitive data.

## `INVALID_RETURN_REASON`

The Return reason is invalid. Provide a valid return reason and try again.

## `LINE_ITEM_CANNOT_BE_RESOLVED`

* Cannot resolve line item for the specified line-item ID. Verify the specified line item ID is correct and try again.
* The line item had a problem while fetching the expiration date for the specified line-item ID.

## `LINE_ITEM_EXPIRATION_DATE_EXCEEDS`

The line item exceeds the return window for the specified line-item ID. The specified line item cannot be returned through the self-service [Returns API](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Returns).

## `LINE_ITEM_HAS_LINE_LEVEL_SATISFACTION_REFUND`

The line item has a line-item level satisfaction refund for the specified line item ID. The line item is not eligible for a self-service return.

## `LINE_ITEM_IS_LINKED_TO_SUBSCRIPTION`

The line item is linked to a subscription. Cannot process the return for non-physical items.

## `LINE_ITEM_IS_NOT_PHYSICAL`

The specified line-item ID is not physical. Cannot process the return for items that are not physical.

## `LINE_ITEM_QTY_IDS_ARE_INVALID`

The specified line-item quantity IDs are not associated with the specified line item. Specify the correct line item quantity IDs for the specified line item and try again.

## `LINE_ITEM_QTY_IDS_MISSING_FOR_PARTIAL_RETURN`

The line-item quantity IDs for this partial return are missing. Specify the line item quantity IDs to include in the specified partial return and try again.

## `LINE_ITEM_QTY_IDS_NOT_ELIGIBLE_FOR_RETURN`

Specified line-item quantity IDs are not eligible for return for the specified line item ID. Verify the specified line-item quantity IDS are correct and try again if they are not correct.

## `LINE_ITEM_QUANTITY_TO_RETURN_IS_MORE_THAN_ALLOWED`

The quantity of line items to return is greater than the expected return quantity for the specified line-item ID. Specify a valid quantity of line items to return for the specified line-item ID and try again.

## `NO_LINE_ITEM_PRESENT_IN_REQUISITION`

The request contains no line items. The request must contain at least one line item. Include at least one line item in the request and try again.

## `NO_RETURN_REASON_CONFIGURED`

Return reasons for the specified order ID are missing. Provide the reasons for the returns and try again.

## `NULL_RETURN_REQUEST`

The return request cannot be null. Ensure the request is not null and try again.

## `ORDERID_CAN_NOT_BE_RESOLVED`

Cannot resolve the specified order ID for the order. Provide a valid order ID for the order and try again.

## `PARTIAL_PRODUCT_COMBINATION_RETURN`

The shopper wants to return part of a product combination. The shopper must return all components within the product combination. Return all line items associated with the product combination for specified requisition ID.

## `password-failure`

The provided password failed authentication for one of the following reasons:

* `Password must be between 8 - 32 characters.`The length of the password must between 8 - 32 characters.
* `Password must include three of the following: Upper case letter, lower case letter, numbers and the special characters: !@#$%^*~:;&><[]{}|-_+=?`\
  –Provided password shall follow the password rule.
* `Password must be alpha-numeric.`\
  Provided password shall follow the password rule.

## `REQUISITION_HAS_ORDER_LEVEL_SATISFACTION_REFUND`

The order has an order level satisfaction refund for a specified order ID. If an order has a satisfaction refund applied against it, the line items within that order are not eligible for return.

## `REQUISITION_NOT_ELIGIBLE_FOR_RETURN`

The specified order ID is not eligible for return. The requisition is in a state that does not allow a return to occur

## `RETURN_PROCESSING_ERROR`

An error occurred while processing the return for the specified order. Ensure the information is correct and try again.

## `RETURN_QUANTITY_CAN_NOT_LESS_THAN_ONE`

Line item return quantity must be greater than 0 for the specified line item. Specify a number greater than zero and less than or equal to the number of eligible items for the line item return quantity and try again.

## `SITE_DOESNOT_ACCEPT_RETURN`

The site does not accept returns. To enable returns for a site, contact your Digital River Representative.

## `UNABLE_TO_RESOLVE_SITE`

Cannot resolve the specified order ID for the order. Specify a valid site for the specified order ID.

## `validation-error`

An error occurred while validating the request for the following reason:

* `Missing required field`\
  The required data is missing. Provide the missing field and try again.
* `validation-failure`–Cannot validate the request for one of the following reasons:
  * The site does not accept the return.
  * The order is not in a returnable state.
  * The return window expired for the specified product.
  * The requested return quantity is greater than the eligible quantity for the line item.
  * Cannot return the specified line item through the self-service Returns API.
