---
description: Learn how to access regulatory fee information.
---

# Accessing regulatory fee information

When [regulatory fees are applied to products](../../../product-management/regulatory-fees/managing-regulatory-fees.md) in a transaction, you can access both [aggregated](accessing-regulatory-fee-information.md#determining-the-aggregated-fee-amount) and [product-level](accessing-regulatory-fee-information.md#getting-information-on-specific-fees) information on these fees. This allows you to provide customers transparency into the transaction's fee types, their costs, and which products the fees apply to.

## Getting the aggregated fee amounts <a href="#determining-the-aggregated-fee-amount" id="determining-the-aggregated-fee-amount"></a>

For transactions that have one or more assessed [regulatory fees](../../../product-management/regulatory-fees/), you can find their aggregated amount in the `totalFees` attribute. This attribute is contained in the [Checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), [Order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), and [Invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) resources. The `totalFees` value does _not_ include taxes assessed on a transaction's regulatory fees. Instead, fee taxes are rolled up into the `totalTax` value.

{% tabs %}
{% tab title="Checkout" %}
```javascript
{
    "id": "4f434b0f-b3b6-4698-8754-becb034f1abd",
    ...
    "totalAmount": 44.09,
    "subtotal": 41.0,
    "totalFees": 16.0,
    "totalTax": 3.09,
    ...
    "items": [
        {
            "id": "f8c25de3-ddba-4a41-9946-3db9801bb04f",
            ...
            "amount": 20.0,
            "quantity": 2,
            ...
            "fees": {
                ...
                "amount": 16.0,
                "taxAmount": 1.2
            }
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

For each line item with applied regulatory fees, we return `fees.amount`. This represents the amount of fees applied to the total `quantity` of that particular line item. For example, if the line item consists of two mobile phones, `fees.amount` is the aggregated fee amount applied to both devices. The `fees.taxAmount` represents taxes assessed on these line item fees.

## Getting information on specific fees

If you [associate regulatory fees with a SKU](../../../product-management/regulatory-fees/managing-regulatory-fees.md#sku-identifier), and then [add that SKU to a checkout](describing-the-items/), we return information on each applied fee. In [Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), [Invoices](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices), and [Orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), this information is contained within `items[].fees.details[]`.

The data in this array is useful when multiple regulatory fees are associated with a SKU. Each element in the array provides a fee's unique `id`, the [fee `type`](../../../product-management/regulatory-fees/managing-regulatory-fees.md#type), the `perUnitAmount`, and the `amount`. The following table shows how some of these attributes are mapped within the [Fee](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fees), Checkout, and Order resources.

| `Fee`    |       | `Checkout`                             |       | `Order`                                |
| -------- | ----- | -------------------------------------- | ----- | -------------------------------------- |
| `id`     | **➔** | `items[].fees.details[].id`            | **➔** | `items[].fees.details[].id`            |
| `type`   | **➔** | `items[].fees.details[].type`          | **➔** | `items[].fees.details[].type`          |
| `amount` | **➔** | `items[].fees.details[].perUnitAmount` | **➔** | `items[].fees.details[].perUnitAmount` |

The same relationship exists between Fees and Invoices:

| `Fee`    |       | `Invoice`                              |
| -------- | ----- | -------------------------------------- |
| `id`     | **➔** | `items[].fees.details[].id`            |
| `type`   | **➔** | `items[].fees.details[].type`          |
| `amount` | **➔** | `items[].fees.details[].perUnitAmount` |

The `details[].amount` is determined by multiplying `details[].perUnitAmount` by the `quantity` of that line item.

In the following example, a physical SKU is created and then associated with two separate regulatory fees. The first is a [battery type fee](../../../product-management/regulatory-fees/managing-regulatory-fees.md#battery) with an `amount` of `5.0`. The second is a [WEEE type fee](../../../product-management/regulatory-fees/managing-regulatory-fees.md#weee) with an `amount` of `3.0`.

The SKU is then attached to a checkout. Since there are now two regulatory fees associated with this checkout's sole line item, `details[]` contains two elements. Each element maps to one of the applied regulatory fees. When the [checkout is converted to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), the returned fees data remains the same.

You can use this information to provide customers detailed regulatory fee information. In the example below, you could inform customers that both a [battery](../../../product-management/regulatory-fees/managing-regulatory-fees.md#battery) and [WEEE](../../../product-management/regulatory-fees/managing-regulatory-fees.md#weee) regulatory fee are applied to the product and provide a cost-breakdown for each.

{% tabs %}
{% tab title="SKU " %}
```javascript
{
    "id": "8639a055-ce57-4e1d-afdd-bf83769c3d21",
    "createdTime": "2021-04-08T15:36:04Z",
    ...
    "physical": true
}
```
{% endtab %}

{% tab title="Battery Fee associated w/ SKU" %}
```javascript
{
    "id": "fee_09eefe18-3352-45b8-b1b7-8f15cad3be5b",
    "skuId": "8639a055-ce57-4e1d-afdd-bf83769c3d21",
    ...
    "amount": 5.0,
    ...
    "createdTime": "2021-04-08T15:38:20Z",
    ...
    "type": "battery"
}
```
{% endtab %}

{% tab title="WEEE Fee associated w/ SKU" %}
```javascript
{
    "id": "fee_76828e24-67ed-46e3-9741-362b9e5e3aed",
    "skuId": "8639a055-ce57-4e1d-afdd-bf83769c3d21",
    ...
    "amount": 3.0,
    ...
    "createdTime": "2021-04-08T15:38:33Z",
    ...
    "type": "weee"
}
```
{% endtab %}

{% tab title="Checkout w/attached SKU" %}
```javascript
{
    "id": "4f434b0f-b3b6-4698-8754-becb034f1abd",
    "createdTime": "2021-04-08T15:39:22Z",
    ...
    "totalAmount": 44.09,
    ...
    "totalFees": 16.0,
    ...
    "items": [
        {
            "id": "f8c25de3-ddba-4a41-9946-3db9801bb04f",
            "skuId": "8639a055-ce57-4e1d-afdd-bf83769c3d21",
            "amount": 20.0,
            "quantity": 2,
            ...
            "fees": {
                "details": [
                    {
                        "type": "weee",
                        "perUnitAmount": 3.0,
                        "amount": 6.0,
                        "id": "fee_76828e24-67ed-46e3-9741-362b9e5e3aed"
                    },
                    {
                        "type": "battery",
                        "perUnitAmount": 5.0,
                        "amount": 10.0,
                        "id": "fee_09eefe18-3352-45b8-b1b7-8f15cad3be5b"
                    }
                ],
                "amount": 16.0,
                "taxAmount": 1.2
            }
        }
    ],
    ...
}
```
{% endtab %}

{% tab title="Order" %}
```javascript
{
    "id": "187279700336",
    "createdTime": "2021-04-08T15:40:32Z",
    ...
    "totalAmount": 44.09,
    ...
    "totalFees": 16.0,
    ...
    "items": [
        {
            "id": "108649890336",
            "skuId": "8639a055-ce57-4e1d-afdd-bf83769c3d21",
            "amount": 20.0,
            "quantity": 2,
            ...
            "fees": {
                "details": [
                    {
                        "type": "weee",
                        "perUnitAmount": 3.0,
                        "amount": 6.0,
                        "id": "fee_76828e24-67ed-46e3-9741-362b9e5e3aed"
                    },
                    {
                        "type": "battery",
                        "perUnitAmount": 5.0,
                        "amount": 10.0,
                        "id": "fee_09eefe18-3352-45b8-b1b7-8f15cad3be5b"
                    }
                ],
                "amount": 16.0,
                "taxAmount": 1.2
            }
        }
    ],
    ...
    "checkoutId": "4f434b0f-b3b6-4698-8754-becb034f1abd"
}
```
{% endtab %}
{% endtabs %}
