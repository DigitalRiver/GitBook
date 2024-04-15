---
description: >-
  Learn how to add multiple items that share the same SKU identifier‌ to a
  Checkout or Invoice.
---

# Managing items with shared SKU identifiers

In a single Checkout or Invoice, you can add multiple [line items](../../../../order-management/creating-and-updating-an-order.md#line-items) that share a [SKU identifier](../../../../product-management/creating-and-updating-skus.md#specifying-a-sku-identifier) but differ in [price](price-of-an-item.md) , [discount type](../applying-a-discount.md), or [subscription details](../../subscriptions/subscription-information-1.md).‌

The following sections demonstrate how items that share a `skuId` can be differentiated based on [price](managing-items-with-shared-sku-identifiers.md#setting-different-prices) and [subscription information](managing-items-with-shared-sku-identifiers.md#handling-multiple-subscription-requests) and how each item is assigned a [unique identifier in the Order response](../../../../order-management/creating-and-updating-an-order.md#line-items).

## Setting different prices

This [create Checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) request contains two items with the same `skuId` but different `price` values. In addition, one item has a `discount` applied to it.

{% tabs %}
{% tab title="curl" %}
```
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '
{
    "currency": "USD",
    "customerId": "987654321",
    "items": [
        {
            "skuId": "05081978",
            "price": 100.00,
            "quantity": 1
        },
        {
            "skuId": "05081978",
            "price": 90.00,
            "quantity": 1,
            "discount":
            {
                "percentOff": 10
            }
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

Even though they share the same `skuId`, Digital River handles both items separately, returning different `amount` and `tax.amount` values for each.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "177406730336",
...
    "items": [
        {
            "skuId": "05081978",
            "amount": 100.0,
            "quantity": 1,
            "tax": {
                "rate": 0.07125,
                "amount": 7.13
            }
        },
        {
            "skuId": "05081978",
            "amount": 81.0,
            "quantity": 1,
            "discount": {
                "percentOff": 10.0,
                "quantity": 1
            },
            "tax": {
                "rate": 0.07125,
                "amount": 5.77
            }
        }
    ],
...
}
```
{% endtab %}
{% endtabs %}

The returned checkout `id` can then be used to [create an Order](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createOrders). In the response to that `POST/orders` request, each element of the `items` array has been assigned a unique `itemId`.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "177406750336",
...
    "items": [
        {
            "itemId": "96361160336",
            "skuId": "05081978",
            "amount": 100.0,
            "quantity": 1,
...
            "tax": {
                "rate": 0.07125,
                "amount": 7.13
            }
        },
        {
            "itemId": "96361170336",
            "skuId": "05081978",
            "amount": 81.0,
            "quantity": 1,
            "discount": {
                "percentOff": 10.0,
                "quantity": 1
            },
...
            "tax": {
                "rate": 0.07125,
                "amount": 5.77
            }
        }
    ],
...
}
```
{% endtab %}
{% endtabs %}

## Handling multiple subscription requests

Perhaps you have a customer who wants to purchase an auto-renew digital magazine subscription for himself and another, nearly identical subscription for a friend. The only difference is that the subscription for the friend must be manually renewed.

In the [create Checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [create Invoice](../../subscriptions/invoices.md#creating-an-invoice) request, assign each item the same `skuId` but different `autoRenewal` and `subscriptionId` values.

{% tabs %}
{% tab title="curl" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '{
    "currency": "USD",
    "customerId": "987654321",
    "items": [
        {
            "skuId": "08141946",
            "subscriptionInfo": {
                "autoRenewal": true,
                "terms": "Insert terms here",
                "subscriptionId": "123"
            },
            "price": 100,
            "quantity": 1
        },
        {
            "skuId": "08141946",
            "subscriptionInfo": {
                "autoRenewal": false,
                "terms": "Insert terms here",
                "subscriptionId": "321"
            },
            "price": 75,
            "quantity": 1
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

The returned checkout `id` can then be used to [create an Order](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createOrders). In the response to that `POST/orders` request, each element of the `items` array has been assigned a unique `itemId`. These identifiers are used to [create](../../../../order-management/informing-digital-river-of-a-fulfillment.md) and [cancel](../../../../order-management/informing-digital-river-of-a-fulfillment.md) [fulfillments](../../../../order-management/fulfillments.md) and process [returns](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/integration-options/checkouts/creating-checkouts/describing-the-items/broken-reference/README.md) and [refunds](../../../../order-management/returns-and-refunds-1/refunds/).

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "177433630336",
    ...
    "items": [
        {
            "itemId": "96392860336",
            "skuId": "08141946",
            ...
            "subscriptionInfo": {
                "subscriptionId": "123",
                "terms": "Insert terms here",
                "autoRenewal": true,
                "freeTrial": false
            }
        },
        {
            "itemId": "96392870336",
            "skuId": "08141946",
            ...
            "subscriptionInfo": {
                "subscriptionId": "321",
                "terms": "Insert terms here",
                "autoRenewal": false,
                "freeTrial": false
            }
        }
    ],
...
}
```
{% endtab %}
{% endtabs %}
