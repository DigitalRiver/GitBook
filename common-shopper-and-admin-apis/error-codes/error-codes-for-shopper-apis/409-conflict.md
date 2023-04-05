---
description: Understand the 409 Conflict error codes.
---

# 409 Conflict

## `[resource]-already-exists`

Tried to create a \[resourceName] with an ID \[resourceId], and that resource already exists.

## `account_closed`

Stop all billing as this account is closed.

## `add-base-product-cart-error`

Cannot add base products to the cart. The possible error descriptions are as follows:

*   `Base products cannot be added to cart.`

    Base products cannot be added to the cart.

## `apply-payment-failure`

Cannot apply a payment method to an empty cart or failed to apply the requested payment method to the cart. The possible error descriptions are as follows:

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

## `apply-shopper-failure`

Cannot apply the shopper account information to the cart. The possible error descriptions are as follows:

*   `Shopper account information could not be applied to cart.`

    Cannot apply the shopper account information to the cart.
* `Billing Address country for request is invalid`–The country associated with the billing address for the request is invalid.

## `card_expired`

The card is expired.

## `card_limit_exceeded`

The transaction exceeds the card limit amount.

## `card_type_block`

The merchant has blocked this card type.

## `card_velocity_exceeded`

The transaction exceeds the card velocity amount.

## `cart-charge-failure`

The cart could not be processed due to a charge failure. The possible error descriptions are as follows:

* `Failed to charge source.`\
  Failed to charge the source.

## `cart-failure`

Some cart operation actions failed. The possible error descriptions are as follows:

*   `Unable to retrieve the cart details due to data inconsistency.`

    Failed to retrieve cart data.

## `cart-fraud-failure`

Cannot submit the order due to fraud validation failure. The possible error descriptions are as follows:

*   `The order could not be submitted due to fraud validation failure`

    The order could not be submitted due to a fraud validation failure.

## `cart-payment-failure`

Cannot submit the order due to payment processing failure. The possible error descriptions are as follows:

* `The order could not be submitted due to payment processing failure`\
  The order could not be submitted due to payment processing failure.
*   `The cart could not be processed due to payment processing failure`

    Cannot process the cart due to a payment processing failure.

## `credit-card-declined`

The credit card payment was declined.

## `credit-floor-exceeded`

The total amount for the order does not exceed the credit card minimum.

## `credit-card-expired`

The credit card used for payment has expired. The possible error descriptions are as follows:

*   `The credit card used for payment has expired`

    The credit card used for payment has expired.

## `concurrent-cart-modification-failure`

Concurrent cart modification is not allowed. The possible error descriptions are as follows:

*   `Request attempted to modify the cart while the cart was being updated by another request.`

    Two cart modification requests cannot occur at the same. Wait a little while and try again.

## `coupon-code-already-used`

The shopper previously entered this coupon code. The shopper cannot use this coupon code again.

## `declined`

The card has been declined for an unknown reason.

## `decline_do_not_retry`

The card has been declined for an unknown reason.

## `delete-payment-failure`

Cannot delete a payment method from a cart. The possible error descriptions are as follows:

* `A payment method cannot be deleted rom an empty cart.` Cannot delete a payment method from an empty cart.

## `do_not_honor`

The card issuing bank has declined this payment.

## `EMPTY_LINE_ITEM_ID`

The line-item ID is missing. Provide the line item ID and try again.

## `EMPTY_RETURN_REASON`

Provide a reason for the return and try again.

## `external-reference-ID-conflict`

The products use the same external reference ID \[erid-1234]: \[12345600, 12345700, 12345800]. Either use the actual product identifier in the request or ensure the external reference ID for each product is unique.

* `unable-to-determine-product-by-ERID`\
  The external reference ID is not unique.

## `field-too-long`

The field \[fieldName] is longer than the maximum length \[fieldMaxLength] allowed.

## `fraud`

The transaction has been identified by the issuing bank as fraudulent.

## `fraud_block`

The transaction has been identified by Digital River as fraudulent.

## `insufficient_funds`

The card has insufficient funds to complete the purchase.

## `invalid_address`

The address does not match the card network's records.

## `invalid_amount`

The amount is not accepted by the card network.

## `invalid-bill-to-country`

The country's billing or shipping address for the request is invalid. The possible error descriptions are as follows:

*   `Billing Address country for request is invalid`

    The country of billing address for the request is invalid.

## `invalid_card_bin`

The card BIN is invalid.

## `invalid_card_number`

The card number entered is invalid.

## `invalid-coupon`

The coupon code is invalid. The shopper cannot use the coupon code.

## `invalid-credit-card-expiration-date`

The credit card expiration date specified for the cart is invalid.

## `invalid-credit-card-number`

The credit card number specified for the cart is invalid.

## `invalid_currency`

This currency is not supported.

## `valid-currency-code`

The requested currency is not supported.

## `invalid_expiration_date`

The card is expired or the expiration date is invalid.

## `invalid-ip-address`

The format of the IP address is invalid. The possible error descriptions are as follows:

* `Requested ip address is not valid`—The format of the IP address is invalid. Provide a valid IP address and try again.

## `invalid-keyword-expression`

Invalid keyword expression: \[expression entered]

## `invalid-locale`

The requested locale is not valid.

## `invalid-offer-id`

The offer ID for the request is invalid.

* `offer-not applicable`\
  The always-triggered offer is not supported.

## `invalid-payment-failure`

Cannot process the cart because the payment methods were not set. The possible error descriptions are as follows:

*   `The cart could not be processed due to no available payment methods set`

    Cannot process the cart because the payment methods set is not available.

## `invalid-payment-method`

The cart does not support the specified payment method. The possible error descriptions are as follows:

*   `Payment method is not supported for this Site`

    The site does not support the specified payment method.

## `invalid_pin`

The PIN provided is invalid or incorrect.

## `invalid-product-id`

The product identifier is invalid.

## `invalid-request`

Request the missing required product identifier.

## `invalid_security_code`

The security code provided is invalid or incorrect.

## `invalid-ship-to-country`

The shipping address country is restricted for request. The possible error descriptions are as follows:

*   `Shipping Address country for request is invalid`

    The shipping address country for the request is invalid.

## `inventory-unavailable-error`

Inventory is unavailable for the product specified in the request.&#x20;

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

## `inventory-status-failure`

Inventory is unavailable for one or more of the products in the cart.

## `ip-address-restriction-error`

The country associated with the IP address for the request is restricted. The possible error descriptions are as follows:

* `Country for ip address is restricted for request`\
  The country associated with the IP address for the request is restricted.

## `issuer_invalid_card`

The card does not exist with the issuer.

## `issuer_not_found`

The card issuer does not exist.

## `issuer_unavailable`

The card issuing bank could not be reached.

## `limit_exceeded`

The transaction amount exceeds your assigned limit.

## `line-item-creation-failure`

Cannot create a line item for the specified product. The possible error descriptions are as follows:

*   `Line item could not be created.`

    The line item cannot be created.
*   `Your shopping cart is currently empty.`

    The shopping cart cannot be empty for line item creation.
*   `This product is no longer available.`

    The line item cannot be created because the product is not available.
* `Line Item could not be created for the product specified.`The product with provided product ID is not in the group to which the offer applies.

## `line-item-update-failure`

Cannot update the line item for the request. The possible error descriptions are as follows:

*   `Line Item could not be updated for the request`

    Cannot update the line item for the request.

## `lost_stolen_card`

The issuing bank has marked this card as lost or stolen.

## `mid_limit_exceeded`

The transaction amount exceeds the limit assigned for this MID.

## `no_response`

The payment processor did not respond.

## `offer-already-used`

The offer is already in use.

## `offer-not-active`

The offer for the request is not active.

## `offer-not-applicable`

Cannot apply the offer ID for the request to the cart.

## `offer-not-deployed`

Cannot use an undeployed coupon code.

## `offer-unavailable`

The offer ID for the request is not available for the cart.

## `offer-usage-limit-exceeded`

Exceeded the offer usage limit. Shoppers cannot use the coupon code.

## `operation-failed`

Cannot complete the operation. The possible error descriptions are as follows:

*   `Cart could not be established for request.`

    An error caused a cart establishment failure.
* `A service failure occurred that prevented the request from being processed`An error occurred during the process of determining the fulfiller.
* `TAX_000001`—The address verification failed during tax computation, such as ZIP or postal code, do not match.
* `Line item could not be determined. Multiple line items found for product`When the system was going to update the line item it found multiple line items of the product in the cart.
* `Quantity restrictions in place; minimum required quantity is [{minumum quantity}].`The product has a minimum purchasable quantity, and the requested quantity is less than the minimum purchasable quantity.
* `Purchase history restrictions in place; allowed quantity is [{maximum quantity}].`The requested quantity is greater than the maximum purchasable quantity of the product.
* `Exception occurred while checking ShippingMethod by ShippingMethodSetter`An exception occurred while checking the shipping method.

## `over-private-store-shopper-restriction`

Cannot add the product to the cart. The shopper requested more than the maximum purchasable quantity \[x], or the remaining purchasable quantity \[y] is less than the quantity they requested. The possible error descriptions are as follows:

* `Maximum purchasable quantity[{maximum quantity}]; Remaining purchasable quantity[{remaining purchasable quantity}]; The product cannot be added to the cart.` The sum of this request quantity and the quantity already purchased in the cart is over the maximum purchasable quantity when the product in a private store has a maximum purchasable quantity and the purchase history restriction setting is true.

## `payment-post-auth-failure`

The order could not be submitted due to payment processing failure.

## `paypal-failure`

Cannot process the cart because PayPal returned a failure or declined status.

## `paypal-lookup-failure`

Cannot process the cart due to a PayPal lookup processing failure. The possible error descriptions are as follows:

* `The cart could not be processed due to paypal lookup processing failure`\
  Cannot process the cart due to a PayPal lookup processing failure.

## `pin_try_exceeded`

The bank's allowable number of PIN tries has been exceeded.

## `precondition-failure`

The request failed on some precondition validations. The possible error descriptions are as follows:

* `Invalid offer level for applied offer with offer ID: {offerId}. Provide a valid offer level and try again.` The offer level for the applied offer with `offerId` is invalid.
* `Invalid offer type for applied offer with offer ID: {offerId}. Provide a valid offer type and try again.` The offer type for the applied offer with `offerId` is invalid.
* `Applied the wrong offer ID: {offerId} with the offer. Enter the correct offer ID and try again.` The trigger point for the applied offer with `offerId` is invalid.
* `Applied the wrong offer ID: {offerId} for this site. Enter the correct offer ID and try again.` The offer with `offerId` is unavailable.
* `The applied offer with offer ID: {offerId} is unavailable. Ensure the active offer is within the total usage limit and that the supported locale matches the user's locale and try again.` The applied offer with the provided `offerId` is unavailable.

## `private-store-remaining-quantity-under-line-item-restriction`

Cannot add the product to the cart. The shopper requested more than the Remaining purchasable quantity \[x] or less than the Minimum purchasable quantity \[y].

## `rate-limit-quota-exceeded`

Exceeded the quota for the allowed number of API requests.

## `restricted-bill-to-country`

The billing address country for the request is restricted. The possible error descriptions are as follows:

* `Billing Address country is restricted for request`The billing address country for the request is restricted.

## `restricted_card`

The use of this card has been restricted by the card network.

## `restricted-ship-to-country`

The shipping address country for the request is restricted. The possible error descriptions are as follows:

* `Shipping Address country is restricted for request`The shipping address country for the request is restricted.

## `resume-cart-failure`

The cart cannot be resumed. The possible error descriptions are as follows:

* `Requisition is not present or not in Source Pending Redirect state.`\
  Incorrect requisition state (not source\_pending\_redirect).
* `The pending redirect order could not be resumed.`\
  Incorrect payments session status (failed, cancelled, pending\_redirect, requires\_source).
* `The pending redirect order is no longer eligible for Resume API. Please use Order API to check current status.`\
  The order was transferred back to ODS.

## `shopper-usage-limit-exceeded`

The shopper exceeded the offer usage limit. The shopper cannot use the coupon code.

## `stop_recurring`

The cardholder has requested all recurring and/or installment charges be stopped.

## `submit-cart-failed`

The cart is not complete, so the shopper could not submit the cart. The possible error descriptions are as follows:

*   `Session cannot be null.`

    The session is null causing the submit cart to fail.
*   `A requisition cannot be null.`

    The requisition is null causing the submit cart to fail.
* `Terms of Sales Acceptance must be true so shopper confirmed the agreement.`The Terms of Sales Acceptance is not true causing the submit cart to fail.
* `Cannot use non-recurring payment method to purchase commitment type subscription`The requisition contains a subscription commit line item, and the payment source does not exist or is not reusable.
* `The cart is not complete and could not be submitted.`The cart is not complete causing the submit cart to fail.
* `The cart cannot be completed due to payment processing failure.`The cart cannot be completed due to a payment processing failure.

## `under-private-store-line-item-restriction`

The product in the private store has a minimum purchasable quantity, and the requested quantity is less than the minimum purchasable quantity.

* `Minimum purchasable quantity[x]; Cannot add the product to the cart.`

## `vat-exemption-failure`

The Rest of World tax exemption is not enabled for this site. [Enable Global Tax ID Management](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-site-settings.htm) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) and try again.

* `Tax Exemption Rest of World tax exemption is not enabled for this site.`

## `voice_authorization_required`

Voice authorization is required to approve the transaction.
