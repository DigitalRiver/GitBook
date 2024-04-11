---
description: Learn how to provide billing, shipping and email address-related information.
---

# Providing address information

You can use [customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) and [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) to provide [ship from](providing-address-information.md#ship-from-address), [ship to](providing-address-information.md#ship-to-address), and [bill to](providing-address-information.md#bill-to-address) address-related information. During the [checkout process](./#sequencing-the-checkout-process), we use this information to select the correct [selling entity](selling-entities.md), determine whether [tax identifiers](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders) are applicable, [screen for fraud](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#fraud-review), and [compute taxes](tax-calculations.md).

{% hint style="warning" %}
Except in [certain scenarios](providing-address-information.md#postal-code-and-state-province-validations), we don't perform real-time address validation. Instead, we expect you to validate the customer's address before sending it to us.
{% endhint %}

When [building checkouts](./), you should pay close attention to how you [sequence sending address information](providing-address-information.md#sequencing-address-information-in-checkout-workflows). And before you can successfully [convert a checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), you must meet certain [address-related requirements](providing-address-information.md#address-requirements-and-validations).

## Sequencing address information in checkouts <a href="#sequencing-address-information-in-checkout-workflows" id="sequencing-address-information-in-checkout-workflows"></a>

For [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) that contain [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), we recommend you send a customer's [shipping address](providing-address-information.md#ship-to-address) and [billing address](providing-address-information.md#billing-address-requirements) in the [create checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts).

We suggest this sequencing because, in our tax computation process, the shipping address takes highest priority, followed by the billing address, and then, finally, the [purchase location](setting-the-purchase-location.md). If we generate a tax estimate based on the checkout's [`billTo`](providing-address-information.md#bill-to-address), and then update that estimate using a [`shipTo`](providing-address-information.md#ship-to-address) you provide in a [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) request, you could receive the following error when you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier):

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "order_submit_failed",
            "message": "Payment session status is invalid."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

For transactions that contain only [digital products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), we recommend that you first collect the customer's current billing information and use it to set the checkout's [`billTo`](providing-address-information.md#bill-to-address). In a subsequent [update checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts), you can [attach the payment source to the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

Since no [ship to address](providing-address-information.md#ship-to-address) is required on digital-only transactions, this sequence ensures tax estimates are accurate and reduces the frequency of order failures. If you don't first send `billTo`, an outdated billing address on the [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) may result in an inaccurate tax estimate when you attach the source to the checkout.

## Address requirements and validations

Every [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) that you create [requires an email address](providing-address-information.md#email-address-requirements). We also [require the customer's billing information](providing-address-information.md#billing-address-requirements).

If a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) only contains [digital products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), you're _not_ required to provide either [`shipFrom`](providing-address-information.md#ship-from-address) or [`shipTo`](providing-address-information.md#ship-to-address). However, when [building a checkout](./) that contains [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), you [must set the ship from country](providing-address-information.md#ship-from-requirements) as well as [certain ship to parameters](providing-address-information.md#ship-to-requirements).

Additionally, in [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) where products are being shipped or billed to specific countries, we [validate the format of postal codes and states](providing-address-information.md#postal-code-and-state-province-validations).

{% hint style="warning" %}
In [registered checkouts](using-the-checkout-identifier.md#registered-checkouts-or-invoices), unless you're using [version](../../../general-resources/versioning.md) `2021-03-23` or earlier of the Digital River APIs, we do not use the associated [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `email`, `shipping`, and [default source's](../../../payments/payment-sources/using-the-source-identifier.md#setting-the-default-payment-source) `owner` values to populate undefined `email`, `shipTo`, and `billTo` attributes in the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).
{% endhint %}

### Email address requirements

In both `POST/checkouts` and `POST/checkouts/{id}` requests, the first-class `email` parameter is technically optional.

{% tabs %}
{% tab title="POST/checkouts request" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
...
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    ...
    "email": "janedoe@digitalriver.com",
    "shipTo": {
        ...
    },
    "shipFrom": {
        ...
    },
    "items": [
        {
            ...
        }
    ],
    ...
}'
```
{% endtab %}
{% endtabs %}

However, when you [convert that checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), the checkout must contain a properly formatted `email`. If it doesn't, the `POST/orders` returns a `400 Bad Request`:

{% tabs %}
{% tab title="POST/orders response" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "order_create_failed",
            "parameter": "email",
            "message": "The order could not be created because a required checkout parameter is missing. Update the checkout information provided before trying again."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Billing address requirements

Every [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) needs to contain the customer's billing address. So, before you [convert a checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), its [`billTo`](providing-address-information.md#bill-to-address) must be populated.

More specifically, the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `billTo` must contain `line1`, `city`, `country`, `postalCode`, and `name`. If it doesn't, then you receive either a `400 Bad Request` that identifies which parameter is missing or a `409 Conflict` that contains a more general message.

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "billTo.address.country",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}

{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "create-order-failed",
            "message": "The order is missing required details and could not be completed."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

If a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) contains a [primary source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources), then you can fulfill its `billTo` requirements by passing the customer's billing address in the [primary source creation method](../../../payments/payment-sources/using-the-source-identifier.md#creating-primary-sources). If you set up your integration this way, we use the source's [`owner`](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/common-payment-objects.md#owner-object) to set the checkout's `billTo`.

When you [combine primary and secondary sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources), the billing address information associated with the primary source takes higher priority.

If you only attach [secondary sources](../../../payments/payment-sources/using-the-source-identifier.md#secondary-payment-sources) to a checkout, then you have two options to meet our billing address requirements. You can either specify `owner` in the [secondary source creation method](../../../payments/payment-sources/using-the-source-identifier.md#creating-secondary-sources). Or you can create the secondary source without `owner` and set the checkout's `billTo`. If you attach multiple secondary sources to a checkout, and each source contains `owner`, we use the last source attached to populate the checkout's `billTo`.

### Ship from requirements

[Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) that contain [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) must met certain [`shipFrom`](providing-address-information.md#ship-from-address) requirements.

First, they need to have a `shipFrom.address.country`. If you don't provide this data when [building a checkout](./), and then [convert that resource to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), a `400 Bad Request` is returned.

{% tabs %}
{% tab title="Error" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "shipFrom.address",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

Second, if your goods are shipping from the United States, then some additional `shipFrom.address` requirements have to be met before Digital River’s tax service performs a calculation.

Specifically, if `country` is `US`, then:

* A `postalCode` is required and needs to, at a minimum, consist of five digits, all of which must be valid for a particular region or address in the United States. For example, a `postalCode` of `99999`, because it doesn't map to any actual location, won’t result in a tax calculation getting returned.
* A `state` is not required, but if you do define this parameter, then `postalCode` needs to be valid for that particular `state`. For example, if `postalCode` is `10001` and `state` is `MN`, then our tax service won’t perform a calculation because the first digit of all zip codes in Minnesota is 5.

### Ship to requirements

[Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) that contain [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) must have a `name`, `line1`, `city`, `postalCode,` and `country` in [`shipTo`](providing-address-information.md#ship-to-address). This is true for all shipping destinations. Additionally, when physical goods are being shipped to destinations within the United States or Canada, you must provide a [properly formatted](providing-address-information.md#states-and-province-validations)  `state`.

{% hint style="info" %}
When the [customer type is business](setting-the-customer-type.md), you should also set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shipTo.organization`. This ensures that the company's name is displayed on [tax invoices](../../../order-management/creating-and-updating-an-order.md#tax-invoices-and-credit-memos).
{% endhint %}

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) that contain [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), if any of the following values are missing, a [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) checkout request returns a `400 Bad Request` :

{% tabs %}
{% tab title="Ship to line1" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "address.line1",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}

{% tab title="Ship to country" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "shipTo.address.country",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}

{% tab title="Ship to city" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "shipTo.address.city",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}

{% tab title="Ship to state" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "shipTo.address.state",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}

{% tab title="Ship to postal code" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "shipTo.address.postalCode",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

A missing `name` returns a similar `400 Bad Request` when you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).

{% tabs %}
{% tab title="Ship to name" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "shipping.name",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Postal code and state/province validations

When products are shipped and billed to certain countries, a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [ship to](providing-address-information.md#ship-to-address) and [bill to](providing-address-information.md#bill-to-address) must contain [postal code](providing-address-information.md#postal-code-validations) and [state/province](providing-address-information.md#states-and-province-validations) data that adheres to a standardized format.&#x20;

{% hint style="info" %}
Digital River uses the same address schemas returned by the [Country Specs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Country-specifications) when performing these postal code and state/province validations.
{% endhint %}

{% code title="Checkout" %}
```javascript
{
    ...
    "shipTo": {
        "address": {
            ...
            "postalCode": "55104",
            "state": "MN",
            "country": "US"
        },
        ...
    },
    ...
    "billTo": {
        "address": {
            ...
            "postalCode": "EC1M 4AN",
            "country": "GB"
        },
        ...
    },
    ...
}
```
{% endcode %}

#### Postal code validations

If the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [ship to](providing-address-information.md#ship-to-address) or [bill to](providing-address-information.md#bill-to-address) `country` is a value in the following table, then Digital River validates the format of `postalCode` using the listed regular expression:

| Ship to/bill to country | Ship to/bill to country code | Ship to/bill to postal code regex                                                                                                                                                    |
| ----------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| United States           | `US`                         | `^[0-9]{5}(?:[- ]?[0-9]{4})?$`                                                                                                                                                       |
| Canada                  | `CA`                         | `^[ABCEGHJ-NPRSTVXYabceghj-nprstvxy][0-9][ABCEGHJ-NPRSTV-Zabceghj-nprstv-z][ ]?[0-9][ABCEGHJ-NPRSTV-Zabceghj-nprstv-z][0-9]$`                                                        |
| Great Britain           | `GB`                         | `^([Gg][Ii][Rr] 0[Aa]{2})\|((([A-Za-z][0-9]{1,2})\|(([A-Za-z][A-Ha-hJ-Yj-y][0-9]{1,2})\|(([A-Za-z][0-9][A-Za-z])\|([A-Za-z][A-Ha-hJ-Yj-y][0-9][A-Za-z]?))))\\\\s?[0-9][A-Za-z]{2})$` |
| Germany                 | `DE`                         | `^\\\\d{5}$`                                                                                                                                                                         |
| France                  | `FR`                         | `^\\\\d{5}$`                                                                                                                                                                         |
| Spain                   | `ES`                         | `^\\\\d{5}$`                                                                                                                                                                         |
| Italy                   | `IT`                         | `^\\\\d{5}$`                                                                                                                                                                         |

With these countries, an improperly formatted ship to or bill to `postalCode` in a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) returns the following error:

{% hint style="info" %}
The same error is returned if you [create a source](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources) with an invalid postal code and then [associate that source with the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).
{% endhint %}

{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "address.postalCode",
            "message": "A required address parameter, postal code, is invalid."
        }
    ]
}
```
{% endcode %}

When collecting shipping and billing addresses associated with these countries, you can use our regular expressions to validate customer submitted postal codes on your front-end before sending that value in a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts), [`createDropIn()`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#step-5-configure-hydrate) or [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md#step-4.-use-digitalriver.js-to-create-a-payment-source) request.

#### States and province validations

If the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [ship to](providing-address-information.md#ship-to-address) and/or [bill to](providing-address-information.md#bill-to-address) `country` is either `US` (United States of America) or `CA` (Canada), and `state` is not an enumerated value, then the following error is returned:

{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "address.state",
            "message": "A required address parameter, state/province, is invalid."
        }
    ]
}
```
{% endcode %}

For a list of acceptable `state` values, refer to:

* [US states and territories](providing-address-information.md#us-states-and-territories)
* [Canadian provinces and territories](providing-address-information.md#canadian-provinces-and-territories)

## Ship from address

The checkout's `shipFrom` defines the address from which a physical product is shipped. It consists of child attributes `address` and `additionalAddressInfo`. Use `address` to provide [basic information](providing-address-information.md#basic-address-information) on the shipment's origin and `additionalAddressInfo` to give us more [detailed information](providing-address-information.md#additional-address-information).

The `shipFrom` parameter can be set at either the [checkout-level](providing-address-information.md#specifying-ship-from-at-the-checkout-level) or the [item-level](providing-address-information.md#specifying-ship-from-at-the-item-level). This allows you to build an order with items that ship from different addresses in different countries.

{% hint style="warning" %}
Your request however cannot contain a combination of `shipFrom` addresses that result in [more than one selling entity being assigned](selling-entities.md#determining-when-multiple-orders-are-required) to the transaction.
{% endhint %}

### Specifying ship from at the checkout-level

The checkout-level `shipFrom` is mapped to any [line items](describing-the-items/) that [contain a physical product](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) but don't have a `shipFrom` value.

Once the following `POST/checkouts` request is submitted, the second element in the `items` array will inherit the checkout-level `shipFrom` value.

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    ...
    "shipFrom": {
        "address": {
            "line1": "350 S 5th St",
            "city": "Minneapolis",
            "postalCode": "55415",
            "state": "MN",
            "country": "US"
        }
    },
    ...
    "items": [
        {
            "skuId": "bc4aab24-2880-4de7-b6b0-07dd6e6841a9",
            "price": 100.00,
            "quantity": 2,
            "shipFrom": {
                "address": {
                    "line1": "1800 Hiawatha Ave",
                    "city": "Minneapolis",
                    "postalCode": "55404",
                    "state": "MN",
                    "country": "US"
                }
            }
        },
        {
            "skuId": "bc4aab24-2880-4de7-b6b0-07dd6e6841a9",
            "price": 50.00,
            "quantity": 3
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

If you don't set the checkout-level `shipFrom`, and one or more physical line items don't specify a `shipFrom`, you can successfully create a checkout. In this case, though, [converting the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) returns the following `400 Bad Request`:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "shipFrom.address",
            "message": "A parameter is missing."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Specifying ship from at the item-level

By specifying `shipFrom` at the item-level, you can [build checkouts](./#creating-and-updating-the-checkout) containing [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) that ship from different countries. A `shipFrom` is not required at the line item-level unless no `shipFrom` is provided at the [checkout-level](providing-address-information.md#specifying-ship-from-at-the-checkout-level).

Additionally, any `shipFrom` values set at the item-level take priority over the checkout-level `shipFrom`.

## Ship to address

When an order contains [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), you're [required to provide a customer's shipping information](providing-address-information.md#ship-to-requirements).

{% hint style="warning" %}
In [registered checkouts](using-the-checkout-identifier.md#registered-checkouts-or-invoices), unless you're using version `2021-03-23` or earlier of the Digital River APIs, we do not use the associated [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `shipping` values to populate the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shipTo`.
{% endhint %}

You should use `address` to provide [basic information](providing-address-information.md#basic-address-information) on the shipment's destination and `additionalAddressInfo` to give us more [detailed information](providing-address-information.md#additional-address-information).

The `shipTo` and `shipping` hash tables also contain other child parameters that allow you to send the customer's `name`, `phone`, `email`, and `organization`.

## Bill to address

The `billTo` hash table contains child parameters `address` and `additionalAddressInfo`. You can use `address` to provide [basic information](providing-address-information.md#basic-address-information) on the customer's billing address and `additionalAddressInfo` to give us more [detailed information](providing-address-information.md#additional-address-information).

You can also use `billTo` to send non-address related information, such as the customer's `name`, `phone`, `email`, and `organization`.

In most scenarios, the `billTo` parameter is optional. However, if you only apply [secondary sources](../../../payments/payment-sources/using-the-source-identifier.md#secondary-payment-sources) to a transaction, then we do enforce [`billTo` requirements](providing-address-information.md#billing-address-requirements).

When [sequencing address information in your checkout workflows](providing-address-information.md#sequencing-address-information-in-checkout-workflows), you can use `billTo` to obtain an accurate tax calculation prior to attaching a payment source to the checkout. This is especially useful in transactions that only contain [digital products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital). In these types of transactions, [ship to information](providing-address-information.md#ship-to-address) is typically not sent in the request. Therefore, Digital River needs `billTo` to generate a tax estimate.

Once you [create an invoice](../../../developer-resources/digital-river-api-reference/invoices.md#creating-an-invoice) or [convert a checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), the response from the API includes `billTo`. This represents the billing address we used for tax computation purposes. Having this information allows you to precisely know what billing address information was used when calculating taxes. It also allows your integration to more easily retrieve any billing information that you might need to send in an email or other form of customer communications.

## Basic address information

An `Address` represents basic address information. The following provides a description of each parameter:

| Parameter    | Description                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `line1`      | The first line of the address                                                                                                                                                                                                                                                                                                                                                                               |
| `line2`      | The second line of the address.                                                                                                                                                                                                                                                                                                                                                                             |
| `postalCode` | <p>The postal code.<br><br>For United States addresses, Digital River supports ZIP+4 codes. They consist of the last four digits of a full nine-digit ZIP code. A nine-digit ZIP Code has two parts: the initial five digits of the zip code indicating the destination post office or delivery area and the last four digits representing a specific delivery route within that overall delivery area.</p> |
| `city`       | The city of the address                                                                                                                                                                                                                                                                                                                                                                                     |
| `state`      | The [state](providing-address-information.md#us-states-and-territories), county, province, or region.                                                                                                                                                                                                                                                                                                       |
| `country`    | A two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard.                                                                                                                                                                                                                             |

You can use the [CountrySpecs](country-specs.md) resource to retrieve [address schemas](country-specs.md#address-schemas) for many countries. These schemas define the required address parameters and provide regular expressions to validate postal code formats.

## Additional address information

Use `additionalAddressInfo` to capture any information that's not included in the basic `address`. This is especially useful for [Brazilian neighborhoods](providing-address-information.md#brazilian-neighborhoods) and [Japanese phonetics and divisions](providing-address-information.md#japanese-phonetics-and-divisions).

### Brazilian Neighborhoods

Brazilian addresses require a `neighborhood` for an order to be successfully created. The following example shows how to specify this value for an address in Brazil.

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '{
    ...
    "shipTo": {
        "address": {
            "line1": "Av. Paulista, 1098, 1º andar",
            "line2": "apto. 101",
            "city": "São Paulo",
            "postalCode": "01310-000",
            "state": "SP",
            "country": "BR"
        },
        "name": "João Ribeiro",
        "phone": "98765-4321",
        "email": "jribeiro@acme.com",
        "additionalAddressInfo": {
            "neighborhood": "Bela Vista"
        }
    },
    ...
}'
```
{% endtab %}
{% endtabs %}

### Japanese phonetics and divisions

For Japanese addresses, customers can provide their division within their organization (for example, the sales department). Additionally, customers can enter their name in two scripting styles: Hiragana and Katakana. Hiragana is the traditional script while Katakana is the phonetic spelling. Customer and courier services often want the phonetic spelling so they can correctly pronounce the customer's name when making a delivery. Katakana is also used by foreigners living in the country who don't have a Japanese name.

Use the `phoneticName` and `division` child attributes of `additionalAddressInfo` to provide this information:

{% tabs %}
{% tab title="cURL" %}
```
curl https://api.digtalriver.com/customers
     -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
     -d currency=JPY \
     -d email="shopxTest@digitalriver.com" \
     -d items[0][skuId]=sku_9234276173 \
     -d items[0][price]=9.29 \
     -d items[0][quantity]=2 \
     -d shipTo[name]="山田 太郎" \
     -d shipTo[phone]="03-1234-1234" \
     -d shipTo[email]="shopxTest@digitalriver.com" \
     -d shipTo[address][line1]="新宿区新宿1-1-1" \
     -d shipTo[address][line2]="新宿ビル203" \
     -d shipTo[address][city]="田原市" \
     -d shipTo[address][postalCode]="123-1234" \
     -d shipTo[address][country]="JP" \
     -d shipTo[additionalAddressInfo][phoneticName]="ヤマダ タロ" \  
     -d shipTo[additionalAddressInfo][division]="営業部" \         
     -d shipTo[amount]="5.95" \
     -d shippingChoice[name]="USPS: Priority (1 day delivery)"
```
{% endtab %}
{% endtabs %}

## US states and territories

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), the following [ship to](providing-address-information.md#ship-to-address) and [bill to](providing-address-information.md#bill-to-address) address `state` values can be used to represent American states, territories, APO/FPO military addresses, and the District of Columbia.

| Code | State          |
| ---- | -------------- |
| `AK` | Alaska         |
| `AL` | Alabama        |
| `AR` | Arkansas       |
| `AZ` | Arizona        |
| `CA` | California     |
| `CO` | Colorado       |
| `CT` | Connecticut    |
| `DE` | Delaware       |
| `FL` | Florida        |
| `GA` | Georgia        |
| `HI` | Hawaii         |
| `IA` | Iowa           |
| `ID` | Idaho          |
| `IL` | Illinois       |
| `IN` | Indiana        |
| `KS` | Kansas         |
| `KY` | Kentucky       |
| `LA` | Louisiana      |
| `MA` | Massachusetts  |
| `MD` | Maryland       |
| `ME` | Maine          |
| `MI` | Michigan       |
| `MN` | Minnesota      |
| `MO` | Missouri       |
| `MS` | Mississippi    |
| `MT` | Montana        |
| `NC` | North Carolina |
| `ND` | North Dakota   |
| `NE` | Nebraska       |
| `NH` | New Hampshire  |
| `NJ` | New Jersey     |
| `NM` | New Mexico     |
| `NV` | Nevada         |
| `NY` | New York       |
| `OH` | Ohio           |
| `OK` | Oklahoma       |
| `OR` | Oregon         |
| `PA` | Pennsylvania   |
| `RI` | Rhode Island   |
| `SD` | South Dakota   |
| `SC` | South Carolina |
| `TN` | Tennessee      |
| `TX` | Texas          |
| `UT` | Utah           |
| `VA` | Virginia       |
| `VT` | Vermont        |
| `WA` | Washington     |
| `WI` | Wisconsin      |
| `WV` | West Virginia  |
| `WY` | Wyoming        |

| Code | Federal District     |
| ---- | -------------------- |
| `DC` | District of Columbia |

| Code | Territory                      |
| ---- | ------------------------------ |
| `AS` | American Samoa                 |
| `FM` | Federated States Of Micronesia |
| `GU` | Guam                           |
| `MH` | Marshall Islands               |
| `MP` | Northern Mariana Islands       |
| `PR` | Puerto Rico                    |
| `PW` | Palau                          |
| `VI` | U.S. Virgin Islands            |

| Code | APO/FPO Military Addresses |
| ---- | -------------------------- |
| `AE` | Armed Forces               |
| `AP` | Armed Forces Pacific       |
| `AA` | Armed Forces America       |

## Canadian provinces and territories

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), the following [ship to](providing-address-information.md#ship-to-address) and [bill to](providing-address-information.md#bill-to-address) address `state` values can be used to represent Canadian provinces and territories.

| Code | Province                  |
| ---- | ------------------------- |
| `AB` | Alberta                   |
| `BC` | British Columbia          |
| `MB` | Manitoba                  |
| `NB` | New Brunswick             |
| `NL` | Newfoundland and Labrador |
| `NS` | Nova Scotia               |
| `ON` | Ontario                   |
| `PE` | Prince Edward Island      |
| `QC` | Quebec                    |
| `SK` | Saskatchewan              |
|      |                           |

| Code | Territory             |
| ---- | --------------------- |
| `NT` | Northwest Territories |
| `NU` | Nunavut               |
| `YT` | Yukon                 |
