---
description: Learn how to create guest and registered checkouts
---

# Checking out guest and registered customers

A [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `customerId` references the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) making the purchase. You can pass this identifier in both [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) and [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) checkout requests.

{% hint style="success" %}
For more information, refer to [sequencing the checkout process](./#sequencing-the-checkout-process) on the [Building checkouts](./) page.
{% endhint %}

If you want to process a [guest checkout](using-the-checkout-identifier.md#guest-checkouts-or-invoices), then don't set `customerId`. Conversely, if you want to process a [registered checkout](using-the-checkout-identifier.md#registered-checkouts-or-invoices), then you should set `customerId`.

## Guest checkouts <a href="#guest-checkouts-or-invoices" id="guest-checkouts-or-invoices"></a>

If you don't set a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `customerId`, then no [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) is associated with the purchase. So, when you want to checkout a guest, don't send `customerId` in the body of a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) request.

In guest checkout scenarios, you'll need to acquire a customer's shipping address (assuming the cart contains [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital)), billing address and email address. In addition, you must create one or more payment [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), and, when [required](tax-identifiers.md#missing-tax-identifier-notifications), you'll also need to create a [tax identifier.](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers)

Once you obtain these addresses and create these resources, you must associate their data with the checkout.

| Guest customer          |       | Checkout            |
| ----------------------- | :---: | ------------------- |
| Shipping details        | **➔** | `shipTo`            |
| Billing details         | **➔** | `billTo`            |
| Email address           | **➔** | `email`             |
| Tax identifiers         | **➔** | `taxIdentifiers[]`  |
| Business or individual? | **➔** | `type`              |
| Payment method(s)       | **➔** | `payment.sources[]` |

For more information refer to:

* [Address requirements](providing-address-information.md#address-requirements-and-validations) on the [Providing address information](providing-address-information.md) page
* [Creating sources ](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources)and [attaching sources to checkouts](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) on the [Managing sources](../../../payments/payment-sources/using-the-source-identifier.md) page
* [Creating tax identifiers](tax-identifiers.md#creating-tax-identifiers) and [attaching tax identifiers to checkouts](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices) on the [Tax identifiers](tax-identifiers.md) page

## Registered checkouts <a href="#registered-checkouts-or-invoices" id="registered-checkouts-or-invoices"></a>

When [checking out](./) a registered customer, make sure you send `customerId` in the body of a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) request. This associates the referenced [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) with the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

When developing registered checkout flows, you should be aware of (1) [what attributes customers and checkouts have in common](using-the-checkout-identifier.md#common-attributes) and (2) [how customer data can be passed to the checkout](using-the-checkout-identifier.md#passing-customer-data-to-checkouts).

### Common attributes

[Customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) and [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) have some common attributes. In registered checkouts, the following data in a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) can be passed to a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). The options that exist for [passing this customer data to checkouts](using-the-checkout-identifier.md#passing-customer-data-to-checkouts) are version dependent.

| Customer           |       | Checkout            |
| ------------------ | :---: | ------------------- |
| `shipping`         | **➔** | `shipTo`            |
| `sources[].owner`  | **➔** | `billTo`            |
| `sources[]`        | **➔** | `payment.sources[]` |
| `taxIdentifiers[]` | **➔** | `taxIdentifiers[]`  |
| `locale`           | **➔** | `locale`            |
| `email`            | **➔** | `email`             |
| `customerType`     | **➔** | `type`              |

For more information refer to:

* [Address requirements](providing-address-information.md#address-requirements-and-validations) on the [Providing address information](providing-address-information.md) page
* [Creating sources](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources), [authenticating sources](../../../payments/payment-sources/using-the-source-identifier.md#authenticating-sources), [saving sources to customers](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers), and [attaching sources to checkouts](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) on the [Managing sources](../../../payments/payment-sources/using-the-source-identifier.md) page
* The [Tax identifiers](tax-identifiers.md) page

### Passing customer data to checkouts

In registered checkouts, the [Digital River APIs version](../../../general-resources/versioning.md) you're using determines how customer data can be passed to checkouts:

#### Version `2021-12-13` and later

In versions `2021-12-13` and later, when you associate a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) with a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), Digital River doesn't, by default, pass that [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) data to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). In other words, undefined [common attributes](using-the-checkout-identifier.md#common-attributes) in a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) are not populated with the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) data.

Instead, once registered customers have signed on to your site and you've obtained their unique identifier, you can make a [`GET/customers/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveCustomers) request to retrieve their shipping address, saved payment sources, billing addresses associated with those sources, tax identifiers, and other personal information.

At each stage of the checkout process, you can present this saved information to customers as an available option. Whether customers select the saved option presented to them or they use your site's forms to enter new information, you must pass this data to the checkout.

For example, when obtaining a ship to address in a checkout that contains [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), you can get the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `shipping`, display it as an available option, and ask customers whether they want to use this saved address. Regardless of whether customers select the saved address or enter a new address, you must set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shipTo`.

#### Version `2021-03-23` and earlier

In versions `2021-03-23` and earlier, when you associate a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) with a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), Digital River by default passes the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) data to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). In other words, any undefined [common attribute](using-the-checkout-identifier.md#common-attributes) in the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) is automatically inherited from the associated [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).

The only exception is `taxIdentifiers[]`. Unless applicable to the transaction, we don't pass any of a [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `taxIdentifiers[]` to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). For more information, refer to [using tax identifiers in registered checkouts](tax-identifiers.md#using-tax-identifiers-in-registered-checkouts) on the [Tax identifiers](tax-identifiers.md) page.

{% hint style="info" %}
Data you set in the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) takes precedence over inherited [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) data. Additionally, any data inherited by default from the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) can always be overwritten in subsequent [update checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts).
{% endhint %}

For example, the following [create checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) contains a `customerId` but doesn't specify `email`, `shipTo`, `billTo`, `locale`, `customerType`, `taxIdentifiers[]` or `sourceId`.

{% tabs %}
{% tab title="POST/checkouts" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "currency": "USD",
    "customerId": 531718920336,
    "taxInclusive": false,
    "shipFrom": {
        "address": {
            "country": "US"
        }
    },
    "shippingChoice": {
        "amount": 5,
        "description": "standard",
        "serviceLevel": "SG"
    },
    "items": [
        {
            "skuId": "25b3f1cf-a6d0-439a-b8e6-7e506452f717",
            "quantity": 2,
            "price": 10
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

Once you submit this request, Digital River determines what [common attributes](using-the-checkout-identifier.md#common-attributes), if any, are undefined in the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), whether the associated [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) contains any of these undefined attributes, and, if it does, retrieves that data and sends it to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

In this particular example, Digital River uses the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `email`, `shipping`, `defaultSourceId`, `locale`, and `type` to set the corresponding [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) attributes. Note that the `owner.address`, `owner.firstName`, `owner.lastName`, and `owner.email` in the customer's [default payment source](../../../payments/payment-sources/using-the-source-identifier.md#setting-the-default-payment-source) are used to populate the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `billTo`.

{% tabs %}
{% tab title="Customer" %}
```javascript
{
    "id": "531718920336",
    "createdTime": "2021-04-12T20:39:42Z",
    "email": "jdoe@digitalriver.com",
    "shipping": {
        "address": {
            "line1": "123 Boulevard",
            "city": "Saint Paul",
            "postalCode": "55155",
            "state": "MN",
            "country": "US"
        },
        "name": "John Doe",
        "phone": "555-555-5555"
    },
    "defaultSourceId": "5349c370-6694-45ff-915a-882e9b62b48d",
    "sources": [
        {
            "id": "5349c370-6694-45ff-915a-882e9b62b48d",
            "createdTime": "2021-04-12T20:40:26Z",
            "type": "creditCard",
            "reusable": true,
            "state": "chargeable",
            "owner": {
                "firstName": "William",
                "lastName": "Brown",
                "email": "null@digitalriver.com",
                "address": {
                    "line1": "10381 Bren Rd W",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "state": "MN",
                    "country": "US"
                }
            },
            "clientSecret": "5349c370-6694-45ff-915a-882e9b62b48d_65525173-9ad9-4339-ba97-f889daf435c6",
            "creditCard": {
                "brand": "Visa",
                "expirationMonth": 7,
                "expirationYear": 2027,
                "lastFourDigits": "1111"
            }
        }
    ],
    "enabled": true,
    "requestToBeForgotten": false,
    "locale": "en_US",
    "type": "individual",
    "liveMode": false
}
```
{% endtab %}

{% tab title="Checkout" %}
```javascript
{
    "id": "37a9569d-b23f-4d3e-b967-8dacb3427cc9",
    "createdTime": "2021-04-12T20:43:18Z",
    "customerId": "531718920336",
    "currency": "USD",
    "email": "jdoe@digitalriver.com",
    "shipTo": {
        "address": {
            "line1": "123 Boulevard",
            "city": "Saint Paul",
            "postalCode": "55155",
            "state": "MN",
            "country": "US"
        },
        "name": "John Doe",
        "phone": "555-555-5555"
    },
    "shipFrom": {
        "address": {
            "country": "US"
        }
    },
    "billTo": {
        "address": {
            "line1": "10381 Bren Rd W",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        },
        "name": "William Brown",
        "email": "null@digitalriver.com"
    },
    "totalAmount": 26.97,
    "subtotal": 25.0,
    "totalFees": 0.0,
    "totalTax": 1.97,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 5.0,
    "items": [
        {
            "id": "3a1fc426-87fb-4216-8619-2d29ac2d5818",
            "skuId": "25b3f1cf-a6d0-439a-b8e6-7e506452f717",
            "amount": 20.0,
            "quantity": 2,
            "tax": {
                "rate": 0.07875,
                "amount": 1.58
            },
            "importerTax": {
                "amount": 0.0
            },
            "duties": {
                "amount": 0.0
            },
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            }
        }
    ],
    "shippingChoice": {
        "amount": 5.0,
        "description": "standard",
        "serviceLevel": "SG",
        "taxAmount": 0.39
    },
    "updatedTime": "2021-04-12T20:43:18Z",
    "locale": "en_US",
    "customerType": "individual",
    "sellingEntity": {
        "id": "C5_INC-ENTITY",
        "name": "DR globalTech Inc."
    },
    "liveMode": false,
    "payment": {
        "sources": [
            {
                "id": "5349c370-6694-45ff-915a-882e9b62b48d",
                "type": "creditCard",
                "amount": 26.97,
                "owner": {
                    "firstName": "William",
                    "lastName": "Brown",
                    "email": "null@digitalriver.com",
                    "address": {
                        "line1": "10381 Bren Rd W",
                        "city": "Minnetonka",
                        "postalCode": "55343",
                        "state": "MN",
                        "country": "US"
                    }
                },
                "creditCard": {
                    "brand": "Visa",
                    "expirationMonth": 7,
                    "expirationYear": 2027,
                    "lastFourDigits": "1111"
                }
            }
        ],
        "session": {
            "id": "55b44240-577c-4485-af5a-2c8224cb6653",
            "amountContributed": 26.97,
            "amountRemainingToBeContributed": 0.0,
            "state": "requires_confirmation",
            "clientSecret": "55b44240-577c-4485-af5a-2c8224cb6653_87c01674-8312-4f3a-afc7-7b2714fd47e8"
        }
    }
}
```
{% endtab %}
{% endtabs %}
