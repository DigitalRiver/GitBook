---
description: >-
  In Digital River coordinated fulfillments, learn how to cancel fulfillment of
  physical products
---

# Cancelling a fulfillment order

In [Digital River coordinated fulfillments](./), you can use the [Fulfillment Cancellations API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Cancellations) to cancel the delivery of [inventory items](../../../product-management/skus.md#inventory-items). When you [request a fulfillment cancellation](instructing-digital-to-cancel-items.md#requesting-a-fulfillment-cancellation), you must specify the items to cancel and in what quantity.

Your integration should also be set up to [respond to fulfillment cancellation events](instructing-digital-to-cancel-items.md#responding-to-cancellation-events).

## Requesting a fulfillment cancellation

If your site allows customers to cancel purchases, before sending a [create fulfillment cancellation request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentCancellations), you should first [ensure the items you want to cancel are in the correct state](instructing-digital-to-cancel-items.md#ensuring-the-correct-item-state). Once you've done that, you can then [define and submit the cancellation request](instructing-digital-to-cancel-items.md#defining-and-submitting-a-fulfillment-cancellation).

### Ensuring the correct item state

Before you activate a cancellation option in your UI, check that the relevant `items[]` in the [fulfillment order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders) are either [`pending`](global-fulfillments.md#the-fulfillment-order-life-cycle) or [`backordered`](global-fulfillments.md#the-fulfillment-order-life-cycle) . Customers shouldn't be allowed to cancel [`shipped`](global-fulfillments.md#the-fulfillment-order-life-cycle) items. However, your integration can provide customers the option to [return shipped items](../../../order-management/returns-and-refunds-1/returns/digital-river-coordinated-returns.md).

### Defining and submitting a fulfillment cancellation request <a href="#defining-and-submitting-a-fulfillment-cancellation" id="defining-and-submitting-a-fulfillment-cancellation"></a>

When customers opt to cancel all or part of a [fulfillment order](global-fulfillments.md#a-fulfillment-order), respond to their request by defining and submitting a [`POST/fulfillment-cancellations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentOrders). The request needs to provide:

* [The fulfillment order identifier](instructing-digital-to-cancel-items.md#fulfillment-order-identifier)
* [The order identifier](instructing-digital-to-cancel-items.md#order-identifier)
* [Data on the items that the customer wants to cancel](instructing-digital-to-cancel-items.md#inventory-item-data)

#### Fulfillment order identifier

A `fulfillmentOrderId` represents the [identifier of the fulfillment order](global-fulfillments.md#unique-identifiers).

| Fulfillment order |       | POST/fulfillment-cancellations |
| ----------------- | :---: | ------------------------------ |
| `id`              | **➔** | `fulfillmentOrderId`           |

#### Order identifier

An `upstreamId` represents the [identifier of the order](../../../order-management/creating-and-updating-an-order.md#unique-identifier). We recommend you set this value for tracking purposes and to maintain data consistency.

| Order |       | POST/fulfillment-cancellations |
| ----- | :---: | ------------------------------ |
| `id`  | **➔** | `upstreamId`                   |

#### Item data <a href="#inventory-item-data" id="inventory-item-data"></a>

For each item that a customer wants to cancel, provide the [fulfillment order line item identifier](global-fulfillments.md#unique-identifiers) that we assigned it. You must also specify the `quantity` of that line item.

| Fulfillment order |       | POST/fulfillment-cancellations   |
| ----------------- | :---: | -------------------------------- |
| `items[].id`      | **➔** | `items[].fulfillmentOrderItemId` |

## A fulfillment cancellation

A successful [`POST/fulfillment-cancellations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentCancellations) returns a [fulfillment cancellation](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Cancellations).

You can use this resource to [determine the state of the cancellation](instructing-digital-to-cancel-items.md#the-fulfillment-cancellation-life-cycle). Additionally, for each item you request to cancel, we provide the [accepted quantity.](instructing-digital-to-cancel-items.md#cancelled-items)

A fulfillment cancellation also contains a unique `id`. You can use this identifier when [responding to cancellation state change events](instructing-digital-to-cancel-items.md#monitoring-and-responding-to-fulfillment-cancellations), as well as [retrieving the fulfillment cancellation](instructing-digital-to-cancel-items.md#retrieving-a-fulfillment-cancellation).

### Items accepted for cancellation <a href="#cancelled-items" id="cancelled-items"></a>

In a [fulfilment cancellation](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Cancellations), each `items[]` provides the `quantity` you specified in the `POST/fulfillment-cancellations` as well as the `quantityAccepted` by the fulfiller. If `quantityAccepted` is less than `quantity`, then the fulfiller didn't approve all the items for cancellation.

### The fulfillment cancellation life cycle

A [fulfillment cancellation](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Cancellations), as well as its `items[]`, have a defined lifecycle, each stage of which is represented by a `state`.

{% hint style="info" %}
We recommend that you [monitor and respond to fulfillment cancellation state change events](instructing-digital-to-cancel-items.md#monitoring-and-responding-to-fulfillment-cancellations).
{% endhint %}

#### Fulfillment cancellation states

A [fulfillment cancellation](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Cancellations) contains a `state`. It indicates where the resource is in its lifecycle. The values for a successful fulfillment cancellation (i.e., the happy path) are `pending` > `accepted`.

| (1) When the fulfillment cancellation...                          | (2) its `state` transitions to... |
| ----------------------------------------------------------------- | --------------------------------- |
| is created but not yet approved for cancellation by the fulfiller | `pending`                         |
| is approved for cancellation by the fulfiller                     | `accepted`                        |
| is rejected for cancellation by the fulfiller                     | `rejected`                        |

#### Line item states

Each of a [fulfillment cancellation's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Cancellations) `items[]` also contains a `state`. The `state` values of a successfully cancelled line item (i.e., the happy path) are `pending` > `accepted`.

| (1) When the line item...                             | (2) its `state` transitions to... |
| ----------------------------------------------------- | --------------------------------- |
| is not yet approved for cancellation by the fulfiller | `pending`                         |
| is approved for cancellation by the fulfiller         | `accepted`                        |
| is rejected for cancellation by the fulfiller         | `rejected`                        |

## Handling fulfillment cancellation state change events <a href="#monitoring-and-responding-to-fulfillment-cancellations" id="monitoring-and-responding-to-fulfillment-cancellations"></a>

Your integration should be capable of [responding to fulfillment cancellation state change events](instructing-digital-to-cancel-items.md#responding-to-cancellation-events). You can also determine a fulfillment cancellation's `state` by [calling the API directly](instructing-digital-to-cancel-items.md#retrieving-a-fulfillment-cancellation).

### Responding to cancellation events

You can [configure your webhooks](../../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md#step-3-create-webhooks) to listen for fulfillment cancellation created, approved, and rejected events. Each [event's](../../../order-management/events-and-webhooks-1/events-1/) `data.object` consists of a [fulfillment cancellation](instructing-digital-to-cancel-items.md#a-fulfillment-cancellation).

#### Fulfillment cancellation created events

When a `POST/fulfillment-cancellations` request is successfully submitted, we create a `fulfillment_cancellation.created` [event](../../../order-management/events-and-webhooks-1/events-1/). This event indicates that your cancellation request has been received by Digital River but not yet approved or rejected by the fulfiller.

#### Fulfillment cancellation approved events

If the fulfiller approves a cancellation request, we create a `fulfillment_cancellation.accepted` event that provides the [quantity of items they accepted for cancellation](instructing-digital-to-cancel-items.md#cancelled-items).

In [Digital River coordinated fulfillments](./) that use the [distributed model](./#distributed-model), you should respond to each fulfillment cancellation approved event by submitting a payment cancellation request through the [Fulfillments API](instructing-digital-to-cancel-items.md#requesting-a-fulfillment-cancellation).

If you're using the [orchestrated model](./#orchestrated-model), we listen for fulfillment cancellation approved events and submit the appropriate payment cancellation request.

For more details, refer to [Capturing and cancelling payment charges](../../../order-management/informing-digital-river-of-a-fulfillment.md).

#### Fulfillment cancellation rejected events

A `fulfillment_cancellation.rejected` event indicates that the fulfiller has declined the cancellation request.

We recommend you respond to these events by notifying customers (typically through email and their order management page) that the cancellation request has been rejected. In the notification, you can provide customers instructions on how to [return physical products](../../../order-management/returns-and-refunds-1/returns/digital-river-coordinated-returns.md) and/or how to [request refunds](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md).

### Retrieving a fulfillment cancellation

There are two requests that can be used to retrieve [fulfillment cancellations](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Cancellations):

* You can [get a specific fulfillment cancellation](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveFulfillmentCancellations) by sending its unique identifier.
* You can [get a list of fulfillment cancellations](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listFulfillmentCancellations) filtered by optional query parameters.
