---
description: Learn how to place a hold on one or more inventory items.
---

# Reserving inventory items

In [Digital River coordinated fulfillments](./), you can use the [Reservations API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Reservations) to place a hold on products. Once you [submit a reservation request](reserving-inventory-items.md#submitting-a-reservation-request), we dynamically select the optimal warehouses to ship the items from. We do this by looking at the ship to country you provide and the product's availability

Once the [reservation](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Reservations) is successfully created, you'll need to use its [unique identifier](reserving-inventory-items.md#unique-identifier) to [release the hold on the products](reserving-inventory-items.md#releasing-a-reservation).

## Submitting a reservation request

A call to the [Reservations API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Reservations) typically occurs late in the [checkout process](../creating-checkouts/), after customers have finalized their carts and selected a [shipping quote](using-shipping-quotes.md#shipping-quotes). So, when defining a [`POST/reservations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createReservations), you can retrieve data from the [checkout](reserving-inventory-items.md#submitting-a-reservation-request).

In the request, you're required to send [product](reserving-inventory-items.md#product-data) and [shipping](reserving-inventory-items.md#shipping-data) data. We also recommend you specify a [unique identifier](reserving-inventory-items.md#unique-identifier) that matches the [checkout's identifier](../creating-checkouts/#checkout-identifier). In addition, your request can set an [expiration period](reserving-inventory-items.md#expiration-period).

### Unique identifier

When submitting a `POST/reservations` request, you should designate a unique `id`. We recommend you retrieve the [checkout's identifier](../creating-checkouts/#checkout-identifier) and use that value to set the reservation's `id`.

| `Checkout` |       | `POST/reservations` |
| ---------- | ----- | ------------------- |
| `id`       | **➔** | `id`                |

This is so that later in the process when you [create a fulfillment order](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentOrders), you can retrieve `checkoutId` from the [upstream order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and use this value to set [`reservationId`](global-fulfillments.md#attaching-a-reservation).

{% hint style="warning" %}
In [Digital River coordinated fulfillments](./), you only need to [attach a reservation identifier](global-fulfillments.md#attaching-a-reservation) to a [create fulfillment order request](global-fulfillments.md#creating-a-fulfillment-order) when you're using the [distributed model](./#distributed-model). In the[ orchestrated model](../../../order-management/fulfillments.md#automated-fulfillment-model), we handle releasing a reservation's hold on products.
{% endhint %}

### Product data

In your `POST/reservations` request, you must pass an array of `items`. These are the [inventory items](../../../product-management/skus.md#inventory-items) you want to place a hold on. Each element in this array needs to specify an `inventoryItemId` and the `quantity` of the item you'd like to reserve.

{% hint style="warning" %}
In [Digital River coordinated fulfillments](./), SKUs and inventory items form [synchronous pairs](../../../product-management/common-attributes.md). So the checkout's `skuId` can be used to set the reservation's `inventoryItemId`.
{% endhint %}

| `Checkout`         |       | `POST/reservations`       |
| ------------------ | ----- | ------------------------- |
| `items[].skuId`    | **➔** | `items[].inventoryItemId` |
| `items[].quantity` | **➔** | `items[].quantity`        |

### Shipping data

To make a reservation, Digital River needs both the customer's [ship to address](reserving-inventory-items.md#ship-to-address) and [shipping choice](reserving-inventory-items.md#shipping-choice). This allows us to determine which warehouses, if any, can ship the product to the customer's country using the desired shipping method.

#### Ship to address

The `shipTo.address` represents a customer's shipping address. You're only required to provide the ship to `country`. When defining the request, you should retrieve the [checkout's ship to values](../creating-checkouts/providing-address-information.md#ship-to-address) and use them to set the reservation's corresponding attributes.

| `Checkout`                  |       | `POST/reservations`         |
| --------------------------- | ----- | --------------------------- |
| `shipTo.address.city`       | **➔** | `shipTo.address.city`       |
| `shipTo.address.postalCode` | **➔** | `shipTo.address.postalCode` |
| `shipTo.address.state`      | **➔** | `shipTo.address.state`      |
| `shipTo.address.country`    | **➔** | `shipTo.address.country`    |

#### Shipping choice

To set a [reservation's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Reservations) `shippingChoice`, retrieve the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`shippingChoice`](../creating-checkouts/shipping-choice.md), and then pass the values in a `POST/reservations`.

{% hint style="info" %}
The checkout's `shippingChoice` is set by using a customer's selected [shipping quote](using-shipping-quotes.md).
{% endhint %}

| `Shipping Quote` |       | `Checkout`                    |       | `POST/reservations`           |
| ---------------- | ----- | ----------------------------- | ----- | ----------------------------- |
|                  |       | `currency`                    | **➔** | `shippingChoice.currency`     |
| `quotes[].total` | **➔** | `shippingChoice.amount`       | **➔** | `shippingChoice.amount`       |
| `quotes[].id`    | **➔** | `shippingChoice.serviceLevel` | **➔** | `shippingChoice.serviceLevel` |

### Expiration period

When making a reservation request, you can tell us when you want the hold to expire. The `expiresInSeconds` value that you provide must be a positive integer.

Once you successfully submit a [`POST/reservations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createReservations), the clock starts ticking. If the hold expires before a [fulfillment order](global-fulfillments.md#a-fulfillment-order) containing the [attached reservation identifier](global-fulfillments.md#attaching-a-reservation) is created, then the reservation expires, and we delete it. At that point, the inventory is [released back into circulation](reserving-inventory-items.md#releasing-a-reservation).

{% tabs %}
{% tab title="POST/reservations " %}
```
curl --location --request POST 'http://api.digitalriver.com/reservations' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
...
--data-raw '{
    "id": "5744204322",
    "items": [
        {
            "inventoryItemId": "9b32defe-76ff-4c95-abb8-7dd607af92d5",
            "quantity": 1,
            "allowOversell": false
        }
    ],
    "shipTo": {
        "address": {
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
    },
    "shippingChoice": {
        "currency": "USD",
        "amount": 5.95,
        "serviceLevel": "SG"
    },
    "expiresInSeconds": 300
}'
```
{% endtab %}
{% endtabs %}

## Releasing a reservation

When you submit a [`POST/reservations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createReservations) request, a `201 Created` response contains a reservation with a unique identifier.

{% hint style="warning" %}
In [Digital River coordinated fulfillments](./) that use the [distributed model](./#distributed-model), the [create reservation request](reserving-inventory-items.md#submitting-a-reservation-request) should be configured so that its [unique identifier](reserving-inventory-items.md#unique-identifier) is the same as the [checkout's identifier](../creating-checkouts/#checkout-identifier).
{% endhint %}

You should persist this identifier. When you [create a fulfillment order](global-fulfillments.md#creating-a-fulfillment-order), make sure you [attach the reservation identifier](global-fulfillments.md#attaching-a-reservation) to the request. Alternatively, you can use the identifier to [cancel the reservation](reserving-inventory-items.md#cancelling-a-reservation).

If you don't perform one of these operations, then the products in the reservation won't be available until the [hold expires](reserving-inventory-items.md#expiration-period). This prevents us from maintaining an accurate, up-to-date accounting of your inventory.

{% tabs %}
{% tab title="Reservation" %}
```javascript
{
    "id": "5678901234",
    "createdTime": "2018-04-25T20:36:00Z",
    "shipTo": {
        "address": {
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
      }
    },
    "shippingChoice": {
        "currency": "USD",
        "amount": 5.95,
        "serviceLevel": "SG"
    },
    "items": [
      {
        "inventoryItemId": "9234276173",
        "quantity": 1,
        "allowOversell": false
      }
    ],
    "expiresInSeconds": 300,
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

### Attaching a reservation to a fulfillment order

In [Digital River coordinated fulfillments](./) that use the [distributed model](./#distributed-model), you can release a reservation by[ attaching its unique identifier](global-fulfillments.md#attaching-a-reservation) to a [`POST/fulfillment-orders`](global-fulfillments.md#creating-a-fulfillment-order) request. This operation passes the reservation's shipping, product, and expiration date to our fulfillment services who reduce the product's inventory levels and close the reservation.

{% hint style="warning" %}
In [Digital River coordinated fulfillments](./) that use the [orchestrated model](./#orchestrated-model), we send an internal request that creates a [fulfillment order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) and releases a reservation's hold on inventory.
{% endhint %}

If you [properly configure a reservation identifier](reserving-inventory-items.md#unique-identifier), it should match the [checkout's identifier](../creating-checkouts/#checkout-identifier). So, when you [synchronously](../../../order-management/creating-and-updating-an-order.md#accepted) or [asynchronously](../../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event) receive an [order](reserving-inventory-items.md#submitting-a-reservation-request) in an `accepted` state, you can retrieve `checkoutId` and use that value to set `reservationId` in a `POST/fulfillment-orders`.

| `Order` in an `accepted` state |       | `POST/fulfillment-orders` |
| ------------------------------ | ----- | ------------------------- |
| `checkoutId`                   | **➔** | `reservationId`           |

### Cancelling a reservation

Cancelling a [reservation](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Reservations) allows us to release the hold and make the products available for inclusion in other [fulfillment orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders).

To cancel a reservation, send its unique identifier in a [`DELETE/reservations/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/deleteReservations) request. This removes the hold on _all_ the inventory items in that reservation. You can't remove a hold on specific items within a reservation.

If you're using either the [distributed](./#distributed-model) or [orchestrated](./#orchestrated-model) fulfillment model, and you [create a reservation](reserving-inventory-items.md#submitting-a-reservation-request) during the checkout process but don't [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), then make sure you delete the reservation.

You should also delete a reservation if you're using the [distributed model](./#distributed-model) and you convert the checkout to an order but, for whatever reason, fail to [attach the reservation to the fulfillment order](reserving-inventory-items.md#attaching-a-reservation-to-a-fulfillment-order).

## Handling failed reservations

When you submit a `POST/reservations`, if any [inventory item](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) in the request has an [`allowOversell` ](../../../product-management/common-attributes.md#allow-oversell)value that is set to `false`, and [inventory levels](checking-inventory-levels.md) for that item are insufficient, the entire hold request will fail. In this case, none of the products in the request will be reserved.

You can remedy this in one of two ways. For the items whose inventory levels are insufficient, you could either set their `allowOversell` values to `true` or remove those products from the request.
