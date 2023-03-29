---
description: Keep track of changes and updates to the Commerce API.
---

# Release notes

V1 is the base version of the Commerce API. The following dates indicate when we released updates to this version.

## 2023/3/29

* We replaced the Commerce API reference with a Commerce API suite that includes the following API references:&#x20;
  * [Shopper APIs reference](https://www.digitalriver.com/docs/commerce-shopper-api/): This API reference provides the resources for an end-to-end ecommerce experience used when our Global Commerce platform is the system of record. The Shopper APIs allow clients to build a storefront, create shopper workflows, operate their store, and display products. For more information, see [Shopper APIs](broken-reference), [Shopper APIs reference](../shopper-apis-reference/), [Common Shopper and Admin APIs](broken-reference), and [Common Shopper and Admin APIs reference](../common-shoppers-and-admin-apis-reference/).&#x20;
  * [Admin APIs reference](https://www.digitalriver.com/docs/commerce-admin-api/): This API reference allows administrators to programmatically create, update, deploy, and retire products on your storefront, create and edit products in bulk, manage product data, and manage sites and subscriptions. Use the Admin APIs when you want to host the Cart and Checkout pages and manage your products via API. For more information, see [Admin APIs](broken-reference), [Admin APIs reference](../admin-apis-reference/), [Common Shopper and Admin APIs](broken-reference), and [Common Shopper and Admin APIs reference](../common-shoppers-and-admin-apis-reference/).
* We updated the following topics:&#x20;
  * [Getting started ](../../master/getting-started/)
  * [Error codes](../../common-shopper-and-admin-apis/error-codes/)&#x20;
* We added the following information:&#x20;
  * [How to resume cart submission](../../shopper-apis/cart/resuming-cart-submission.md)
  * [Considerations](../../shopper-apis/orders-1/landed-costs.md#considerations) for [landed costs](../../shopper-apis/orders-1/landed-costs.md)
  * [Best practice flows by payment type](../../payments/sources/using-the-source-identifier.md#best-practice-flows-by-payment-type)
* We added the following subscription notification enhancements:
  * [Sending an expired credit card notification](../../admin-apis/subscription-management/subscription-notifications/sending-an-expired-credit-card-notification.md)
  * [Sending a subscription renewal reminder](../../admin-apis/subscription-management/subscription-notifications/sending-a-subscription-renewal-reminder-notification.md)
  * [Sending a payment failure notification](../../admin-apis/subscription-management/subscription-notifications/sending-a-payment-failure-notification.md)

## 2023/3/16

Digital River adds Clearpay to the payment method roster! By leveraging Afterpay, your shoppers have the flexibility to buy now and pay for their purchases in 3 interest-free payments over 60 days. Learn how you can add Clearpay [here](../../payments/supported-payment-methods/clearpay.md).

## 2023/3/14

[Amazon Pay](../../payments/supported-payment-methods/amazon-pay.md) is a global digital wallet paving the way for your brand to gain visibility and access to millions of existing Amazon customers. This payment method boasts a highly secure and seamless checkout experience, leveraging saved shipping and payment information in the shopper's Amazon account. As a result, the shopper can complete their transactions in 3 simple clicks and almost twice as fast as other payment options. Digital River supports [Amazon Pay Checkout](../../payments/supported-payment-methods/amazon-pay.md#how-it-works).
