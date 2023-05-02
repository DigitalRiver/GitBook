---
description: Understand the subscription action processed event.
---

# Subscription action processed event

When a subscription is changed, Digital River creates the `subscription.action.processed`. This event tells you if the subscription update succeeded or failed and provides the details of the pending actions in the payload. The `actionType` identifies the action applied to the subscription. The actions are described below.

## `activate`

When you [activate a shopper's subscription](../../../admin-apis/subscription-management/activating-a-subscription.md), the subscription state changes from `pendingActivation` to `Subscribed`. It also updates the subscription expiration date and all subscription-related data columns.

## `cancel`

When you start[ a shopper's subscription](../../../admin-apis/subscription-management/activating-a-subscription.md), the subscription state changes from `pendingActivation` to `Subscribed`. It also updates the subscription expiration date and all subscription-related data columns.

## `email`

You will be notified when you [update a shopper's subscription billing or shipping email address](../../../admin-apis/subscription-management/updating-a-subscriptions-billing-and-shipping-email-address.md).

Billing email address: `subscription.billingOption.billAddress.emailAddress`\
Shipping email address: `subscription.shipToAddress.emailAddress`

## `expiration_date`

When you [update a shopper's subscription payment option](../../../common-shopper-and-admin-apis/subscriptions/updating-the-subscriptions-payment-option.md), the system associates a new billing or payment option with the subscription. When updated successfully, Retry On Account Update will trigger a billing attempt if the subscription falls under the renewal window.

## `payment_option`

When you [update a shopper's subscription payment option](../../../common-shopper-and-admin-apis/subscriptions/getting-a-shoppers-subscription.md), the system associates a new billing or payment option with the subscription. When updated successfully, Retry On Account Update will trigger a billing attempt if the subscription falls under the renewal window.

## `payment_source`

When you [update a shopper's subscription payment source](../../../common-shopper-and-admin-apis/subscriptions/updating-the-subscriptions-payment-source.md), the system associates the new payment source with the subscription. If there is a billing option associated with the payment source, the system will create a new billing option for the payment source. The request payload contains the `sourceId` and `isShippingSameAsBilling` flag.

## `perpetual_price`

When you [modify the subscription's perpetual price](../../../admin-apis/subscription-management/assigning-a-perpetual-unit-price.md#creating-or-changing-a-perpetual-unit-price) for a shopper, the system changes the subscription price[ for the remaining subscription cycle](../../../general-resources/admin-apis-reference/subscriptions/midterm-change.md#perpetual-unit-price). The system updates the perpetual price or the hold price.

## `reduce`

When you [modify the subscription's perpetual price](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Perpetual-price/operation/changePerpetualPrice) for a shopper, the system changes the [subscription price](../../../general-resources/admin-apis-reference/subscriptions/midterm-change.md#perpetual-unit-price)[ for the remaining subscription cycle](../../../general-resources/admin-apis-reference/subscriptions/midterm-change.md#perpetual-unit-price). The system updates the perpetual price or the hold price.

## `reference_id`

You will be notified when you [modify the subscription's external reference ID](broken-reference).

## `renewal_price`

When you change the shopper's subscription price, the system updates the shopper's subscription renewal price.

## `renewal_product`

When you [change the shopper's subscription renewal product](../../../admin-apis/subscription-management/changing-the-subscription-renewal-product.md), the system updates the shopper's subscription renewal product.

## `renewal_quantity`

When you [change the shopper's subscription renewal quantity](../../../common-shopper-and-admin-apis/subscriptions/changing-the-subscription-renewal-quantity.md), the system updates the shopper's subscription renewal quantity.

## `renewal_type`

When you [change the shopper's subscription renewal type](../../../common-shopper-and-admin-apis/subscriptions/changing-the-subscription-renewal-type.md), the system updates the shopper's subscription renewal quantity.

## `ship_to_address`

When you [change the shopper's ship-to address](../../../general-resources/reference/elements/#shipping-address-change), the system either adds or updates the shopper's ship-to address.
