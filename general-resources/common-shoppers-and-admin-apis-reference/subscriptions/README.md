---
description: Learn more about subscriptions as they apply to Shopper APIs and Admin APIs.
---

# Subscriptions

## Cancel resource

The following describes some of the key attributes of a [cancel](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Subscription/operation/cancelSubscription) subscription.

### Suppress cancel notification

The `suppressCancelNotification` is a boolean element that you can use to suppress the cancel notification email. The value is set to `false` by default.

## Payment-option resource

The following describes some of the key attributes of a subscription's [payment-option](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment/operation/updatePaymentSource).

### Payment option identifier

The `paymetOptionId` is a payment option identifier.

### Is the shipping address the same as the billing address

The `isShippigSameAsBilling` indicates whether the subscription's shipping address is the same as the billing address. The value is set to `true` by default.

## Payment-source resource

The following describes some of the key attributes of a subscription's [payment-source](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment/operation/updatePaymentSource).

### Source identifier

The `sourceId` is the payment source identifier.

### Is the shipping address the same as the billing address

The `isShippigSameAsBilling` indicates whether the subscription's shipping address is the same as the billing address. The value is set to `true` by default.

## Reduce resource

The following describes some of the key attributes for subscription's [reduce](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Immediate-Midterm-Change/operation/reduceSubscription) resource.

#### Add-ons

The `addOns` is an array of objects. The objects are sub-components, features, or products that a shopper can add to their subscription product for an additional fee per renewal cycle. An add-on is incremental to the main subscription product and follows the subscription renewal cycle. During the lifecycle of a subscription, the shopper can add or remove the add-on products. When a shopper adds an add-on product to a subscription, Digital River renews the add-on product at the same time as the main subscription product until the shopper deactivates the add-on.

#### Product

The `product` object contains the product's identifier information.

* **id**: The [product identifier](../product-identifier.md).
* **externalReferenceId**: The product's [external reference identifier](../external-reference-identifier-erid.md). It's your company's unique identifier for the product.&#x20;

#### Quantity

The `quantity` is a numeric number that indicates the number of add-ons.

#### Prorated unit price

When the `proratedUnitPrice` is present, it overrides all other prices and skips normal proration. When it is not present, [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) [pricing and proration applies](https://help.digitalriver.com/help/gc/Products/All-Products/Configuring-the-product-settings.htm#UpgradesAndDowngrades).

## Renewal-type resource

The following describes some of the key attributes of a subscription's [renewal-type](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/updateRenewalType).

### Auto renewal

The `autoRenewal` is a boolean element that you can use to enable the automatic renewal of the subscription.

## Renewal-quantity resource

The following describes some of the key attributes of a subscription [renewal-quantity](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/changeSubscriptionRenewalQuantity).

### Renewal quantity

The `renewalQuantity` is the subscription's renewal quantity.

## Ship-to-address resource

The following describes some of the key attributes of a subscription's [ship-to-address](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Address/operation/modifyShippingAddress).

### First name

The `firstname` is the shopper's first name.

### Last name

The `lastname` is the shopper's last name.

### Company name

The `companyName` is the company name.

### Line 1

The `line1` is the first line of the address such as the street address.

### Line 2

The `line2` is the second line of the address such as the apartment, suite, block number, area name, or space number.

### Line 3

The `line3` is the third line of the address.

### City

The `city` is the city of the address.

### Country subdivision

The `countrySubdivision` is the [state](https://docs.digitalriver.com/commerce-api/cart/creating-or-updating-a-cart/providing-address-information#us-states-and-territories), county, province, or region.

### Postal code

The `postalCode` is the postal code.\
\
For United States addresses, Digital River supports ZIP+4 codes. They consist of the last four digits of a full nine-digit ZIP code. A nine-digit ZIP Code has two parts: the initial five digits of the zip code indicating the destination post office or delivery area and the last four digits representing a specific delivery route within that overall delivery area.

### Country

The `country` is a two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard.

### Phone number

The `phoneNumber` is the shopper's phone number.

### Country name

The `countryName` is the name of the country.

### Email address

The `emailAddress` is the shopper's email address.
