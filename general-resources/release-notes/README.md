---
description: Keep track of changes and updates to the Commerce API.
---

# Release notes

V1 is the base version of the Commerce API. The following dates indicate when we released updates to this version.

## 2022/7/27

* We expanded our Klarna Pay Later offering with the addition of payment options in Canada, France, Ireland, Poland, and Portugal. You can learn more [here](../../payments/payments-solutions/digitalriver.js/payment-methods/klarna.md).
* We expanded our TreviPay B2B payment offering to include locales in Denmark and New Zealand! You can find more details [here](../../payments/payments-solutions/digitalriver.js/payment-methods/trevipay.md). ****&#x20;

## 2022/6/30

We released the [Webhook service](https://help.digitalriver.com/help/gc/Administration/Webhook-Service/Webhook-service.htm) for Commerce API. The Webhook service now supports events covering the entire [subscription cycle](../../subscriptions/subscription-lifecycle.md). You can choose to manage the service through the [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) interface or the [Webhooks API](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Webhook-Event-Management). You can now integrate the Webhook service for Commerce API with endpoints to get an instant update on events throughout the entire [subscription cycle](../../subscriptions/subscription-lifecycle.md). We also updated the list of [webhook events](../../events-and-webhooks/events/event-types.md) in the Webhook service. You can now choose from more subscription events.

## 2022/6/29

* We added `precondition-failure` error codes to [409 Conflict](../../error-codes.md#409-conflict) in the [Error codes](../../error-codes.md) section.
* We updated the following APIs:
  * Renamed "API Trigger Offer" to "[Trigger offer by cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(API%20Trigger%20Offer\)/post)".
  * Added the [Trigger offer by line item](https://www.digitalriver.com/docs/commerce-api-reference/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items%20\(API%20Trigger%20Offer\)/post). Use this API to trigger a product-level offer.
  * Updated the descriptions for the [Order Lookup](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Order-Lookup/paths/\~1v1\~1shoppers\~1order-lookup/post) API.

## 2022/6/16

* We added support for [applying store credit](../../consumer-browsing-experience-1/common-use-cases/applying-store-credit.md) to non-recurring transactions. Store credit allows merchants to offer customers a store credit as a payment type at checkout.
* We now support [two payments in a cart](../../payments/sources/using-the-source-identifier.md).
* You can now [detach a payment from a cart](../../payments/sources/using-the-source-identifier.md#detaching-payment-sources-from-a-cart).
* You can now create [secondary sources](../../payments/sources/using-the-source-identifier.md#creating-secondary-sources) through the [Sources API](https://www.digitalriver.com/docs/commerce-api-reference/#operation/createSources) by sending your confidential API key in a POST /sources request.

## 2022/6/1

We restructured the API tags and descriptions for the Shopper API as follows:

* Renamed Apply Payment Methods to [Apply or Detach Payment Methods](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post) and added the [Detach all applied payment methods from the cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1payment/delete).
* Restructured the offer API tags and revised their descriptions for [Retrieve all POP offers for a cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1point-of-promotions\~1{popName}\~1offers/get) and [Retrieve all offers](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1offers/get).
* Updated the sample payload for [Retrieve cart applied offers](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers/get).
* Added [Update shopper payment options](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options\~1{paymentOptionId}/post).
* We moved the following webhook APIs under [Webhook Event Management](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Webhook-Event-Management):
  * [Get all webhook subscriptions](https://www.digitalriver.com/docs/commerce-api-reference/#operation/getAllWebhooksUsingGET)
  * [Create a new webhook](https://www.digitalriver.com/docs/commerce-api-reference/#operation/createNewWebhookUsingPOST)
  * [Get a specific webhook by ID](https://www.digitalriver.com/docs/commerce-api-reference/#operation/getWebhookByIdUsingGET)
  * [Delete a webhook](https://www.digitalriver.com/docs/commerce-api-reference/#operation/deleteWebhookUsingDELETE)
  * [Update a webhook](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updateWebhookUsingPATCH)
* We added [Payment Source](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Source) and added the following source APIs:
  * [Get a source by source by identifier](https://www.digitalriver.com/docs/commerce-api-reference/#operation/retrieveSources)
  * [Create a secondary source](https://www.digitalriver.com/docs/commerce-api-reference/#operation/createSources)
* Added `cart-charge-failure` to the list of [409 Conflict errors](../../error-codes.md#409-conflict) in [Error codes](../../error-codes.md).

## 2022/5/6

* We updated the [authorization decline codes](../../cart/submitting-a-cart/authorization-declines.md) for customer-initiated and merchant-initiated transactions.
* We added more [error codes](../../error-codes.md), including the [credit card error codes](../../error-codes.md#credit-card-error-and-declined-message) and a [DNS outage error message](../../error-codes.md#500-internal-server-error).

## 2022/4/1

We upgraded Google Pay to offer the up-to-date Google Pay wallet experience. You can now [configure the dynamic Google Pay button](../reference/elements/google-pay-elements.md#google-pay-element-styles-and-customization) by applying your preferred button styles.

## 2022/3/28

We added support for the [iDEAL ](../../payments/payments-solutions/digitalriver.js/payment-methods/configuring-ideal.md)payment method.

## 2022/3/16

We added support for the [Bancontact ](../../payments/payments-solutions/digitalriver.js/payment-methods/configuring-bancontact.md)payment method.

## 2022/1/26

We added support for the [Boleto ](../../payments/payments-solutions/digitalriver.js/payment-methods/configuring-boleto.md)payment method.
