---
description: Understand why a payment information change triggers a notification.
---

# Sending a payment information change notification

You will immediately receive a notification when a shopper changes their payment method or credit card detail information, billing address, or email address.

## Notification trigger

The following activities trigger this notification.

* Digital River receives updated stored credit card information from a [Card Account Updater](card-account-updater.md).
* The shopper [changes the quantity of the subscription product](../../../common-shopper-and-admin-apis/subscriptions/reducing-the-quantity-of-a-subscription.md) while placing an order and while [placing an order and creating a new billing option](../../../common-shopper-and-admin-apis/subscriptions/associating-a-new-billing-option-to-an-existing-subscription.md).
* The shopper [manually renews their subscription by changing the renewal date and creating](../updating-the-subscription-renewal-date.md)[ a new billing option](../../../common-shopper-and-admin-apis/subscriptions/associating-a-new-billing-option-to-an-existing-subscription.md#payment-option).
* The shopper [associates a new payment source](../../../common-shopper-and-admin-apis/subscriptions/associating-a-new-billing-option-to-an-existing-subscription.md#payment-source) or [option](../../../common-shopper-and-admin-apis/subscriptions/associating-a-new-billing-option-to-an-existing-subscription.md#payment-option) for an existing subscription.
* The shopper [places an order for a mid-term change](../applying-a-midterm-change-with-price-override.md) and also [creates a new billing option](../../../common-shopper-and-admin-apis/subscriptions/associating-a-new-billing-option-to-an-existing-subscription.md#payment-source).
* The shopper [updates their billing option from the Self-Service section of your online store](https://help.digitalriver.com/help/gc/Customer-Service/Customer-service.htm#CustomerSelfService). The shopper can use the Self-Service section of your online store to edit the existing payment method or add a new payment method.&#x20;
* You submit an `AddUpdateShopperRequest` through the [User Management service](../../../shopper-apis/shoppers/managing-shoppers/user-management.md) to add or modify a shopper, including the shopper's default billing method.
* The shopper goes to your custom page that contains the `displayUpdateAddressPaymentInfoPage` attribute.
* You [change the subscription renewal product](../changing-the-subscription-renewal-product.md).
* You [change the subscription renewal quantity](../../../common-shopper-and-admin-apis/subscriptions/changing-the-subscription-renewal-quantity.md).
* You update the subscription's payment option with or without the `expand=all` query parameter to create a shopper's billing option for a subscription.&#x20;
* You [update the subscription's payment source](../../../common-shopper-and-admin-apis/subscriptions/updating-the-subscriptions-payment-source.md).
* You [update the subscriber's ship-to and bill-to email addresses for all subscriptions](../../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-all-subscriptions) so they can receive notifications.&#x20;
* You [create ](../../../shopper-apis/shoppers/retrieving-sources.md#creating-shopper-payment-options)or [update a shopper's payment option](../../../shopper-apis/shoppers/retrieving-sources.md#updating-the-shoppers-payment-options).
* You [get a specific subscription by identifier](../../../common-shopper-and-admin-apis/subscriptions/getting-a-subscription-by-identifier.md).

The following classes trigger a payment information change notification:

* `RetryAccountUpdateDataProcessor`
* `UpdateEmailAddressRequestProcessor`
* `PaymentSourceRequestProcessor`
* `SubscriptionTask`
* `SubscriptionIml`
* `AddEditPaymentForm`
* `SubscriptionInfoEditPaymentInfoCommand`
* `DisplayUpdateAddressPaymentInfoPage`
