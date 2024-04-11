---
description: >-
  Learn how to set the price and aggregate price of items in a Checkout or
  Invoice.
---

# Setting the price of an item

When [describing items](./) in a Checkout or Invoice, in addition to the required `skuId`parameter, you'll also need to define the [price](price-of-an-item.md#defining-a-price) or [aggregate price](price-of-an-item.md#defining-an-aggregate-price).

## Defining a price

In a `POST` Checkout or Invoice request, the `price` parameter represents the price of a single line item.

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    "customerId": 520984250336,
    ...
    "items": [
        {
            "skuId": "77817db3-5b74-443e-86fc-b04ee6637f29",
            "price": 100.00,
            "quantity": 2
        },
        {
            "skuId": "e446860d-86a6-4e22-ba38-bbaa2c17de55",
            "price": 50.00,
            "quantity": 3
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

For each line item in the response, the `amount` returned is derived by multiplying the`price` and `quantity` supplied in the request.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "180144300336",
    ...
    "items": [
        {
            "skuId": "77817db3-5b74-443e-86fc-b04ee6637f29",
            "amount": 200.0,
            "quantity": 2,
            ...
        },
        {
            "skuId": "e446860d-86a6-4e22-ba38-bbaa2c17de55",
            "amount": 150.0,
            "quantity": 3,
            ...
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

## Defining an aggregate price

In a `POST` Checkout or Invoice request, the `aggregatePrice` parameter represents the total price of one or more items, regardless of the `quantity` you specify.

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    "customerId": 520984250336,
    ...
    "items": [
        {
            "skuId": "77817db3-5b74-443e-86fc-b04ee6637f29",
            "aggregatePrice": 100.00,
            "quantity": 2
        },
        {
            "skuId": "e446860d-86a6-4e22-ba38-bbaa2c17de55",
            "aggregatePrice": 50.00,
            "quantity": 3
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

For each line item in the response, the `amount` returned is equal to the `aggregatePrice` you supplied in the request.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "180144320336",
    ...
    "items": [
        {
            "skuId": "77817db3-5b74-443e-86fc-b04ee6637f29",
            "amount": 100.0,
            "quantity": 2,
            ...
        },
        {
            "skuId": "e446860d-86a6-4e22-ba38-bbaa2c17de55",
            "amount": 50.0,
            "quantity": 3,
            ...
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

### Use cases

To better illustrate the aggregate price concept, the following examples provide use cases where the `aggregatePrice` parameter could be applied.

#### Example one

Let's say your website offers a price break when customers buy three or more laptop computers. This entices a shopper to purchase three laptops in one order. The customer is given a discounted price of $2,000 for the total order. That discounted price represents the `aggregatePrice`. The individual unit prices are now based on that `aggregatePrice`. So the effective price of each individual laptop is adjusted to approximately $667.67.

#### Example two

The `aggregatePrice` attribute can also be useful in buy one, get one (BOGO) free scenarios. You operate a grocery delivery service and your website has a BOGO offer on cases of soda. A customer purchases two cases and the offer is applied. The `aggregatePrice` is the cost of the first case of soda divided by two.
