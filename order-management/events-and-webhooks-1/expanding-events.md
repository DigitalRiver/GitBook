---
description: >-
  Gain a better understanding of the events that are available for expansion,
  the extra data they contain, and how to subscribe to them
---

# Expanding events

Your account can be configured so that Digital River expands the [`data.object`](events-1/#event-data) of certain [event types](events-1/#event-types) before pushing them to a [webhook's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Webhooks) designated `address`. Currently, four expandable events exist: [`order.accepted`](events-1/event-types.md#order.accepted), [`order.cancelled`](events-1/event-types.md#order.cancelled), [`order.refunded`](events-1/event-types.md#order.refunded), and [`fulfillment.created`](events-1/event-types.md#fulfillment.created).

Relative to their default version, `items[].productDetails` in these enhanced events contains (1) `physical` , a boolean which indicates whether Digital River classified that product as [physical or digital](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), and (2) `metadata`, assuming you defined this parameter in the [SKU](../../product-management/creating-and-updating-skus.md) or [`productDetails`](../../product-management/using-product-details.md).

{% hint style="info" %}
You can also access these additional key-value pairs by making a [get order request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders/operation/retrieveOrders) with the `expand` query parameter set to `true`.
{% endhint %}

{% tabs %}
{% tab title="order.accepted" %}
```json
{
    "id": "e2ab8696-53fc-4ac9-9f5f-f38eb61fbf05",
    "type": "order.accepted",
    "data": {
        "object": {
            "id": "295759800336",
            ...
            "items": [
                {
                    "id": "229219830336",
                    ...
                    "productDetails": {
                        "id": "sku_8128ce28-d4a8-475b-9fce-6e78c38da88b",
                        ...
                        "physical": true,
                        "metadata": {
                            "more": "data",
                            "evenMore": "data"
                        },
                        ...
                    },
                    ...
                }
            ],
            ...
        }
    },
    ...
}
```


{% endtab %}

{% tab title="fulfillment.created" %}
```json
{
    "id": "45570b11-95e6-41bb-be20-f46f6dc6194b",
    "type": "fulfillment.created",
    "data": {
        "object": {
            "id": "ful_17323b58-96c4-4239-a0ed-be93c15faae0",
            ...
            "orderDetails": {
                ...
                "items": [
                    {
                        "id": "229219830336",
                        ...
                        "productDetails": {
                            "id": "sku_8128ce28-d4a8-475b-9fce-6e78c38da88b",
                            ...
                            "physical": true,
                            "metadata": {
                                "more": "data",
                                "evenMore": "data"
                            },
                            ...
                        },
                        ...
                    }
                ],
                ...
            }
        }
    },
    ...
}
```
{% endtab %}
{% endtabs %}

If you think your application could use this extra data to, for example, populate [customer notifications](../customer-notifications.md) or determine whether the product is physical and its details need to be sent to your logistics provider, you'll first need to ask your Digital River representative to turn the feature on. Once that's done, for each of the supported event types, you'll be able to choose between its standard or expanded version when [configuring a webhook in Digital River Dashboard](../../administration/dashboard/developers/webhooks/).

<figure><img src="../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>
