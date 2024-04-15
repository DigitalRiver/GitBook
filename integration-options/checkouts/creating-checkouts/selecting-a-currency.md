---
description: >-
  Learn how to determine whether a currency is supported and how it is
  prioritized.
---

# Selecting a currency

[Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) require a  `currency` that conforms to the [ISO 4217](https://www.xe.com/iso4217.php) standard.

However, not all currencies contained in the ISO 4217 list are supported in the Digital River APIs. Instead, the `currency` you pass must be [supported by the payment method](selecting-a-currency.md#supported-currencies) used to fund the transaction.&#x20;

You should also remember that the `currency` you send in a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts) or [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts) always [takes priority](selecting-a-currency.md#how-currency-is-prioritized) over the value you pass when [creating the payment source](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources).

## Supported currencies

To access a list of available currencies for each [supported payment method](../../../payments/supported-payment-methods/), refer to the [Payment method guide](https://www.digitalriver.com/payment-method-guide/).&#x20;

If the `currency` you send in a [create or update Checkout](./) request is not supported by the [source](../../../payments/payment-sources/), you receive the following error:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "currency_unactivated",
            "parameter": "currency",
            "message": "Currency 'PAB' is not activated."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

You might also receive a `409 Conflict` response that contains a `code` of `invalid_parameter`. In this case, the error could have been thrown because `currency` consisted of incorrect characters, an obsolete, Euro-zone currency, or another currency no longer in circulation.

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "currency",
            "message": "'YEM' is not a valid currency."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## How currency is prioritized

For some payment methods, it's required that you set `currency` in the configuration object of [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources), while for others it's optional.&#x20;

However, if you do pass `currency`, and then [attach the source to a checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts), the [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) `currency` doesn't need to match the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `currency`. Both values just have to be [supported by the underlying payment method](selecting-a-currency.md#supported-currencies).&#x20;

The [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `currency` always takes priority over the [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) `currency`. This means, upon [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) creation, we [generate a charge](../../../order-management/orders/payment-charges/#how-a-charge-is-created) in the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `currency`.

The following example demonstrates this concept. In this case, a payment source created in `USD` is [attached to a checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) with a `currency` of `HKD`. After the [checkout is converted to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)  `payment.charges[].currency` is also `HKD`.

{% tabs %}
{% tab title="Source" %}
```javascript
{
    "clientId": "gc",
    "channelId": "headless",
    "liveMode": false,
    "id": "721adac5-cbfa-4f4f-989b-58414dd231c3",
    "clientSecret": "721adac5-cbfa-4f4f-989b-58414dd231c3_1e2b0d18-d57f-4033-b4c9-ce1e8a83e7cc",
    "type": "creditCard",
    "reusable": false,
    "owner": {
        "firstName": "William",
        "lastName": "Brown",
        "email": "null@digitalriver.com",
        "address": {
            "line1": "10381 Bren Rd W",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55343"
        }
    },
    "state": "chargeable",
    "creationIp": "209.87.180.27",
    "createdTime": "2021-04-30T19:16:51.525Z",
    "updatedTime": "2021-04-30T19:16:51.525Z",
    "flow": "standard",
    "browserInfo": {
        "userAgent": "PostmanRuntime/7.28.0",
        "acceptHeader": "*/*",
        "browserIp": "209.87.180.27"
    },
    "creditCard": {
        "brand": "Visa",
        "expirationMonth": 7,
        "expirationYear": 2027,
        "lastFourDigits": "1111",
        "paymentIdentifier": "00700"
    }
}
```
{% endtab %}

{% tab title="Checkout" %}
```javascript
{
    "id": "b6992697-e621-4043-8e5a-1a7898320c9c",
    "createdTime": "2021-04-30T19:15:52Z",
    "currency": "HKD",
    "email": "anyemail@digitalriver.com",
    "shipTo": {
        "address": {
            "line1": "10380 Bren Road W",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        },
        "name": "John Doe"
    },
    "shipFrom": {
        "address": {
            "country": "US"
        }
    },
    "totalAmount": 26.89,
    "subtotal": 25.0,
    "totalFees": 0.0,
    "totalTax": 1.89,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 5.0,
    "items": [
        {
            "id": "5e59eb4f-f2fb-4741-981c-5c5e2cff88b2",
            "skuId": "9289476d-660a-4631-abf4-9bf48f260449",
            "amount": 20.0,
            "quantity": 2,
            "tax": {
                "rate": 0.07525,
                "amount": 1.51
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
        "taxAmount": 0.38
    },
    "updatedTime": "2021-04-30T19:15:52Z",
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
                "id": "721adac5-cbfa-4f4f-989b-58414dd231c3",
                "type": "creditCard",
                "amount": 26.89,
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
            "id": "b22ac65b-499c-4809-8737-bf0b5ec2e447",
            "amountContributed": 26.89,
            "amountRemainingToBeContributed": 0.0,
            "state": "requires_confirmation",
            "clientSecret": "b22ac65b-499c-4809-8737-bf0b5ec2e447_0b250864-490c-447d-8dde-9d85d6c013bf"
        }
    }
}
```
{% endtab %}

{% tab title="Order" %}
```javascript
{
    "id": "188601460336",
    "createdTime": "2021-04-30T19:23:13Z",
    "currency": "HKD",
    "email": "anyemail@digitalriver.com",
    "shipTo": {
        "address": {
            "line1": "10380 Bren Road W",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        },
        "name": "John Doe"
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
    "totalAmount": 26.89,
    "subtotal": 25.0,
    "totalFees": 0.0,
    "totalTax": 1.89,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 5.0,
    "items": [
        {
            "id": "110117910336",
            "skuId": "9289476d-660a-4631-abf4-9bf48f260449",
            "amount": 20.0,
            "quantity": 2,
            "state": "created",
            "stateTransitions": {
                "created": "2021-04-30T19:23:13Z"
            },
            "tax": {
                "rate": 0.07525,
                "amount": 1.51
            },
            "importerTax": {
                "amount": 0.0
            },
            "duties": {
                "amount": 0.0
            },
            "availableToRefundAmount": 0.0,
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
        "taxAmount": 0.38
    },
    "updatedTime": "2021-04-30T19:23:13Z",
    "locale": "en_US",
    "customerType": "individual",
    "sellingEntity": {
        "id": "C5_INC-ENTITY",
        "name": "DR globalTech Inc."
    },
    "liveMode": false,
    "payment": {
        "charges": [
            {
                "id": "82cbbfa5-e324-46fd-971c-7130eb10ccd3",
                "createdTime": "2021-04-30T19:23:16Z",
                "currency": "HKD",
                "amount": 26.89,
                "state": "capturable",
                "captured": false,
                "refunded": false,
                "sourceId": "721adac5-cbfa-4f4f-989b-58414dd231c3",
                "type": "customer_initiated"
            }
        ],
        "sources": [
            {
                "id": "721adac5-cbfa-4f4f-989b-58414dd231c3",
                "type": "creditCard",
                "amount": 26.89,
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
            "id": "b22ac65b-499c-4809-8737-bf0b5ec2e447",
            "amountContributed": 26.89,
            "amountRemainingToBeContributed": 0.0,
            "state": "complete",
            "clientSecret": "b22ac65b-499c-4809-8737-bf0b5ec2e447_0b250864-490c-447d-8dde-9d85d6c013bf"
        }
    },
    "state": "accepted",
    "stateTransitions": {
        "accepted": "2021-04-30T19:23:16Z"
    },
    "fraudState": "passed",
    "fraudStateTransitions": {
        "passed": "2021-04-30T19:23:16Z"
    },
    "requestToBeForgotten": false,
    "capturedAmount": 0.0,
    "cancelledAmount": 0.0,
    "availableToRefundAmount": 0.0,
    "checkoutId": "b6992697-e621-4043-8e5a-1a7898320c9c"
}
```
{% endtab %}
{% endtabs %}
