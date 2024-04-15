---
description: Learn more about the orders resource
---

# Orders

[Orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) handle the purchases of customers. When you create an order, you are instructing Digital River, as the [authorized reseller](../../), to send an authorization request that starts the collection process.

An order's data persist, acting as a permanent record of the sale, which Digital River is required to maintain for auditing purposes.

An order maintains an enduring record of when it was placed, a [charge is created](payment-charges/#how-a-charge-is-created) and [captured](payment-charges/#captures), a [refund](../returns-and-refunds-1/refunds/) is processed, and other key events in the [order lifecycle](the-order-lifecycle.md) occur. More specifically, an order persists:

* The total [refunded](payment-charges/#refunds), [cancelled](payment-charges/#cancels), and [captured](payment-charges/#captures) payment amounts
* A [charge](payment-charges/) containing a [payment source](../../payments/payment-sources/), an amount charged to that source, and the [state of the charge](payment-charges/#the-charge-lifecycle)

The following diagram depicts the relationship between an order and other resources in the Digital River APIs.

![](<../../.gitbook/assets/Order-object (1).png>)

To ensure that your integration is functioning properly, you can create test orders using the information contained in the [Testing Scenarios](../../developer-resources/testing-scenarios.md) page.

## The orders resource

In the following section, you'll find information on some of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) attributes and how you might use them in downstream requests. For a complete list, refer to the [Orders API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) reference documentation.

### Unique identifier

An [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) contains a unique `id`. You can use this identifier when [initiating physical fulfillments](../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md), [cancelling shipments](../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/instructing-digital-to-cancel-items.md), [capturing and cancelling payments](../informing-digital-river-of-a-fulfillment.md), [creating physical returns](../returns-and-refunds-1/returns/digital-river-coordinated-returns.md), [handling third-party returns](../returns-and-refunds-1/returns/creating-a-return.md), and [issuing refunds](../returns-and-refunds-1/refunds/issuing-refunds.md).

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "177452480336",
    ...
```
{% endtab %}
{% endtabs %}

### Ship to values

An order's `shipTo` values are displayed on [invoices and credit memos](../accessing-invoices-and-credit-memos.md).

```javascript
    ...
    "customerId": "987654321",
    ...
    "shipTo": {
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "string",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        },
        "name": "Jane Doe",
        "phone": "952-111-1111",
        "email": "jdoe@digitalriver.com",
        "organization": "Digital River"
    },
```

### Amounts, fees, and taxes

The order's total amount, [fees](../../product-management/regulatory-fees/), taxes, and other costs are the same as those presented to customers when they confirmed the purchase. You can retrieve these values and display them to customers on their order confirmation page.

```javascript
    ...
    "totalAmount": 177.67,
    "subtotal": 172.5,
    "totalFees": 0.0,
    "totalTax": 5.17,
    "totalDuty": 0.0,
    "totalDiscount": 7.5,
    "totalShipping": 5.0,
    ...
```

### Line items

Digital River assigns each of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `items[]` a unique `id`. You need this identifier when [capturing and cancelling payments](../informing-digital-river-of-a-fulfillment.md), [handling third-party returns](../returns-and-refunds-1/returns/creating-a-return.md), and [issuing refunds](../returns-and-refunds-1/refunds/issuing-refunds.md).&#x20;

Depending on how you [send product data in checkouts](../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data), each of an order's `items[]` also contains either a [`skuId`](../../product-management/skus.md#product-details) or a [`productDetails`](../../product-management/skus.md#product-details) object.

In addition, these `items[]`  store detailed price, tax, and quantity information that you can display to customers on order confirmation and order detail pages.

For more information on `subscriptionInfo`, refer to the [Subscription information](../../integration-options/checkouts/subscriptions/subscription-information-1.md) page.

```javascript
    ...
    "items": [
        {
            "id": "96415480336",
            "skuId": "08141946",
            "amount": 100.0,
            "quantity": 1,
            "state": "created",
            "stateTransitions": {
                "created": "2020-05-21T17:26:34Z"
            },
            "tax": {
                "rate": 0.0,
                "amount": 0.0
            },
            "subscriptionInfo": {
                "billingAgreementId": "cfeba2ac-d532-49e4-99f4-7a433507facf",
                "terms": "Insert terms here",
                "autoRenewal": true,
                "freeTrial": false
            }
        },
        {
            "id": "96415490336",
            "skuId": "05081978",
            "amount": 67.5,
            "quantity": 1,
            "discount": {
                "percentOff": 10.0,
                "quantity": 1
            },
            "state": "created",
            "stateTransitions": {
                "created": "2020-05-21T17:26:34Z"
            },
            "tax": {
                "rate": 0.07125,
                "amount": 4.81
            }
        }
    ],
    ...
```

### Tax invoices and credit memos

In most cases, Digital River populates an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `invoicePDFs` and `creditMemoPDFs` with information that you can use to [access and share tax invoice and credit memo files](../accessing-invoices-and-credit-memos.md).

```javascript
    ...
    "invoicePDFs": [
        {
            "url": "https://api.digitalriver.com/files/23c7e1a5-25e4-41a9-b935-eda98dfa238b/content",
            "id": "23c7e1a5-25e4-41a9-b935-eda98dfa238b"
        }
    ],
    "creditMemoPDFs": [
        {
            "url": "https://api.digitalriver.com/files/5cec4a32-853f-485a-90a0-15ea0a614355/content",
            "id": "5cec4a32-853f-485a-90a0-15ea0a614355"
        }
    ],
    ...
```

### State and fraud state

For more information about an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` and `fraudState`, refer to the [Order lifecycle](the-order-lifecycle.md) page.

### Tax identifiers

Orders with [applied tax identifiers](../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#applying-tax-identifiers) contain an array of [tax identifier objects](../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#the-tax-identifier-object).

{% tabs %}
{% tab title="JSON" %}
```javascript
  ...
  "taxIdentifiers": [{
        "id": "a6809a63-e6a9-4016-abbc-f33d19fccb5b",
        "customerId": "5774321009",
        "type": "uk",
        "value": "GB000283536",
        "state": "verified",
        "stateTransitions":
             {"pending": "2020-05-13T11:00:00.000Z", "verified": "2020-05-15T16:00:00.000Z"},
        "verified_name": "Descon Ltd",
        "verified_address": "Design House, 18b Tromode, Isle of Man",
        "createdTime": "2020-08-01T02:25:53Z",
        "updatedTime": "2020-08-01T05:47:21Z"
    }],
   ...
```
{% endtab %}
{% endtabs %}

### Charges

An [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `charges[]` contains one or more elements, each representing a [charge](payment-charges/) created from a [primary or secondary payment source](../../payments/payment-sources/using-the-source-identifier.md#primary-versus-secondary-sources). Each charge contains a unique identifier, an `amount`, a [`state`](payment-charges/#the-charge-lifecycle), and the identifier of the [payment source](../../payments/payment-sources/) used to create the charge.

```javascript
    ...
    "charges": [
        {
            "id": "d3a02b03-1378-431e-81a5-9cb6dd54d90b",
            "createdTime": "2020-05-21T17:26:37Z",
            "currency": "USD",
            "amount": 177.67,
            "state": "capturable",
            "captured": false,
            "refunded": false,
            "sourceId": "deabb3a4-14e4-4702-a13b-ddaac23277d3"
        }
    ],
    ...
```

### Request to be forgotten

An [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `requestToBeForgotten` indicates whether an order's data is scheduled for deletion. This is the only attribute (other than `metadata`) that can be modified in an update order request.

```javascript
    ...
    "requestToBeForgotten": false,
    ...
}
```

{% swagger src="../../.gitbook/assets/2021-12-13.json" path="/orders/{id}" method="get" %}
[2021-12-13.json](../../.gitbook/assets/2021-12-13.json)
{% endswagger %}
