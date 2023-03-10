---
description: Learn more about the carts resource.
---

# Carts

The [Carts ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts)resource provides access to a customer's cart and cart data. Use the Cart resource to get, update, or modify a cart.

{% hint style="danger" %}
**Important**: All methods in this API require an anonymous (limited access) or authenticated (full access) token.
{% endhint %}

<figure><img src="../../.gitbook/assets/2a56cbc-Digital_River_Demo_Online_Store_Checkout_cart.png" alt=""><figcaption></figcaption></figure>

## API trigger offer source

### Cart

The cart object contains the cart information by line items and applied order offers.

### Line items

The `lineItems` object contains information on each line item and applied product offers.

#### Line item

A single line in a cart. At a minimum, a line item contains a single product identifier and quantity.

The `lineItem` is an array of objects that contains product information and quantity.

* **Quantity**: The `quantity` is the number of products added to the cart. The value must be a valid integer. If the quantity is not explicitly specified, the default is 1.
* **Product**: The product is an array that contains the [product identifier](../common-shoppers-and-admin-apis-reference/product-identifier.md).
  * **id**: the product identifier.
* **Subscription information**: The `subscriptionInfo` object contains the base information related data for an external subscription engine. Available for [third party subscription engine support only](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Third-Party-Subscription-Engine-Support/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(subscriptionInfo\)/post).
  * **Automatic renewal**: When set to `true`, the `autoRenewal` indicates the subscription will renew automatically (as opposed to manually).
  * **Terms**: The `terms` describe the recurring purchase terms for the customer.
  * **Free trial**: When set to true, the `freeTrial` indicates the subscription is a free trial.
  * **Start time**: The subscription's start date in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format (`yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`).
  * **End time**: The subscription's end date in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format (`yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`).
  * **Billing agreement identifier**: The `billingAgreementId` is the Digital River billing agreement ID. It represents the terms the customer agreed to when they stored their card details or chose to apply them to any kind of recurring purchase. The ID of the agreement can then be referenced for subsequent purchases, which gives us the ability to tie them together.
* **Billing optimization**: The `billingOptimization` object is the ECO (Expired Card Optimizer) billing optimization tool for a 3rd party subscription. Available for [third party subscription engine support only](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Third-Party-Subscription-Engine-Support/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(subscriptionInfo\)/post).
  * **Subscription identifier**: The `subscriptionId` is the subscription's identifier.
  * **Segment identifier**: The `segmentId` is the unique segment identifier for each renewal term. For example, you can set the initial acquisition to `1`. Thereafter, you can increment the renewal term identifier value by 1 for each additional renewal term.
  * **Renewal attempt number**: The `renewalAttemptNumber` is the billing attempt number for the current renewal. The value should reset to `1` after every successful renewal.&#x20;

#### Charge type

When using a third party subscription engine, use the `chargeType` field to specify the transaction's charge type. Provide this value with the `subscriptionInfo` object in the request body. If the `subscriptionInfo` object is not present in the request, the `chargeType` value will be ignored. The valid enums are:

* **customer\_initiated**: The customer initiates the transaction such as the first purchase of a subscription order.
* **merchant\_initiated**: The merchant initiates the transaction such as automatically renewing a subscription.&#x20;
* **moto**: Customer service initiates the transactions such as a mail order or telephone order (moto).

Available for [third party subscription engine support only](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Third-Party-Subscription-Engine-Support/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(subscriptionInfo\)/post).

#### Applied product offers

The `appliedProductOffer` object contains an offer and/or shipping offer as applicable for the product.

* **Offer**: This object contains either the offer identifier (`offerId`) or the [external reference identifier](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) (`externalReferenceId`) and a custom description (`customDescription`) of the offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.
* **Shipping offer**: This object contains either the offer identifier (`offerId`) or the [external reference identifier](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) (`externalReferenceId`) and a custom description (`customDescription`) of the shipping offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.

### Applied order offers

The `appliedOrderOffers` object contains an offer and/or shipping offer as applicable for the order.

#### **Offer**

This object contains either the offer identifier (`offerId`) or the [external reference identifier](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) (`externalReferenceId`) and a custom description (`customDescription`) of the offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.

#### **Shipping offer**

This object contains either the offer identifier (`offerId`) or the [external reference identifier](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) (`externalReferenceId`) and a custom description (`customDescription`) of the shipping offer. Use `externalReferenceId` only if your site enforces a unique offer ERID.

## API trigger offer query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of API trigger offers. The following topics describe the query parameters available for the apply-payment-method by [cart ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(API%20Trigger%20Offer\)/post)and line-item. For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Skip offer arbitration

Use [`skipOfferArbitration` ](../../shopper-apis/cart/managing-offers-in-a-cart/dynamic-offers-personalization/overriding-a-promotional-url-offer-discount.md#skip-offer-arbitration-flag)to enable or disable the Global Commerce Merchandising Offer arbitration logic. When enabled (set to `true`), Digital River disables the skip offer arbitration to find the best price for a product and displays the base price. When disabled (set to `false`), Digital River enables the skip offer arbitration to find the best price and the best offer wins.

## Apply or detach payment method query parameters

The following describes the query parameters for [apply-payment-method](carts.md#apply-payment-method-query-parameters).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Token

The `token` is the authorized or anonymous token for the shopper.

## Apply shipping option query parameters

The following describes the query parameters for [apply-shipping-option](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shipping-Option).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Shipping option identifier

The `shippingOptionId` is the shipping option identifier for the cart.

### Token

The `token` is the authorized or anonymous token for the shopper.

## Apply shopper query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of shopper information. The following topics describe the query parameters available for the [apply-shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Billing address identifier

The `billingAddressId` identifies the shopper's address resource. If no value is provided, Digital River uses the shopper's default address.

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Payment option identifier

The `paymentOptionId` is the payment option identifier for a specific payment method. Digital River uses this value when a shopper selects a payment method and applies it to their cart. If the shopper does not select a payment method, Digital River uses the shopper's default payment option.

### Shipping address identifier

The `shippingAddressId` is the identifier of a shopper address resource to use as the shipping address. If neither shipping nor a billing address is provided, the default address for the shopper is used. Otherwise, the billing address ID (if provided) is applied as the default shipping address.

### Token

The `token` is the authorized token for the shopper.

## Billing and shipping address query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of billing and shipping addresses. The following topics describe the query parameters available for the [billing address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address) and [shipping address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Address). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Country

The `country` is a two-digit [ISO 3166-2](https://en.wikipedia.org/wiki/ISO\_3166-2) country code.

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Postal code

The `postalCode` is the postal code. For United States addresses, Digital River supports ZIP+4 codes. They consist of the last four digits of a full nine-digit ZIP code. A nine-digit ZIP Code has two parts: the initial five digits of the zip code indicating the destination post office or delivery area and the last four digits representing a specific delivery route within that overall delivery area.

### Token

The `token` is the authorized or anonymous token for the shopper.

## Cart resource

The following describes some of the key attributes for a [cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post).

### Billing Address

The `billingAddress` object contains the shopper's billing information.

### Charge type

The `chargeType` specifies the charge type for the transaction. The valid values are:

* `customer_initiated`: The shopper initiates the transaction. For example, when shopper first purchases the subscription.
* `merchant_initiated`: The merchant initiates the transaction. For example, when the subscription automatically renews.
* `moto`: Customer service initiates the transaction. For example, a mail order or telephone order transaction.

### Custom attributes

The `customAttributes` is an object that list the default custom attributes.

### IP address

The `ipAddress` is the shopper's IP address for the current session.

### Line items

The `lineItems` is an object containing the line items associated with the cart.

#### Line item

The `lineItem` is an array of ofobjects that define the line item.

* **Quantity**: The `quantity` is the number of products added to the cart. The value must be a valid integer. If the quantity is not explicitly specified, the default is 1.
* **Product**: The `product` object.
  * `id`: The [product identifier](../common-shoppers-and-admin-apis-reference/product-identifier.md).
* **Custom attributes**: An customAttributes object contains the default custom attributes.
  * `attribute`: An `attribute` is an array of objects that define the specific qualities of the line item.
    * `name`:  Tthe attribute's name.
    * `value`:  The `value` associated with the attribute.
    * `type`: The type of attribute.
* **Pricing**: The `pricing` object allows you to set the sale price for a line item in a cart. Only available for [unit price override](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Price-override) and [line item price override](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Price-override/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(line%20Item%20price\)/post).
  * `currency`: A three-letter [ISO 4217](https://www.xe.com/iso4217.php) currency code. Only available for [unit price override](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Price-override).
  * `value`: The value of the price override or sale price. Only available for [unit price override](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Price-override).
  * `itemPrice`: This object allows you to set the overall total item price with quantity (`salePriceWithQuantity`). Only available for [line item price override](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Price-override/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(line%20Item%20price\)/post).
    * `value`: The value of the overall total item price with quantity.&#x20;
    * `currency`: A three-letter [ISO 4217](https://www.xe.com/iso4217.php) currency code.&#x20;

### Organization identifier

The `organizationId` is the identifier used to identify the business. This string allows a maximum of 50 characters. You can use it to supply the shopper's [`companyId`](carts.md#company-identifier) when the shopper chooses [TreviPay](../../payments/supported-payment-methods/trevipay.md) as the payment method.

### Shipping address

The `shippingAddress` object contains the shopper's shipping information.

### Suppress order confirmation email

A real order uses `suppressorderconfirmationemail` to suppress the order confirmation e-mail. If you want to use this feature, contact your Customer Success Manager.

### Terms of sales acceptance

The `termsOfSalesAcceptance` indicates whether or not the shopper accepted the [Terms of Service](../../shopper-apis/cart/creating-or-updating-a-cart/terms-of-sale-acceptance.md).

## Update current cart query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of carts. The following topics describe the query parameters available for [carts/active](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### External reference identifier (ERID)

The [externalReferenceId](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) is a company's internal identifier for a product.&#x20;

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Offer identifier

The `offerId` is the offer's identifier.

### Parent line item identifier

The `parentLineItemId` is the line item identifier of the parent product. While adding a child product to the cart, provide the line item identifier of the parent product along with the offer identifier to specify the child product should be associated with which parent product line item.

### Product identifier

A `productId` is your unique [product identifier](carts.md#product-identifier) or unique stock keeping unit (SKU) for a product. A product's unique identifier is represented by an `id`.&#x20;

### Promotional code

The `promoCode` is the promotional code the shopper wants to apply to the cart.

### Quantity

The `quantity` is the number of products added to the cart. The value must be a valid integer. If the quantity is not explicitly specified, the default is 1.

### Suppress order confirmation email

A real order uses `suppressorderconfirmationemail` to suppress the order confirmation e-mail. If you want to use this feature, contact your Customer Success Manager.

### Term identifier

The `termId` is the finance term identifier associated with the cart. You must pass the `termId` with the `productId` or `externalReferenceId`.

### Token

The `token` is the authorized or anonymous token for the shopper.'

## Cart offers resource

The following describes some of the key attributes of [cart offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers).

### POP name

The `popName` is the name of the point of promotion (POP).

## Cart offers query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of cart offers. The following topics describe the query parameters available for [cart offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Token

The `token` is the authorized or anonymous token for the shopper.

### format

The `format` overrides the default format of XML for the Authorize Shopper API. Valid values are XML and JSON.

## Cart applied offers

The following describes some of the key attributes for [cart applied offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers\~1%7BofferId%7D/delete).

### Offer identifier

The `offerId` is the offer's identifier.

## Cart applied offers query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of applied offers. The following topics describe the query parameters available for [applied-offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers/get). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### API key

The `apiKey` is your account's [API key](../../resources/API-structure/) used to authenticate your API requests. You must specify either an `apiKey` or `token`.

### Token

The `token` is the authorized or anonymous token for the shopper. You must specify either an `apiKey` or `token`.

## Cart eligible offers query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of eligible offers. The following topics describe the query parameters available for [eligible-offers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1eligible-offers/delete). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Token

The `token` is the authorized or anonymous token for the shopper.

## Line items query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of line items. The following topics describe the query parameters available for [line-items](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/get). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Action

The `action` parameter modifies the POST behavior. The action parameter determines the method behavior for handling the quantity associated with a posted line item. Valid values are: `add`, `update`, and `subtract`. The default `action` for the[ `POST /vq1/shoppers/me/carts/active/line-items/{lineItemsId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post) resource method is `update`. The default `action` for the [`POST /v1/shoppers/me/carts/active/line-items`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post) resource method is `add`. To override the default method behavior for handling quantity, explicitly specify the value of the action query parameter.

### Company Identifier

The `companyId` is the company's identifier.

### Expand

Use the [`expand` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task.&#x20;

### External reference identifier (ERID)

The [externalReferenceId](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) is a company's internal identifier for a product.&#x20;

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Offer identifier

The `offerId` is the offer's identifier.

### Line item identifier

A comma-separated list of one or more line item identifiers.

### Parent line item identifier

The `parentLineItemId` is the line item identifier of the parent product. While adding a child product to the cart, provide the line item identifier of the parent product along with the offer identifier to specify the child product should be associated with which parent product line item.

### Product identifier

A `productId` is the your unique [product identifier](carts.md#product-identifier) or unique stock keeping unit (SKU) for a product. A product's unique identifier is represented by an `id`.&#x20;

### Token

The `token` is the authorized or anonymous token for the shopper.

### Quantity

The `quantity` is the number of products added to the cart. The value must be a valid integer. If the quantity is not explicitly specified, the default is 1.

### Suppress order confirmation email

A real order uses `suppressorderconfirmationemail` to suppress the order confirmation e-mail. If you want to use this feature, contact your Customer Success Manager.

## Payment methods query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of payment methods. The following topics describe the query parameters available for [payment-methods](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Methods). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the [`expand` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task.&#x20;

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Token

The `token` is the authorized or anonymous token for the shopper.

## Resume cart query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the contents of the resume cart. The following topics describe the query parameters for [resume-cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items%20\(API%20Trigger%20Offer\)/post). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the [`expand` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task.&#x20;

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Token

The `token` is the authorized or anonymous token for the shopper.

## Shipping options query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the shipping options. The following topics describe the query parameters for [shipping-options](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Options). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the [`expand` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task.&#x20;

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Token

The `token` is the authorized or anonymous token for the shopper.

## Submit cart query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the contents of the submit cart. The following topics describe the query parameters for [submit-cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the [`expand` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task.&#x20;

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Token

The `token` is the authorized or anonymous token for the shopper.

## Tax registration resource

The following describes some of the key attributes for [updating a tax registration](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations/post).

### Key

The `key` is the tax registration key.

### Value

The `value` is the tax identifier.

## Tax registration query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the contents of the tax registration. The following topics describe the query parameters for [tax registration](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### API key

The apiKey is your account's [API key](../../resources/API-structure/) used to authenticate your API requests. You must specify either an `apiKey` or `token`. Only applies to [`GET /v1/shoppers/me/carts/active/tax-registrations/schema`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations\~1schema/get).

### Token

The `token` is the authorized or anonymous token for the shopper. You must specify either an `apiKey` or `token`.

## Web checkout query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the contents of the web checkout. The following topics describe the query parameters for [web-checkout](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

The following describes query parameters for [web-checkout](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout).

### External reference identifier (ERID)

The [`externalReferenceId`](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) is a company's internal identifier for a product.&#x20;

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Product identifier

A `productId` is your unique [product identifier](carts.md#product-identifier) or unique stock keeping unit (SKU) for a product. A product's unique identifier is represented by an `id`.&#x20;

### Theme identifier

The `themeId` is the identifier of the theme associated with a site. The theme controls the styles of a Digital River-hosted web page.

### Token

The `token` is the authorized or anonymous token for the shopper.
