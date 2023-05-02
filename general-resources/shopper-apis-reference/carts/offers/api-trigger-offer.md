---
description: Learn more about the API trigger offer.
---

# API trigger offer

## API trigger offer source

### Cart

The cart object contains the cart information by line items and applied order offers.

### Line items

The `lineItems` object contains information on each line item and applied product offers.

#### Line item

A single line in a cart. At a minimum, a line item contains a single product identifier and quantity.

The `lineItem` is an array of objects that contains product information and quantity.

* **Quantity**: The `quantity` is the number of products added to the cart. The value must be a valid integer. If the quantity is not explicitly specified, the default is 1.
* **Product**: The product is an array that contains the [product identifier](../../../common-shoppers-and-admin-apis-reference/product-identifier.md).
  * **id**: the product identifier.
* **Subscription information**: The `subscriptionInfo` object contains the base information-related data for an external subscription engine. Available for [third-party subscription engine support only](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Third-Party-Subscription-Engine-Support/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(subscriptionInfo\)/post).
  * **Automatic renewal**: When set to `true`, the `autoRenewal` indicates the subscription will renew automatically (as opposed to manually).
  * **Terms**: The `terms` describe the recurring purchase terms for the customer.
  * **Free trial**: When set to true, the `freeTrial` indicates the subscription is a free trial.
  * **Start time**: The subscription's start date in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format (`yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`).
  * **End time**: The subscription's end date in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format (`yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`).
  * **Billing agreement identifier**: The `billingAgreementId` is the Digital River billing agreement ID. It represents the terms the customer agreed to when they stored their card details or applied them to any recurring purchase. The agreement ID can then be referenced for subsequent purchases, which allows us to tie them together.
* **Billing optimization**: The `billingOptimization` object is the ECO (Expired Card Optimizer) billing optimization tool for a 3rd party subscription. Available for third-party[ subscription engine support only](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Third-Party-Subscription-Engine-Support/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(subscriptionInfo\)/post).
  * **Subscription identifier**: The `subscriptionId` is the subscription's identifier.
  * **Segment identifier**: The `segmentId` is the unique segment identifier for each renewal term. For example, you can set the initial acquisition to `1`. After that, you can increment the renewal term identifier value by 1 for each additional renewal term.
  * **Renewal attempt number**: The `renewalAttemptNumber` is the billing attempt number for the current renewal. The value should reset to `1` after every successful renewal.&#x20;

#### Charge type

When using a third-party subscription engine, use the `chargeType` field to specify the transaction's charge type. Provide this value with the `subscriptionInfo` object in the request body. The `chargeType` value will be ignored if the object is absent in the request. The valid enums are:

* **customer\_initiated**: The customer initiates the transaction, such as the first purchase of a subscription order.
* **merchant\_initiated**: The merchant initiates the transaction, such as automatically renewing a subscription.&#x20;
* **moto**: Customer service initiates the transactions such as a mail order or telephone order (moto).

Available for [third-party subscription engine support only](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Third-Party-Subscription-Engine-Support/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(subscriptionInfo\)/post).

#### Applied product offers

The `appliedProductOffer` object contains an offer, and/or shipping offer applies to the product.

* **Offer**: This object contains either the offer identifier (`offerId`) or the external reference identifier (`externalReferenceId`) and a custom description (`customDescription`) of the offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.
* **Shipping offer**: This object contains either the offer identifier (`offerId`) or the external reference identifier (`externalReferenceId`) and a custom description (`customDescription`) of the shipping offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.

### Applied order offers

The `appliedOrderOffers` object contains an offer and/or shipping offer as applicable for the order.

#### **Offer**

This object contains either the offer identifier (`offerId`) or the [external reference identifier](../../../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) (`externalReferenceId`) and a custom description (`customDescription`) of the offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.

#### **Shipping offer**

This object contains either the offer identifier (`offerId`) or the [external reference identifier](../../../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) (`externalReferenceId`) and a custom description (`customDescription`) of the shipping offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.

## API trigger offer query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of API trigger offers. The following topics describe the query parameters for the apply-payment-method by [cart ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(API%20Trigger%20Offer\)/post)and line item. For more information on how to use query parameters, see [Fields and query parameters](../../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Skip offer arbitration

Use [`skipOfferArbitration`](../../../../shopper-apis/cart/managing-offers-in-a-cart/dynamic-offers-personalization/overriding-a-promotional-url-offer-discount.md#skip-offer-arbitration-flag) to enable or disable the Global Commerce Merchandising Offer arbitration logic. When enabled (set to `true`), Digital River disables the skip offer arbitration to find the best price for a product and displays the base price. When disabled (set to `false`), Digital River enables the skip offer arbitration to find the best price, and the best offer wins.
