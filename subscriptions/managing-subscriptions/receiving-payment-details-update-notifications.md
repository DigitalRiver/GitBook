---
description: >-
  Learn how to receive notification when a shopper updates their payment details
  for a subscription.
---

# Receiving payment details update notifications

You can use the Subscription Service Notification (SSN) to send updated payment details notifications emails to shoppers to increase the card update and renewal success rate for a subscription. A notification allows you to prompt a customer to update their card before it expires.

## Triggering a payment details update notification

An SSN is triggered when:

* A Customer Service Representative (CSR) [updates a shopper's subscription information](https://help.digitalriver.com/help/gc/Customer-Service/Managing-subscription-details.htm#ViewingAndModifyingSubscriptionInformation) from [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
* A CSR uses the [Search Shoppers option](https://help.digitalriver.com/help/gc/Customer-Service/Searching-for-shoppers.htm#SearchingForShoppers) in Global Commerce to modify the shopper's billing option.&#x20;
* A shopper [updates their billing option from the Self-Service section of your online store](https://help.digitalriver.com/help/gc/Customer-Service/Customer-service.htm#CustomerSelfService). The shopper can use the Self-Service section to edit the existing payment method or add a new payment method.&#x20;
* You submit an `AddUpdateShopperRequest` through the [User Management service](../../customers-1/user-management.md) to add or modify a shopper, including the shopper’s default billing method.
* You use [`POST/v1/shoppers/me/payment-options`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) or [`POST /v1/shoppers/me/payment-options?expand=all`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) to create a shopper's billing option for a subscription.
* You use [`POST /v1/shoppers/me/payment-options/`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) or [`POST /v1/shoppers/me/payment-options/{paymentOptionId}`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) to update a shopper's payment option for a subscription.
* You use [`POST /v1/subscriptions/{subscriptionId}/payment-options`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updatePaymentOption) to update the subscription payment option.
* You use [`POST /v1/subscriptions/{subscriptionId}/payment-source`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updatePaymentSource) to update the payment source.
* The shopper changes the subscription product by [upgrading or downgrading the subscription product](changing-the-subscription-renewal-product.md), [creating a new billing option](associating-a-new-billing-option-to-an-existing-subscription.md#payment-option) or [payment source](associating-a-new-billing-option-to-an-existing-subscription.md#payment-source) for an existing subscription, or renew a subscription using a new billing option.
* The shopper [changes the quantity of the subscription product](../selling-subscriptions-without-add-ons/reducing-the-quantity-of-a-subscription.md) while placing an order and while [placing an order and creating a new billing option](associating-a-new-billing-option-to-an-existing-subscription.md).
* The shopper [places an order for a mid-term change](../selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md) and also [creates a new billing option](associating-a-new-billing-option-to-an-existing-subscription.md#payment-source).
* The shopper places an order to [manually renew their subscription](modifying-the-subscription-renewal-date.md) and also [creates a new billing option](associating-a-new-billing-option-to-an-existing-subscription.md#payment-option).
* The shopper goes to your custom page that contains the `displayUpdateAddressPaymentInfoPage` attribute.
* The shopper goes to your custom page that contains the `updatePaymentInfo` attribute.
* You use [`POST /v1/subscriptions/{subscriptionId}/email`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Email-Updater/operation/emailUpdater) to update the subscriber's email address for a specific subscription.&#x20;
* You use [`POST /v1/shoppers/me?applyEmailToSubscriptions=true`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post)  to update a subscription customer's ship-to and bill-to email addresses for all subscriptions so they can receive notifications.&#x20;
