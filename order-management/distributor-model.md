---
description: >-
  Gain a better understanding of how to implement fulfillments with the
  distributor model
---

# Distributor model

To fulfill your [physical goods](../product-management/skus.md#how-products-are-classified-as-physical-or-digital), Digital River provides you the option of setting up a direct integration with one or more distributors, each of whom has purchased and stored your inventory. In this model, you and the distributor are responsible for handling inventory synchronization as well as managing the cost of goods.

Before deploying, you’ll need to provide us with some basic information about each of your distributors—such as their unique identifier, name and address, and whether to remit shipping costs to them—so that we can properly configure them in our accounting systems.

<figure><img src="../.gitbook/assets/Distribution model seq diagram.png" alt=""><figcaption></figcaption></figure>

After customers place an order, a [payment charge](../developer-resources/digital-river-api-reference/payment-charges.md#how-a-charge-is-created) is authorized and a line item ships, your commerce platform needs to send the agreed upon identifier of the distributor, their up-to-date costs of goods, shipping costs (if applicable), and preferred payout currency in a [`POST /fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments/operation/createFulfillments) request (which triggers a [charge capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) attempt).

{% hint style="success" %}
If a fulfillment involves multiple line items and different distributors are assigned to each, then your request can pass their data in separate `items[]`.&#x20;
{% endhint %}

```
curl --location 'https://api.digitalriver.com/fulfillments' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your secret API token>' \
--data '{
    "orderId": "308604120336",
    "currency": "EUR",
    "items": [
        {
            "itemId": "243441700336",
            "quantity": "1",
            "subfulfillerId": "1234",
            "distributorCost": 400,
            "shippingCost": 10
        }
    ]
}'
```

Digital River stores this data so that it can be used in the reconciliation process when the distributor submits an invoice for shipping and/or product costs.
