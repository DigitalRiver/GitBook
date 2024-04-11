---
description: >-
  In Digital River coordinated fulfillments, learn how to use the Fulfillment
  Orders API and Shipments API to manage fulfillment of physical products
---

# Managing a fulfillment order

A [fulfillment order](global-fulfillments.md#a-fulfillment-order) manages the fulfillment of a transaction's [SKU-inventory item pairs](../../../product-management/common-attributes.md). You only use this resource in [Digital River coordinated fulfillments](./).

If you're using the [distributed model](./#distributed-model), you must send a [create fulfillment order request](global-fulfillments.md#creating-a-fulfillment-order) to initiate physical fulfillment.

If you're using the [orchestrated model](./#orchestrated-model), Digital River submits this fulfillment order request for you.

In both the distributed and orchestrated models, you should subscribe to [events that occur during a fulfillment order's lifecycle](global-fulfillments.md#listening-and-responding-to-fulfillment-order-events). These events notify you of (1) [pending shipments](global-fulfillments.md#pending-events), (2)[ backordered products](global-fulfillments.md#backordered-events), (3) [shipped products](global-fulfillments.md#shipped-events) and (4) [product cancellations](global-fulfillments.md#cancelled-events).

You can also use [shipments](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments) to [track the progress of a delivery.](global-fulfillments.md#tracking-a-shipment)

## Creating a fulfillment order

In the [distributed model](./#distributed-model)**,** once you either [synchronously](../../../order-management/creating-and-updating-an-order.md#accepted) or [asynchronously](../../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event) receive an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in an [`accepted`](../../../order-management/creating-and-updating-an-order.md#handling-accepted-orders) state, your integration should [handle the order state change event](../../../order-management/creating-and-updating-an-order.md#handling-accepted-orders) by sending a create fulfillment order request. This [`POST/fulfillment-orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentOrders) request initiates the fulfillment of a transaction's [SKU-inventory item pairs](../../../product-management/common-attributes.md).

{% hint style="success" %}
In the [orchestrated model](./#orchestrated-model), we listen for an [`accepted`](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) order and handle this state change event by internally submitting a create fulfillment order request.
{% endhint %}

The following describes the request's required data and optional data:

{% hint style="info" %}
For a full list of specifications, refer to the [Fulfillment Orders APIs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) reference documentation.
{% endhint %}

#### Required data

Every `POST/fulfillment-orders` request must include [currency](global-fulfillments.md#currency), [created time](global-fulfillments.md#upstream-order-time), [shipping address](global-fulfillments.md#ship-to-address), [shipping method](global-fulfillments.md#shipping-choices), and [product](global-fulfillments.md#product-information) data.

This required data can be retrieved from an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in an [`accepted`](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) state:

| Order in an `accepted` state  |       | `POST/fulfillment-orders` |
| ----------------------------- | ----- | ------------------------- |
| `currency`                    | **➔** | `currency`                |
| `createdTime`                 | **➔** | `upstreamOrderTime`       |
| `shipTo.country`              | **➔** | `shipTo.country`          |
| `shippingChoice.serviceLevel` | **➔** | `shippingChoice.id`       |
| `items[].skuId`               | **➔** | `items[].inventoryItemId` |
| `items[].quantity`            | **➔** | `items[].quantity`        |
| `items[].tax.amount`          | **➔** | `items[].tax.amount`      |

#### Optional data

In addition to other optional data, a `POST/fulfillment-orders` request accepts [product](global-fulfillments.md#product-information), [customer](global-fulfillments.md#customer-information), [ship to](global-fulfillments.md#ship-to-address), upstream order identifier, and locale data. If you placed a hold on products, you should also [attach the reservation identifier](global-fulfillments.md#attaching-a-reservation).

This optional data can be retrieved from an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in an [`accepted`](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) state:

| `items[].id`                    | **➔** | `items[].upstreamId`      |
| ------------------------------- | :---: | ------------------------- |
| `items[].amount`                | **➔** | `items[].total`           |
| `shipTo.name`or `billTo.name`   | **➔** | `name` or `shipTo.name`   |
| `shipTo.phone`or `billTo.phone` | **➔** | `phone` or `shipTo.phone` |
| `shipTo.email`or `billTo.email` | **➔** | `email` or `shipTo.email` |
| `shipTo`                        | **➔** | `shipTo`                  |
| `id`                            | **➔** | `upstreamId`              |
| `locale`                        | **➔** | `locale`                  |
| `checkoutId`                    | **➔** | `reservationId`           |

### Currency

The `currency` in the request should be the same as the value in the upstream [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). This avoids creating downstream invoicing errors, issues with customs, and incorrect tax computations.

### Upstream order time

As with all [dates and times in the Digital River APIs](../../../developer-resources/best-practices.md#dates-and-times), the `createdTime` of the upstream [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is in [UTC](https://www.timeanddate.com/time/aboututc.html) and adheres to the [ISO-8601](https://en.wikipedia.org/wiki/ISO\_8601) standard. You should not modify this date-time value before using it to set `upstreamOrderTime` in a [fulfillment order](global-fulfillments.md#creating-a-fulfillment-order).

```javascript
{
    "id": "186962110336",
    "createdTime": "2021-04-02T18:46:45Z",
    ...
}
```

### Customer information

You can set the customer's `name`, `email`, and `phone` at the fulfillment order level and within `shipTo`.

### Ship to address

The [fulfillment order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) `shipTo` values should be the same as the upstream [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`shipTo`](../creating-checkouts/providing-address-information.md#ship-to-address).

### Attaching a reservation

The [fulfillment order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) `reservationId` should reference the [reservation](reserving-inventory-items.md) that was used to place a hold on the products.

{% hint style="info" %}
When [creating a reservation](reserving-inventory-items.md#submitting-a-reservation-request), you should [set the reservation's identifier](reserving-inventory-items.md#unique-identifier) value to be same as the [checkout's identifier](../creating-checkouts/#checkout-identifier).
{% endhint %}

If the create fulfillment order request doesn't contain a `reservationId`, Digital River still attempts to allocate the specified inventory items. If we determine inventory levels are too low, what happens at that point depends on whether you [allow overselling of an item](../../../product-management/common-attributes.md#allow-oversell) and whether your channel is set up to accept backorders.

### Shipping choices

When setting the [fulfillment order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) `shippingChoice.id`, you should use the [order's](global-fulfillments.md#creating-a-fulfillment-order) [`shippingChoice.serviceLevel`](../creating-checkouts/shipping-choice.md#shipping-method) . This value maps to the [identifier of the shipping quote](using-shipping-quotes.md#unique-identifier-and-service-levels) selected by the customer.

| Shipping quote |       | Order                         |       | Fulfillment Order   |
| -------------- | ----- | ----------------------------- | ----- | ------------------- |
| `id`           | **➔** | `shippingChoice.serviceLevel` | **➔** | `shippingChoice.id` |

If you want to set the [fulfillment order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) `signatureRequiredType`, you'll need to persist the [shipping quote](using-shipping-quotes.md#shipping-quotes) selected by the customer. You can then retrieve the [shipping quote's `signatureRequiredType`](using-shipping-quotes.md#signature-requirements) and use that value to set the fulfillment order's `signatureRequiredType`.

If the upstream [order](global-fulfillments.md#creating-a-fulfillment-order) triggers the [landed cost feature](../creating-checkouts/landed-costs.md#how-landed-cost-is-represented), then set the fulfillment order's `dutiesPaid` to `true`. This notifies the shipping carrier that the customer has already paid the full landed cost and they should invoice you for any duties paid.

### Product information

Use the [fulfillment order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) `items` array to specify product information. The [line items](../../../order-management/creating-and-updating-an-order.md#line-items) must be retrieved from the upstream [order](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveOrders). The same is true for most of a fulfillment order's optional product data.

For example, you can use `giftMessage` to send the downstream fulfiller a message that customers want included with the package. The `giftWrap` flag allows you to indicate whether the product should be wrapped.

## A fulfillment order

Once you successfully submit a `POST/fulfillment-orders` request, a [fulfillment order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) contains [unique identifiers](global-fulfillments.md#unique-identifiers) that are needed for downstream processing. Additionally, we return attributes that inform you of a [fulfillment order's state](global-fulfillments.md#the-fulfillment-order-life-cycle) and [categorize the status of its line items](global-fulfillments.md#product-status-by-category).

### Unique identifiers

Once a [fulfillment order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) is created, we assign it a unique identifier. We also assign unique identifiers to each of [its line items](global-fulfillments.md#product-information). You should persist all of these values.

You'll need the fulfillment order identifier to [retrieve the object](global-fulfillments.md#retrieving-a-fulfillment-order).

When submitting [product cancellation requests](instructing-digital-to-cancel-items.md) and [product return requests](../../../order-management/returns-and-refunds-1/returns/digital-river-coordinated-returns.md), you must provide both the fulfillment order identifier and the relevant line item identifiers.

In the [distributed model](./#distributed-model), you can retrieve these identifiers from the `201 Created` response to a [`POST/fulfillment-orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentOrders) request.

In the [orchestrated model](./#orchestrated-model), you can retrieve these identifiers by listening for the [`fulfillment_order.pending` ](global-fulfillments.md#pending-events)event.

### The fulfillment order life cycle

You should be aware of both the [fulfillment order's lifecycle](global-fulfillments.md#fulfillment-order-level) and the[ fulfillment order's line item's lifecycle](global-fulfillments.md#line-item-level). In both, each stage of the lifecycle is represented by a `state`.

#### Fulfillment order level

The `state` attribute at the fulfillment order level indicates where a [fulfillment order](global-fulfillments.md#a-fulfillment-order) is in its lifecycle. The values for a successful fulfillment (i.e., the happy path) are `pending` > `shipped`.

| (1) When the fulfillment order...                         | (2) its `state` transitions to... |
| --------------------------------------------------------- | --------------------------------- |
| is created but not yet partially or fully shipped         | `pending`                         |
| partially or fully ships                                  | `shipped`                         |
| is cancelled by the customer, the client or the fulfiller | `cancelled`                       |

#### Line item level

The line item `state` attribute indicates where a [fulfillment order](global-fulfillments.md#a-fulfillment-order)'s line item is in its lifecycle. The values for a successfully fulfilled line item (i.e., the happy path) are `pending` > `shipped`.

| (1) When the line item...                                                                                                      | (2) its `state` transitions to... |
| ------------------------------------------------------------------------------------------------------------------------------ | --------------------------------- |
| has not yet partially or fully shipped                                                                                         | `pending`                         |
| is configured to [allow oversell](../../../product-management/managing-inventory.md#allow-oversell) and is awaiting restocking | `backordered`                     |
| partially or fully ships                                                                                                       | `shipped`                         |
| is cancelled by the customer, the client or the fulfiller                                                                      | `cancelled`                       |

### Product status by category

Each element of [fulfillment order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) `items` array indicates how many items are `pending`, `backordered`, `shipped`, `cancelled`, and `returned`. In aggregate, these values equal the total `quantity` of that line item, which represents the amount originally purchased by the customer.

## Monitoring and responding to a fulfillment order

You can determine a [fulfillment order's](global-fulfillments.md#creating-a-fulfillment-order) [`state`](global-fulfillments.md#the-fulfillment-order-life-cycle) by either [calling the API](global-fulfillments.md#retrieving-a-fulfillment-order) or [listening for webhook events](global-fulfillments.md#listening-and-responding-to-fulfillment-order-events).

### Retrieving a fulfillment order

There are two methods in the [Fulfillment Orders API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) that can be used to retrieve fulfillment orders. You can either [get a list of fulfillment orders](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listFulfillmentOrders) filtered by optional query parameters. Or you can [get an individual fulfillment order](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveFulfillmentOrders) by including its unique identifier as a path parameter in the request.

### Listening and responding to fulfillment order events

We recommend you respond to a [fulfillment order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) [`state`](global-fulfillments.md#the-fulfillment-order-life-cycle) changes by listening for the [pending](global-fulfillments.md#pending-events), [backordered](global-fulfillments.md#backordered-events), [shipped](global-fulfillments.md#shipped-events), and [cancelled](global-fulfillments.md#cancelled-events) events.

In all of these events, `data.object` contains the unique identifier of:

* The[ fulfillment order and each of its line items](global-fulfillments.md#unique-identifiers)
* The [upstream order](../../../order-management/creating-and-updating-an-order.md#unique-identifier) and each of [its line items](../../../order-management/creating-and-updating-an-order.md#line-items)
* Each line item's [SKU-inventory item pair](../../../product-management/common-attributes.md#unique-identifier).

#### Fulfillment order pending events <a href="#pending-events" id="pending-events"></a>

When Digital River queues a fulfillment order for creation, we create a `fulfillment_order.pending` event. The event's `data.object` is a [fulfillment order](global-fulfillments.md#a-fulfillment-order) in a [`pending`](global-fulfillments.md#the-fulfillment-order-life-cycle) state.

In the [orchestrated model](./#orchestrated-model), use this event to retrieve and save the fulfillment order's identifier as well as each of its line item's identifiers.

{% hint style="info" %}
A [`pending`](global-fulfillments.md#the-fulfillment-order-life-cycle) fulfillment order doesn't necessarily mean that all of its line items are also [`pending`](global-fulfillments.md#the-fulfillment-order-life-cycle). A line item can be `pending`, `shipped`, `backordered` or `cancelled` while the fulfillment order is still `pending`.
{% endhint %}

#### Fulfillment order backordered events <a href="#backordered-events" id="backordered-events"></a>

Upon receiving a backordered notification from your channel's designated fulfiller, Digital River sends you a `fulfillment_order.backordered` event. The event's `data.object` contains an array of backordered `items`.

For each product in the `items` array, we provide an estimated `availableTime` (assuming the fulfiller sends us this information). We also specify the original `ordered` quantity as well as the quantity of `backOrdered` items that triggered the event.

The `totalBackordered` is the aggregated `backOrdered` quantity from all the backordered events. When processing duplicate backordered events, you can use this value as a checksum, thereby ensuring your system does not exceed the total `ordered` amount.

You can use the `fulfillment_order.backordered` event as a trigger to send a delayed order notification (typically an email) to the customer. In the email, we recommend that you provide a link that directs customers to their order management page.

On this page, you should provide customers the option to fully or partially cancel the order. If they select either option, make sure you respond to this event by submitting a [create fulfillment cancellation request](instructing-digital-to-cancel-items.md).

{% tabs %}
{% tab title="fulfillment_order.backordered" %}
```javascript
{
    "id": "evt_e381g2ff-7d42-3b05-91d5-e711443r3521",
    ...
    "data": {
        "object": {
            ...
            "items": [
                {
                    ...
                    "ordered": 6,
                    "backordered": 2,
                    "totalBackordered": 3,
                    "availableTime": 2020-11-25T20:36:00Z,
                    ...
                }
            ],
            ...
        },
        "previousAttributes": {}
    },
    ...
    "type": "fulfillment_order.backordered"
}
```
{% endtab %}
{% endtabs %}

#### Fulfillment order shipped events <a href="#shipped-events" id="shipped-events"></a>

Once Digital River receives a shipped notification from your channel's designated fulfiller, we create an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../../order-management/events-and-webhooks-1/events-1/#event-types) of `fulfillment_order.shipped`. Its `data.object` consists of a [shipment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments). To [track a shipment's progress](global-fulfillments.md#tracking-a-shipment), persist `data.object.id`, which represents the shipment's identifier.

In the event's payload, `fulfillmentOrderUpstreamId` represents the [order's](global-fulfillments.md#creating-a-fulfillment-order) `id` and each `items[].fulfillmentOrderItemUpstreamId` maps to an `items[].id` in that [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

{% tabs %}
{% tab title="fulfillment_order.shipped" %}
```javascript
{
    "id": "evt_d290f1ee-6c54-4b01-90e6-d701748f0851",
    ...
    "data": {
        "object": {
            "id": "29016544906",
            ...
            "fulfillmentOrderId": "5774321009",
            "fulfillmentOrderUpstreamId": "9292981838",
            ...
            "items": [
                {
                    "id": "8760948870",
                    "fulfillmentOrderItemId": "650398674428",
                    "fulfillmentOrderItemUpstreamId": "650398674428",
                    ...
                    "quantity": 1,
                    ...
                }
            ],
            ...
        },
        "previousAttributes": {}
    },
    ...
    "type": "fulfillment_order.shipped"
}
```
{% endtab %}
{% endtabs %}

In the [distributed model](./#distributed-model), respond to this event by sending a [`POST /fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments/operation/updateFulfillments), which [captures](../../../developer-resources/digital-river-api-reference/payment-charges.md#captures) the appropriate amount of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) payment[ charges](../../../developer-resources/digital-river-api-reference/payment-charges.md).

The following table lists the data to retrieve from the event and then pass in a `POST /fulfillments`.

| Event                                    |       | `POST /fulfillments`     |
| ---------------------------------------- | ----- | ------------------------ |
| `data.object.id`                         | **➔** | `shipmentId`             |
| `items[].id`                             | **➔** | `items[].shipmentItemId` |
| `fulfillmentOrderUpstreamId`             | **➔** | `orderId`                |
| `items[].fulfillmentOrderItemUpstreamId` | **➔** | `items[].itemId`         |
| `items[].quantity`                       | **➔** | `items[].quantity`       |

#### Fulfillment order cancelled events <a href="#cancelled-events" id="cancelled-events"></a>

Whenever a fulfillment order is fully or partially cancelled, we send you a `fulfillment_order.cancelled` event.

The source of these events are either [`POST/fulfillment-cancellations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentCancellations) requests that your system submits or cancellation notifications sent by the product's fulfiller. The event's `data.object` is a [fulfillment order](global-fulfillments.md#a-fulfillment-order) in a `cancelled` state.

In the event's payload, `upstreamId` represents the [order's](global-fulfillments.md#creating-a-fulfillment-order) [unique identifier](../../../order-management/creating-and-updating-an-order.md#unique-identifier) and `items[].upstreamId` represents a [line item's identifier](../../../order-management/creating-and-updating-an-order.md#line-items) in an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

In the [distributed model](./#distributed-model), _every time_ you receive `fulfillment_order.cancelled`, retrieve data from the event and send it in a [`POST/fulfillments`](../../../order-management/informing-digital-river-of-a-fulfillment.md) request. This request instructs Digital River to [cancel](../../../developer-resources/digital-river-api-reference/payment-charges.md#cancels) the appropriate amount of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) payment[ charges](../../../developer-resources/digital-river-api-reference/payment-charges.md).

{% hint style="success" %}
In the [orchestrated model](./#orchestrated-model), we listen for the cancelled event and respond to it by submitting an internal payment cancel request.
{% endhint %}

The following table lists the data you must retrieve from each `fulfillment_order.cancelled` event and then pass in a `POST/fulfillments`.

| `fulfillment_order.cancelled` event |       | `POST/fulfillments`      |
| ----------------------------------- | ----- | ------------------------ |
| `upstreamId`                        | **➔** | `orderId`                |
| `items[].upstreamId`                | **➔** | `items[].itemId`         |
| `items[].cancelled`                 | **➔** | `items[].cancelQuantity` |

## Tracking a shipment

The products in a [fulfillment order ](global-fulfillments.md#a-fulfillment-order)can be delivered to the end customer in one or more shipments. Each of these shipments is represented by the [Shipment resource](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments).

You can use the unique shipment identifier you receive in a [`fulfillment_order.shipped`](global-fulfillments.md#shipped-events) event to [submit queries](global-fulfillments.md#querying-the-shipments-api) that return a [shipment's contents](global-fulfillments.md#determining-the-contents-of-a-shipment) and provide [tracking information](global-fulfillments.md#monitoring-the-progress-of-a-shipment).

### Querying the Shipments API

There are two methods for querying the [Shipments API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments). You can either retrieve an individual shipment by sending its unique identifier as a path parameter in a [`GET/shipments/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveShipments) request. Or you can submit a [`GET/shipments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listShipments) request to retrieve a list of shipments and use optional query parameters to filter the results.

### Determining the contents of a shipment

A [shipment's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments) `items` array returns each shipment item's unique identifier and the item's shipped `quantity`. All the relevant upstream identifiers of the item are also included.

Additionally, when the shipped item is a smartphone or cellphone, the downstream fulfiller may pass back to you `unitAttributes` that help identify and track the device. These attributes consist of a serial, [IMEI](https://en.wikipedia.org/wiki/International\_Mobile\_Equipment\_Identity), or [SIM](https://en.wikipedia.org/wiki/SIM\_card) card number

### Monitoring the progress of a shipment

A [shipment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments) provides numerous data points that you can use to track a delivery's progress.

For the entire shipment, we provide you a `trackingUrl` that directs customers to a page where they can enter the `trackingNumber` provided by the `trackingCompany`.

At the shipment item level, we also give you a `trackingUrl` that directs customers to a page where they can enter the item's `trackingNumber` and monitor the delivery progress of specific products.
