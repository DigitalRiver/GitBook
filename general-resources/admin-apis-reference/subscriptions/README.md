---
description: Learn more about the subscriptions as they apply to Admin APIs.
---

# Subscriptions

## Activate resource

The following describes some of the key attributes for [activate ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Subscription/operation/activateSubscription)subscription.

### Activation key

The `activationKey` activates the subscription.

### Activation date

The `activationDate` is the subscription's activation date is the date when the shopper activates or begins using the subscription and marks the start of the subscription period. This is the date when the subscription term begins. Digital River uses this date to renew the subscription if it is set to auto-renew. The activation date is important because the other dates in the lifecycle (like billing) either begin with the activation date or depend on the activation date.

### Expiration date

The `expirationDate` is the date when the subscription expires.

## Email resource

The following describes some of the key attributes for a [subscription's shipping and billing email address](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Email-Updater).

### Email address

The `emailAddress` is the the updated billing and shipping email address for a subscription.

## Expiration-date resource

The following describes some of the key attributes in a subscription's [expiration-date](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Subscription/operation/updateExpirationDate).

### Expiration date

The `expirationDate` is date when the subscription expires.

## Perpetual-price resource

The following describes some of the key attributes in a subscription's [perpetual-price](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Subscription/operation/getSubscriptionInfo).

### Perpetual unit price

The `perpetualUnitPrice` is the perpetual unit price of the subscription product.

### Add-ons

The `addOns` is an array of the objects. The objects sub-components, features, or products that a shopper can add to their subscription product for an additional fee per renewal cycle. An add-on is incremental to the main subscription product and follows the subscription renewal cycle. During the lifecycle of a subscription, the shopper can add or remove the add-on products. When a shopper adds an add-on product to a subscription, Digital River renews the add-on product at the same time as the main subscription product until the shopper deactivates the add-on.

## Preview resource

The following describes some of the key attributes in a subscription's [preview](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Immediate-Midterm-Change/operation/previewSubscription).

### Add-ons

The `addOns` is an array of the objects. The objects sub-components, features, or products that a shopper can add to their subscription product for an additional fee per renewal cycle. An add-on is incremental to the main subscription product and follows the subscription renewal cycle. During the lifecycle of a subscription, the shopper can add or remove the add-on products. When a shopper adds an add-on product to a subscription, Digital River renews the add-on product at the same time as the main subscription product until the shopper deactivates the add-on.

#### Product

The `product` object contains the product's identifier information.

* **id**: The product identifier.
* **externalReferenceId**: The product's external reference identifier.

#### Quantity

The `quantity` is a numeric number that indicates the number of add-ons.

#### Prorated unit price

When the `proratedUnitPrice` is present, it overrides all other prices and skips normal proration. When it is not present, [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) [pricing and proration applies](https://help.digitalriver.com/help/gc/Products/All-Products/Configuring-the-product-settings.htm#UpgradesAndDowngrades).

## Preview-cart resource

The following describes some of the key attributes in a subscription's [preview-cart](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Immediate-Midterm-Change/operation/previewCartSubscription).

### Add-ons

The `addOns` is an array of the objects. The objects sub-components, features, or products that a shopper can add to their subscription product for an additional fee per renewal cycle. An add-on is incremental to the main subscription product and follows the subscription renewal cycle. During the lifecycle of a subscription, the shopper can add or remove the add-on products. When a shopper adds an add-on product to a subscription, Digital River renews the add-on product at the same time as the main subscription product until the shopper deactivates the add-on.

#### Product

The `product` object contains the product's identifier information.

* **id**: The product identifier.
* **externalReferenceId**: The product's external reference identifier.

#### Quantity

The `quantity` is a numeric number that indicates the number of add-ons.

#### Prorated unit price

When the `proratedUnitPrice` is present, it overrides all other prices and skips normal proration. When it is not present, [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) [pricing and proration applies](https://help.digitalriver.com/help/gc/Products/All-Products/Configuring-the-product-settings.htm#UpgradesAndDowngrades).

## Reference-id resource&#x20;

The following describes some of the key attributes in a subscription's [reference-id](https://www.digitalriver.com/docs/commerce-admin-api/#tag/External-Reference/operation/modifyExternalReferenceId).

### External reference identifier

The externalReferenceId is the [external reference identifier](./#external-reference-identifier) for the subscription.

## Renewal-price source

The following describes some of the key attributes in a subscription [renewal-price](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/changeSubscriptionRenewalPrice).

### Renewal unit price

The `renewalUnitPrice` is the price for the subscription's renewal unit.

## Renewal-product resource

The following describes some of the key attributes in a subscription [renewal-product](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/updateRenewalProduct).

### Renewal product identifier

The `renewalProductId` is the subscription's renewal product identifier.
