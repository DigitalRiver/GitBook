---
description: Gain a better understanding of how to use the checkout's taxInclusive flag
---

# Configuring taxes

During [checkouts](./), you can specify whether or not taxes are included in your product and shipping prices.&#x20;

On this page, you'll find information on how to use the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `taxInclusive` flag to:

* [Pass tax inclusive prices](configuring-taxes.md#passing-tax-inclusive-prices)
* [Pass tax exclusive prices](configuring-taxes.md#passing-tax-exclusive-prices)

## Passing tax inclusive prices

If you want Digital River to subtract taxes from `shippingChoice.amount` and each `items[].price`, set `taxInclusive` to `true`.

{% tabs %}
{% tab title="POST /checkouts" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
...
--data-raw '{
    "currency": "USD",
    "taxInclusive": true,
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
    "shippingChoice": {
        "amount": 5,
        "description": "standard",
        "serviceLevel": "SG"
    },
    "items": [
        {
            "skuId": "ed7b06bd-7b2e-4525-9156-cd6fcbe7fe42",
            "quantity": 2,
            "price": 10
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

With this configuration, Digital River computes shipping and line-item taxes and then subtracts these computed values from the prices you passed in the request.

In the response, we provide an updated `shippingChoice.amount` and the computed `shippingChoice.taxAmount` and do the same for each `items[]`.

The checkout's `subtotal` represents the pre-tax price of its `items[]` and `shippingChoice.amount` and `totalTax` aggregates `shippingChoice` and `items[]` taxes.

{% tabs %}
{% tab title="Checkout" %}
```javascript
{
    "id": "7ffe373b-b358-4c76-8210-5dc118ce77ae",
    ...
    "totalAmount": 25.03,
    "subtotal": 23.28,
    "totalFees": 0.0,
    "totalTax": 1.75,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 4.68,
    "items": [
        {
            "id": "1d99324f-6afa-4a90-808b-9d1234e2fc92",
            "skuId": "ed7b06bd-7b2e-4525-9156-cd6fcbe7fe42",
            "amount": 18.6,
            "quantity": 2,
            "tax": {
                "rate": 0.07525,
                "amount": 1.4
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
        "amount": 4.68,
        "description": "standard",
        "serviceLevel": "SG",
        "taxAmount": 0.35
    },
    ...
}
```
{% endtab %}
{% endtabs %}

## Passing tax exclusive prices

If you want Digital River to add taxes to the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shippingChoice.amount` and each `items[].price`, set `taxInclusive` to `false`.

{% tabs %}
{% tab title="POST /checkouts" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
...
--data-raw '{
    "currency": "USD",
    "taxInclusive": false,
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
    "shippingChoice": {
        "amount": 5,
        "description": "standard",
        "serviceLevel": "SG"
    },
    "items": [
        {
            "skuId": "ed7b06bd-7b2e-4525-9156-cd6fcbe7fe42",
            "quantity": 2,
            "price": 10
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

With this configuration, Digital River computes shipping and line-item taxes and returns these values in `shippingChoice.taxAmount` and `items[].tax.amount` .

Note that `shippingChoice.amount` remains the same as the value sent in the request. Likewise, each `items[].amount` equals the aggregated `price` in the request.

{% tabs %}
{% tab title="Checkout" %}
```javascript
{
    "id": "288ef50f-6b23-40ae-a8ad-3048b7f99ccf",
    ...
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
            "id": "b5125c43-dc3b-4da4-a299-d8d0734f2873",
            "skuId": "ed7b06bd-7b2e-4525-9156-cd6fcbe7fe42",
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
    ...
}
```
{% endtab %}
{% endtabs %}

## Guidelines for displaying tax

The display of tax during the checkout experience should follow [these guidelines](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sysparm\_article=KB0010559\&sys\_kb\_id=a6423b4c1b769090f4304158dc4bcbc3\&spa=1) _(_[_access required_](../../../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools)_)_.
