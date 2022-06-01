---
description: Learn how the Commerce API uses HTTP response status codes.
---

# Error codes

The Commerce API uses HTTP response status codes. These codes indicate whether an API request succeeded or failed. HTTP status codes group responses into the following classes:

* The `2xx` range indicates success.
* The `4xx` range indicates an error that failed based on the provided information provided (for example, you omitted a parameter, or a charge failed).
* The `5xx` range indicates an error with Digital River's servers.

Some errors `4xx` errors include an [error code](error-codes.md#error-codes). The error code is a short string with a brief explanation.

## Error format

Digital River uses the following format for errors:

```javascript
"errors": {
  "error": [
    {
      "relation": "https://api.digitalriver.com/v1/shoppers/SubmitCartResource",
      "code": "{error-code}",
      "subcode": "{error-subcode}",
      "description": "{error-description}"
    }
  ]
}
```

A basic error message (`error`) includes the following information:

* `code`–This parameter categorizes the failure reasons that look different but point to the same issue.
* `subcode`–This optional parameter appears when the system has more information about the error.
* `description`–A brief description of the error.

### Credit card error and declined message

A transaction error for a payment method such as a credit card saved in the payment source may contain additional information as shown in the following [declined message](https://docs.digitalriver.com/commerce-api/cart/submitting-a-cart/authorization-declines) (`declinedMessage`) example:

```javascript
"errors": {
    "error": [
        {
            "relation": "https://developers.digitalriver.com/v1/shoppers/SubmitCartResource",
            "code": "declined",
            "subcode": "fraud_block",
            "description": "The transaction has been identified by Digital River as fraudulent.",
            "declinedMessage": {
                "merchantDeclinedType": "Hard",
                "customerDeclinedType": "Hard",
                "code": "7011"
            }
        }
    ]
}
```

### Credit card error codes

The error codes for transactions using a credit card saved in the payment source are described below.

#### `declined`

The `declined` error code has the following subcodes:

* `account_frozen`–The account is frozen.
* `account_closed`–The account is closed.
* `authentication_required`–The transaction requires authentication.
* `blacklisted_card`–The credit card is blacklisted.
* `card_limit_exceeded`–The transaction exceeds the card limit amount.
* `card_not_active`–The card is not active yet.
* `card_type_block`–The merchant has blocked this card type.
* `card_velocity_exceeded`–The transaction exceeds the velocity amount.
* `declined`–The card has been declined for an unknown reason.
* `declined_can_retry`–The card has been declined for an unknown reason.
* `do_not_honor`–The card issuing bank has declined this payment.
* `duplicate_transaction`–The transaction is a duplicate.
* `fraud`–The transaction has been identified by the issuing bank as fraudulent.
* `fraud`–The transaction has been identified as fraudulent.
* `fraud_block`–The transaction has been identified by Digital River as fraudulent.
* `illegal_action`–The transaction has been identified as illegal.
* `insufficient_funds`–The card has insufficient funds to complete the purchase
* `invalid_amount`–The amount is not accepted by the card network.
* `invalid_currency`–The currency is not supported.
* `invalid_field_data`–The transaction contains invalid data.
* `invalid_merchant`–The merchant is invalid for this type of transaction.
* `invalid_payment_method`–The payment method used is invalid.
* `invalid_security_field`–The transaction contains invalid data.
* `invalid_transaction_type`–The transaction type is invalid.
* `issuer_unavailable`–The card does not exist with the issuer.
* `limit_exceeded`–The transaction amount exceeds your assigned limit.
* `lost_stolen_card`–The issuing bank has marked this card as lost or stolen.
* `mid_limit_exceeded`–The transaction amount exceeds the limit assigned for this MID.
* `new_card_issued`–New account information is available.
* `no_response`–The payment processor did not respond.
* `pin_try_exceeded`–The bank's allowable number of PIN tries has been exceeded.
* `restricted_card`–The use of this card has been restricted by the card network.
* `sca_not_completed`–The payment authorization was not initiated as the shopper did not successfully complete the authentication process.
* `stop_recurring`–Stop all billing as this account is closed.
* `suspected_fraud`–The issuer has identified this transaction potentially as fraudulent.
* `unidentified_error`–The card has been declined for an unknown reason.

#### `declined - contact bank`

The `declined - contact bank` error code has the following subcodes:

* `voice_authorization_required`–Voice authorization is required by the issuer.

#### `invalid`

The `invalid` error code has the following subcodes:

* `issuer_invalid_card`–The card does not exist with the issuer.

#### `invalid card`

The `invalid card` error code has the following subcodes:

* `card_expired`–The card is expired.
* `invalid_address`–The address does not match the card network's records.
* `invalid_card_number`–The card number entered is invalid.
* `invalid_card_bin`–The card bin is invalid.
* `invalid_expiration_date`–The card is expired or the expiration date is invalid.
* `invalid_pin`–The PIN provided is invalid or incorrect.
* `invalid_security_code`–The security code provided is invalid or incorrect.
* `issuer_not_found`–The card issuer does not exist.

### `declinedMessage`&#x20;

A `declinedMessage` includes the following information:

* `code`–This code helps to categorize failure reasons for the declined message that look different but point to the same issue.
* `merchantDeclinedType`–This field indicates the authentication decline type of transaction initiated by the merchant.
* `customerDeclinedType`–This field indicates the authentication decline type of transaction initiated by the shopper.

## Error codes

The following topics contain a list of API error codes.

### 400 Bad Request

* `dr_limited_token_invalid`–The limited token is invalid, expired, or revoked. Provide a valid token and try again.
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
* `INVALID_RETURN_REASON`–The Return reason is invalid. Provide a valid return reason and try again.
* `LINE_ITEM_CANNOT_BE_RESOLVED`–
  * Cannot resolve line item for the specified line-item ID. Verify the specified line item ID is correct and try again.
  * The line item had a problem while fetching the expiration date for the specified line-item ID.
* `LINE_ITEM_EXPIRATION_DATE_EXCEEDS`–The line item exceeds the return window for the specified line-item ID. The specified line item cannot be returned through the self-service [Returns API](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Returns).
* `LINE_ITEM_HAS_LINE_LEVEL_`\
  `SATISFACTION_REFUND`–The line item has a line-item level satisfaction refund for the specified line item ID. The line item is not eligible for a self-service return.
* `LINE_ITEM_IS_LINKED_TO_SUBSCRIPTION`–The line item is linked to a subscription. Cannot process the return for non-physical items.
* `LINE_ITEM_IS_NOT_PHYSICAL`–The specified line-item ID is not physical. Cannot process the return for items that are not physical.
* `LINE_ITEM_QTY_IDS_ARE_INVALID`–The specified line-item quantity IDs are not associated with the specified line item. Specify the correct line item quantity IDs for the specified line item and try again.
* `LINE_ITEM_QTY_IDS_MISSING_`\
  `FOR_PARTIAL_RETURN`–The line-item quantity IDs for this partial return are missing. Specify the line item quantity IDs to include in the specified partial return and try again.
* `LINE_ITEM_QTY_IDS_NOT_ELIGIBLE_`\
  `FOR_RETURN`–Specified line-item quantity IDs are not eligible for return for the specified line item ID. Verify the specified line-item quantity IDS are correct and try again if they are not correct.
* `LINE_ITEM_QUANTITY_TO_RETURN_`\
  `IS_MORE_THAN_ALLOWED`–The quantity of line items to return is greater than the expected return quantity for the specified line-item ID. Specify a valid quantity of line items to return for the specified line-item ID and try again.
* `NO_LINE_ITEM_PRESENT_IN_REQUISITION`–The request contains no line items. The request must contain at least one line item. Include at least one line item in the request and try again.
* `NO_RETURN_REASON_CONFIGURED`–Return reasons for the specified order ID are missing. Provide the reasons for the returns and try again.
* `NULL_RETURN_REQUEST`–The return request cannot be null. Ensure the request is not null and try again.
* `ORDERID_CAN_NOT_BE_RESOLVED`–Cannot resolve the specified order ID for the order. Provide a valid order ID for the order and try again.
* `PARTIAL_PRODUCT_COMBINATION_RETURN`–The shopper wants to return part of a product combination. The shopper must return all components within the product combination. Return all line items associated with the product combination for specified requisition ID.
* `password-failure`–The provided password failed authentication for one of the following reasons:
  * `Password must be between 8 - 32 characters.`The length of the password must between 8 - 32 characters.
  * `Password must include three of the following: Upper case letter, lower case letter, numbers and the special characters: !@#$%^*~:;&><[]{}|-_+=?`\
    –Provided password shall follow the password rule.
  * `Password must be alpha-numeric.`\
    Provided password shall follow the password rule.
* `SITE_DOESNOT_ACCEPT_RETURN`–The site does not accept returns. To enable returns for a site, contact your Digital River Representative.
* `REQUISITION_HAS_ORDER_LEVEL_`\
  `SATISFACTION_REFUND`–The order has an order level satisfaction refund for a specified order ID. If an order has a satisfaction refund applied against it, the line items within that order are not eligible for return.
* `REQUISITION_NOT_ELIGIBLE_FOR_RETURN`–The specified order ID is not eligible for return. The requisition is in a state that does not allow a return to occur
* `RETURN_PROCESSING_ERROR`–An error occurred while processing the return for the specified order. Ensure the information is correct and try again.
* `RETURN_QUANTITY_CAN_NOT_LESS_THAN_ONE`–Line item return quantity must be greater than 0 for the specified line item. Specify a number greater than zero and less than or equal to the number of eligible items for the line item return quantity and try again.
* `UNABLE_TO_RESOLVE_SITE`–Cannot resolve the specified order ID for the order. Specify a valid site for the specified order ID.
* `validation-error`–An error occurred while validating the request for the following reason:
  * `Missing required field`\
    The required data is missing. Provide the missing field and try again.
* `validation-failure`–Cannot validate the request for one of the following reasons:
  * The site does not accept the return.
  * The order is not in a returnable state.
  * The return window expired for the specified product.
  * The requested return quantity is greater than the eligible quantity for the line item.
  * Cannot return the specified line item through the self-service Returns API.

### 401 Unauthorized

* `invalid_client`–The provided client is invalid. Provide the correct client information and try again.
* `invalid_request`–The required parameter is missing or empty. Provide the missing parameter and try again.
*   `invalid_token`–Invalid token for the Shopper Session. The token is no longer valid and must be refreshed to continue making API calls. This error occurs when there is a bad Dispatch token or Global Commerce User API token. To resolve this error, issue an API call to identify where the token originated and when it expired, for example:

    \
    `GET /oauth20/access-tokens?token=your_access_token HTTP/1.1 Host: api.digitalriver.com`



    Where `your_access_token` is a placeholder for the actual token.

    The response shows you where the token originated in the `domain` field and when it expired in the `expiresIn` field. The possible error descriptions are as follows:

    *   `Invalid token for specified shopper`

        The provided token is invalid for the specified shopper.
    * `Session expired`–The shopper session is expired. Try refreshing the token.
    *   `Request Site ID does not match Token Site ID`

        The value of the Header `siteId` does not match the site ID in the token.
    *   `Invalid Token for Shapper Session`

        The provided token is invalid.

### 403 Forbidden&#x20;

* `forbidden`–Cannot complete the request, as the call is not permitted.

### 404 Not Found

* `duplicate_offer_identifier`–The system gets duplicated offer identifier (offer ID or offer external reference ID) from the request. The possible error descriptions are as follows:
  * `Use either offer ID or offer external reference ID in the Applied Offers payload and try again.`\
    Provide either the offer ID or the offer external reference ID. You cannot provide both.
* `duplicate_product_identifier`–The system gets duplicated product identifier (product ID or product external reference ID) from the request. The possible error descriptions are as follows:
  *   `Use either product ID or product external reference ID in the Applied Offers payload and try again.`

      Provide either the product ID or the product external reference ID. You cannot provide both.
* `invalid-offer-id`–The offer ID for the request is invalid. The possible error descriptions are as follows:
  * `The offer ID: {offerID} for the request is invalid. Provide a valid offer ID or Offer external reference ID and try again.`The offer ID for the request is invalid.
  * `The offer external reference ID: {offerId} for the request is invalid. Provide a valid offer ID or Offer external reference ID and try again.` The external reference ID for the request is invalid.
* `no-offer-identifier`–The system cannot get an offer identifier (offer ID or offer external reference Id) from the request. The possible error descriptions are as follows:
  * `The offer ID or offer external reference ID is missing. Provide the offer ID or external reference ID and try again.`Provide the offer ID or external reference ID.
  * `Use either offer ID or offer external reference ID in the Applied Offers payload and try again.`Provide either the offer ID or offer external reference ID. You cannot provide both.
* `no-offer-identifier`–The system cannot get an offer identifier (offer ID or offer external reference Id) from the request. The possible error descriptions are as follows:
  * `The offer ID or offer external reference ID is missing. Provide the offer ID or external reference ID and try again.`Provide the offer ID or external reference ID.
  * `Use either offer ID or offer external reference ID in the Applied Offers payload and try again.`Provide either the offer ID or the offer external reference ID. You cannot provide both.
* `no-product-identifier`–The system cannot get the product identifier (product ID or product external reference ID) from the request. The possible error descriptions are as follows:
  * `The product ID or product external reference ID is missing. Provide the product ID or external reference ID and try again.`Provide the product ID or product external reference ID.
* `resource-not-found`–Could not find a \[resourceName] resource with an internal ID \[resourceId]. The possible error descriptions are as follows:
  * `Invalid site for specified company`\
    The company of the site with the provided header `siteId` and the one with the provided header `companyId` are different, but they should be the same one.
  *   `Could not find a Line Item with an id of {line item id}`

      Could not find the line item for the provided ID.
  *   `Could not find an Order with an id of {orderId}`

      Could not find the order for the provided ID.
  * `A Cart identifier for the provided value of \"298407701971\" is not valid.` The cart identifier (`cartId`) is not valid. Provide the correct value for the `cartId` and try again.

### 405 Method Not Allowed

* `method-not-allowed`
  * OAuth API–Request used incorrect HTTP method.
  * Shopper API–The method is not allowed.

### 409 Conflict

* `[resource]-already-exists`–Tried to create a \[resourceName] with an ID \[resourceId], and that resource already exists.
* `account_closed`–Stop all billing as this account is closed.
* `add-base-product-cart-error`–Cannot add base products to the cart. The possible error descriptions are as follows:
  *   `Base products cannot be added to cart.`

      Base products cannot be added to the cart.
* `apply-payment-failure`–Cannot apply a payment method to an empty cart or failed to apply the requested payment method to the cart. The possible error descriptions are as follows:
  *   `The shopper must have an approved line of credit account.`

      Apply payment failure due to the shopper having no approved line of credit account.
  *   `The line of credit account is not available.`

      The line of credit account is not available causing shopper applying failure.
  *   `Insufficient credit balance available.`

      There is no sufficient credit balance available.
  *   `Purchase amount does not meet minimum requirements.`

      The total purchase amount of the requisition is less than the minimal amount setting of the site.
  * `A payment method cannot be detached from an empty cart.` Cannot detach a payment method from an empty cart.
  * `The source with id [{souce_id}] was not found.` Cannot find the source with ID `{source_id}`.
* `apply-shopper-failure`–Cannot apply the shopper account information to the cart. The possible error descriptions are as follows:
  *   `Shopper account information could not be applied to cart.`

      Cannot apply the shopper account information to the cart.
* `Billing Address country for request is invalid`–The country associated with the billing address for the request is invalid.
* `card_expired`–The card is expired.
* `card_limit_exceeded`–The transaction exceeds the card limit amount.
* `card_type_block`–The merchant has blocked this card type.
* `card_velocity_exceeded`–The transaction exceeds the card velocity amount.
* `cart-charge-failure`–The cart could not be processed due to a charge failure. The possible error descriptions are as follows:
  * `Failed to charge source.`\
    Failed to charge the source.
* `cart-failure`–Some cart operation actions failed. The possible error descriptions are as follows:
  *   `Unable to retrieve the cart details due to data inconsistency.`

      Failed to retrieve cart data.
* `cart-fraud-failure`–Cannot submit the order due to fraud validation failure. The possible error descriptions are as follows:
  *   `The order could not be submitted due to fraud validation failure`

      The order could not be submitted due to a fraud validation failure.
* `cart-payment-failure`–Cannot submit the order due to payment processing failure. The possible error descriptions are as follows:
  * `The order could not be submitted due to payment processing failure`\
    The order could not be submitted due to payment processing failure.
  *   `The cart could not be processed due to payment processing failure`

      Cannot process the cart due to a payment processing failure.
* `credit-card-declined`–The credit card payment was declined.
* `credit-floor-exceeded`–The total amount for the order does not exceed the credit card minimum.
* `credit-card-expired`–The credit card used for payment has expired. The possible error descriptions are as follows:
  *   `The credit card used for payment has expired`

      The credit card used for payment has expired.
* `concurrent-cart-modification-failure`–Concurrent cart modification is not allowed.The possible error descriptions are as follows:
  *   `Request attempted to modify the cart while the cart was being updated by another request.`

      Two cart modification requests cannot occur at the same. Wait a little while and try again.
* `coupon-code-already-used`–The shopper previously entered this coupon code. The shopper cannot use this coupon code again.
* `declined`–The card has been declined for an unknown reason.
* `decline_do_not_retry`–The card has been declined for an unknown reason.
* `delete-payment-failure`–Cannot delete a payment method from a cart. The possible error descriptions are as follows:
  * `A payment method cannot be deleted rom an empty cart.` Cannot delete a payment method from an empty cart.
* `do_not_honor`–The card issuing bank has declined this payment.
* `EMPTY_LINE_ITEM_ID`–The line-item ID is missing. Provide the line item ID and try again.
* `EMPTY_RETURN_REASON`–for the return and try again.
* `field-too-long`–The field \[fieldName] is longer than the maximum length \[fieldMaxLength] allowed.
* `fraud`–The transaction has been identified by the issuing bank as fraudulent.
* `fraud_block`–The transaction has been identified by Digital River as fraudulent.
* `insufficient_funds`–The card has insufficient funds to complete the purchase.
* `invalid_address`–The address does not match the card network's records.
* `invalid_amount`–The amount is not accepted by the card network.
* `invalid-bill-to-country`–The country's billing or shipping address for the request is invalid. The possible error descriptions are as follows:
  *   `Billing Address country for request is invalid`

      The country of billing address for the request is invalid.
* `invalid_card_bin`–The card BIN is invalid.
* `invalid_card_number`– card number entered is invalid.
* `invalid-coupon`–The coupon code is invalid. The shopper cannot use the coupon code.
* `invalid-credit-card-expiration-date`–The credit card expiration date specified for the cart is invalid.
* `invalid-credit-card-number`–The credit card number specified for the cart is invalid.
* `invalid_currency`–This currency is not supported.
* `valid-currency-code`–The requested currency is not supported.
* `invalid_expiration_date`–The card is expired or the expiration date is invalid.
* `invalid-ip-address`–The format of the IP address is invalid. The possible error descriptions are as follows:
  * `Requested ip address is not valid`—The format of the IP address is invalid. Provide a valid IP address and try again.
* `invalid-keyword-expression`–Invalid keyword expression: \[expression entered]
* `invalid-locale`–The requested locale is not valid.
* `id-offer-id`–The offer ID for the request is invalid.
* `invalid-payment-failure`–Cannot process the cart because the payment methods were not set. The possible error descriptions are as follows:
  *   `The cart could not be processed due to no available payment methods set`

      Cannot process the cart because the payment methods set is not available.
* `invalid-payment-method`–The cart does not support the specified payment method. The possible error descriptions are as follows:
  *   `Payment method is not supported for this Site`

      The site does not support the specified payment method.
* `invalid_pin`–The PIN provided is invalid or incorrect.
* `invalid-product-id`–`invalid-product-id`
* `invalid-request`–Request the missing required product identifier.
* `invalid_security_code`–The security code provided is invalid or incorrect.
* `invalid-ship-to-country`–The shipping address country is restricted for request. The possible error descriptions are as follows:
  *   `Shipping Address country for request is invalid`

      The shipping address country for the request is invalid.
* `invalid-token`–The request contains an invalid token.
* `invalid_transaction_type`–The transaction type is invalid.
*   `inventory-unavailable-error`–Inventory is unavailable for the product specified in the request.&#x20;

    The possible error descriptions are as follows:

    *   `We're sorry but {product_name} is currently out of stock and cannot be added to your cart. We apologize for any inconvenience.`

        The product cannot be added to the cart because it is out of stock.
    *   `Were sorry but there is not enough of this product in stock to complete this order. Please update your quantities and proceed to checkout.`

        The inventory quantity is not enough to complete this order.
    *   `We are sorry, some products are out of stock and unavailable for purchase at this time`

        Some products are out of stock for a bundled child with a tight bundle policy. The following description appears in the subcode: `inventory-unavailable-to-add-tight-bundle-child-line-item`
    *   `We're sorry but {product_name} is currently out of stock and cannot be added to your cart. We apologize for any inconvenience.`

        Some products are out of stock for a bundled child with a semi-tight bundle policy. The following description appears in the subcode `inventory-unavailable-to-add-semi-tight-bundle-child-line-item`.
    *   `We are sorry, but the following products are currently out of stock and cannot be added to your cart: {product_name}. We apologize for any inconvenience.`

        Some products are out of stock for a bundled child with a semi-tight bundle policy. The following description appears in the subcode: `inventory-unavailable-to-add-semi-tight-bundle-child-line-item`
* `inventory-status-failure`–Inventory is unavailable for one or more of the products in the cart.
* `ip-address-restriction-error`–The country associated with the IP address for the request is restricted. The possible error descriptions are as follows:
  * `Country for ip address is restricted for request`\
    The country associated with the IP address for the request is restricted.
* `issuer_invalid_card`–The card does not exist with the issuer.
* `issuer_not_found`–The card issuer does not exist.
* `issuer_unavailable`–The card issuing bank could not be reached.
* `limit_exceeded`–The transaction amount exceeds your assigned limit.
* `line-item-creation-failure`–Cannot create a line item for the specified product. The possible error descriptions are as follows:
  *   `Line item could not be created.`

      The line item cannot be created.
  *   `Your shopping cart is currently empty.`

      The shopping cart cannot be empty for line item creation.
  *   `This product is no longer available.`

      The line item cannot be created because the product is not available.
  * `Line Item could not be created for the product specified.`The product with provided product ID is not in the group to which the offer applies.
* `line-item-update-failure`–Cannot update the line item for the request. The possible error descriptions are as follows:
  *   `Line Item could not be updated for the request`

      Cannot update the line item for the request.
* `lost_stolen_card`–The issuing bank has marked this card lost or stolen.
* `mid_limit_exceeded`–The transaction amount exceeds the limit assigned for this MID.
* `no_response`–The payment processor did not respond.
* `offer-already-used`–The offer is already in use.
* `offer-not-active`–The offer for the request is not active.
* `offer-not-applicable`–Cannot apply the offer ID for the request to the cart.
* `offer-not-deployed`–Cannot use an undeployed coupon code.
* `offer-unavailable`–The offer ID for the request is not available for the cart.
* `offer-usage-limit-exceeded`–Exceeded the offer usage limit. Shoppers cannot use the coupon code.
* `operation-failed`–Cannot complete the operation. The possible error descriptions are as follows:
  *   `Cart could not be established for request.`

      An error caused a cart establishment failure.
  * `A service failure occurred that prevented the request from being processed`An error occurred during the process of determining the fulfiller.
  * `TAX_000001`—The address verification failed during tax computation, such as ZIP or postal code, do not match.
  * `Line item could not be determined. Multiple line items found for product`When the system was going to update the line item it found multiple line items of the product in the cart.
  * `Quantity restrictions in place; minimum required quantity is [{minumum quantity}].`The product has a minimum purchasable quantity, and the requested quantity is less than the minimum purchasable quantity.
  * `Purchase history restrictions in place; allowed quantity is [{maximum quantity}].`The requested quantity is greater than the maximum purchasable quantity of the product.
  * `Exception occurred while checking ShippingMethod by ShippingMethodSetter`An exception occurred while checking the shipping method.
* `over-private-store-shopper-restriction`–Cannot add the product to the cart. The shopper requested more than the maximum purchasable quantity \[x], or the remaining purchasable quantity \[y] is less than the quantity they requested. The possible error descriptions are as follows:
  * `Maximum purchasable quantity[{maximum quantity}]; Remaining purchasable quantity[{remaining purchasable quantity}]; The product cannot be added to the cart.`The sum of this request quantity and the quantity already purchased in the cart is over the maximum purchasable quantity when the product in a private store has a maximum purchasable quantity and the purchase history restriction setting is true.
* `payment-post-auth-failure`–The order could not be submitted due to payment processing failure.
* `paypal-failure`–Cannot process the cart because PayPal returned a failure or declined status.
* `paypal-lookup-failure`–Cannot process the cart due to a PayPal lookup processing failure. The possible error descriptions are as follows:
  * `The cart could not be processed due to paypal lookup processing failure`\
    Cannot process the cart due to a PayPal lookup processing failure.
* `pin_try_exceeded`–The bank's allowable number of PIN tries has been exceeded.
* `private-store-remaining-quantity-under-line-item-restriction`–Cannot add the product to the cart. The shopper requested more than the Remaining purchasable quantity \[x] or less than the Minimum purchasable quantity \[y].
* `rate-limit-quota-exceeded`–Exceeded the quota for the allowed number of API requests.
* `restricted-bill-to-country`–The billing address country for the request is restricted. The possible error descriptions are as follows:
  * `Billing Address country is restricted for request`The billing address country for the request is restricted.
* `restricted_card`–The use of this card has been restricted by the card network.
* `restricted-ship-to-country`–The shipping address country for the request is restricted. The possible error descriptions are as follows:
  * `Shipping Address country is restricted for request`The shipping address country for the request is restricted.
*   `resume-cart-failure`–

    The cart cannot be resumed. The possible error descriptions are as follows:

    * `Requisition is not present or not in Source Pending Redirect state.`\
      Incorrect requisition state (not source\_pending\_redirect).
    * `The pending redirect order could not be resumed.`\
      Incorrect payments session status (failed, cancelled, pending\_redirect, requires\_source).
    * `The pending redirect order is no longer eligible for Resume API. Please use Order API to check current status.`\
      The order was transferred back to ODS.
* `shopper-usage-limit-exceeded`–The shopper exceeded the offer usage limit. The shopper cannot use the coupon code.
* `stop_recurring`–The cardholder has requested all recurring and/or installment charges be stopped.
* `submit-cart-failed`–The cart is not complete, so the shopper could not submit the cart. The possible error descriptions are as follows:
  *   `Session cannot be null.`

      The session is null causing the submit cart to fail.
  *   `A requisition cannot be null.`

      The requisition is null causing the submit cart to fail.
  * `Terms of Sales Acceptance must be true so shopper confirmed the agreement.`The Terms of Sales Acceptance is not true causing the submit cart to fail.
  * `Cannot use non-recurring payment method to purchase commitment type subscription`The requisition contains a subscription commit line item, and the payment source does not exist or is not reusable.
  * `The cart is not complete and could not be submitted.`The cart is not complete causing the submit cart to fail.
  * `The cart cannot be completed due to payment processing failure.`The cart cannot be completed due to a payment processing failure.
* `under-private-store-line-item-restriction`–`Minimum purchasable quantity[x]; Cannot add the product to the cart.`The product in the private store has a minimum purchasable quantity, and the requested quantity is less than the minimum purchasable quantity.
*   `vat-exemption-failure`–`Tax Exemption Rest of World tax exemption is not enabled for this site.`

    The Rest of World tax exemption is not enabled for this site. [Enable Global Tax ID Management](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-site-settings.htm) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) and try again.
* `voice_authorization_required`–Voice authorization is required by the issuer.

### 412 Precondition Failed

* `invalid-discount`–The value of the discount is invalid. The possible error descriptions are as follows:
  * `The discount value is invalid. Provide a valid discount value and try again.`The discount value is invalid for one of the following reasons:
    * The value of `discount` is less than 0
    * The value of `discount` is over the maximum value of DOUBLE when `discountType` is `amountOff`.
    * The value of `discount` is greater than 100 when `discountType` is `percentOff`.
* `invalid-discount-type`–The value of the discount type is invalid. The possible error descriptions are as follows:
  * `The offer discount type is invalid. Provide a valid offer discount type and try again.`The value of `discountType` shall be `amountOff` or `percentOff`.
* `invalid-product-id`–The product ID is invalid. The possible error descriptions are as follows:
  * `The product ID or product external reference ID is invalid. Provide the correct product ID or product external reference ID and try again.`The product ID or product for external reference ID is invalid.
* `no-discount-or-type`–The validation failed for `discount` or `discountType`. The possible error descriptions are as follows:
  * `Either the discount or discount type or both are missing. Include both the discount and discount type in the payload and try again.`Need to provide `discount` and `discountType`.
  * `precondition-failure`–The request failed on some precondition validations.  The possible error descriptions are as follows:
    * `Invalid offer level for applied offer with offer ID: {offerId}. Provide a valid offer level and try again.`The offer lever for applied offer with `offerId` is invalid.
    * `Invalid offer type for applied offer with offer ID: {offerId}. Provide a valid offer type and try again.`\
      The offer type for the applied offer with `offerId` is invalid.
    * `Applied the wrong offer ID with the offer. Enter the correct offer ID and try again.`The trigger point for the applied offer with `offerId` is invalid.
    * `Applied the wrong offer ID for this site. Enter the correct offer ID and try again.`The offer with the specified `offerId` is unavailable.
    * `The applied offer with offer ID: {offerId} is unavailable. Ensure the active offer is within the total usage limit and that the supported locale matches with user's locale and try again.`The applied offer with provided ID is unavailable.

### 413 Request Entity Too Large

* `custom_descriptions_exceeds_limitation`–The length of the `customDescription` exceeds the limitation. The possible error descriptions are as follows:
  * `The custom description for the offer exceeds length limitation (2000). Shorten the custom description and try again.`\
    The length of the `customDescription` cannot exceed the length limitation (2000).

### 500 Internal Server Error

* `system-error`–An unexpected system error occurred.
* `internal-payment-error`–An internal server error occurred, try again later.
