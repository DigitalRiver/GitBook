---
description: >-
  Learn how to manage returns when Digital River is your designated fulfillment
  coordinator
---

# Digital River coordinated returns

In [Digital River coordinated fulfillments](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/), you can use the [Fulfillment Returns API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Returns) to [request](digital-river-coordinated-returns.md#requesting-a-fulfillment-return) and [retrieve](digital-river-coordinated-returns.md#retrieving-a-fulfillment-return) returns. After you create a [fulfillment return](digital-river-coordinated-returns.md#a-fulfillment-return), you should monitor and respond to the [events it emits](digital-river-coordinated-returns.md#listening-for-fulfillment-return-events).

## Requesting a fulfillment return

When requesting a fulfillment return, you should first [ensure the items you want to return are in the correct state](digital-river-coordinated-returns.md#ensuring-the-correct-item-state). Once you've done that, you can then [define and submit the return request](digital-river-coordinated-returns.md#defining-and-submitting-a-fulfillment-return).

### Ensuring the correct item state

Before providing customers the option to return an item, you should ensure that the item is in a [`shipped` state](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#line-item-level). Customers shouldn't be allowed to return `pending`, `backordered`, or `cancelled` items. You can obtain this information by either [retrieving the upstream fulfillment order](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#retrieving-a-fulfillment-order) or [listening for fulfillment order events](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#listening-and-responding-to-fulfillment-order-events).

{% hint style="warning" %}
You may decide you want to build your integration so that customers have the [option to cancel](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/instructing-digital-to-cancel-items.md) `pending` and `backordered` items.
{% endhint %}

### Defining and submitting a fulfillment return

When customers indicate they want to return all or part of a [fulfillment order](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#a-fulfillment-order), submit a `POST/fulfillment-returns` request that specifies the items to return and in what quantity. More specifically, you need to provide us the [identifier of the fulfillment order](digital-river-coordinated-returns.md#fulfillment-order-identifier) these items are attached to, [data on the inventory items](digital-river-coordinated-returns.md#inventory-item-data) to return, and the [identifier of the upstream order](digital-river-coordinated-returns.md#order-identifier).

#### Fulfillment order identifier

The `fulfillmentOrderId` parameter is used to specify the [identifier of the upstream fulfillment order](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#unique-identifiers) associated with this return.

#### Inventory item data

For each item you want to return, you must provide the [identifier it was assigned in the upstream fulfillment order](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#unique-identifiers) and the `quantity` of that item to return.

#### Order identifier

In the request, you should also set `upstreamId` to the [identifier of the upstream order](../../creating-and-updating-an-order.md#unique-identifier). This allows you to retrieve this identifier from the payload of a [`fulfillment_return.accepted` event](digital-river-coordinated-returns.md#return-accepted-events) and use it when [issuing refunds](../refunds/issuing-refunds.md).

### Upstream data sent in a `POST` fulfillment return request

When defining a `POST/fulfillment-returns` request, you can retrieve the required data from the following upstream [Order](../../orders/) and [Fulfillment Order](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#a-fulfillment-order) resources.

| Upstream API       | Attribute    |       | Fulfillment Returns API          |
| ------------------ | ------------ | ----- | -------------------------------- |
| Fulfillment Orders | `id`         | **➔** | `fulfillmentOrderId`             |
| Fulfillment Orders | `items[].id` | **➔** | `items[].fulfillmentOrderItemId` |
| Orders             | `id`         | **➔** | `upstreamId`                     |

## A fulfillment return

Once you've successfully submitted a `POST/fulfillment-returns` request, you get back a fulfillment return with a unique `id` which you can use to later [retrieve the fulfillment return](digital-river-coordinated-returns.md#retrieving-a-fulfillment-return).

The object provides you information on each [requested and accepted return item](digital-river-coordinated-returns.md#returned-items). A fulfillment return also contains enumerations that indicate its [state](digital-river-coordinated-returns.md#the-fulfillment-return-life-cycle) and [who initiated it](digital-river-coordinated-returns.md#return-initiator).

Once the [fulfiller approves the return](digital-river-coordinated-returns.md#return-approved-events), we also provide the [return address](digital-river-coordinated-returns.md#return-address) where the customer should ship the items.

### Returned items

The `items` array of a fulfilment return contains information on requested and accepted returns. For each item in this array, `quantity` is the number of items you requested to be returned. The `quantityAccepted` is how many items have been accepted for return by the fulfiller.

When `quantityAccepted` is less than `quantity`, then the fulfiller has not yet approved all products for return.

### The fulfillment return life cycle

A Digital River coordinated physical return has a defined lifecycle at both the [fulfillment return level](digital-river-coordinated-returns.md#fulfillment-return-level) and [line item](digital-river-coordinated-returns.md#line-item-level) level. Each stage of these lifecycles is represented by the `state` attribute.

#### Fulfillment return level

The `state` attribute at the fulfillment return level indicates where a [fulfillment return](digital-river-coordinated-returns.md#a-fulfillment-return) is in its lifecycle. The values for a successful fulfillment return (i.e., the happy path) are `created` > `pending` > `accepted`.

| (1) When the fulfillment return request...                                                           | (2) the state transitions to... |
| ---------------------------------------------------------------------------------------------------- | ------------------------------- |
| has been received by the fulfiller but they haven't approved or rejected it yet                      | `created`                       |
| has been approved by the fulfiller but the returned items haven't been received at the warehouse yet | `pending`                       |
| has been accepted by the fulfiller because the returned items have been received at the warehouse    | `accepted`                      |
| has been rejected by the fulfiller                                                                   | `rejected`                      |

#### Line item level

The `state` attribute at the item level indicates where a line item is in its return lifecycle. The values for a successfully returned line item (i.e., the happy path) are `pending` > `accepted`.

| (1) When the line item...                                                                                                               | (2) the state transitions to... |
| --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| identifier is sent in a successful`POST/fulfillment-returns` request but the product(s) is not yet approved for return by the fulfiller | `pending`                       |
| has been received by the fulfiller at the warehouse and the product(s) return is accepted                                               | `accepted`                      |
| return request is rejected by the fulfiller                                                                                             | `rejected`                      |

### Return initiator

The `type` attribute indicates who initiated the return. A `client` return is standard and is typically initiated by a customer though the storefront. A `warehouse` return is initiated when a shipment is refused.

### Return address

Once [a return request](digital-river-coordinated-returns.md#requesting-a-fulfillment-return) is approved by the fulfiller, we populate the `location` hash table. This data structure provides the address where a customer should return the products. To be notified of these approvals, you can subscribe to [`fulfillment_return.pending`](digital-river-coordinated-returns.md#return-approved-events) events.

## Monitoring and responding to fulfillment returns

Once you have successfully submitted a `POST/fulfillment-returns` request, you can determine its status by either [calling the API directly](digital-river-coordinated-returns.md#retrieving-a-fulfillment-return) or [listening for webhook events](digital-river-coordinated-returns.md#listening-for-fulfillment-return-events).

### Retrieving a fulfillment return

There are two methods in the [Fulfillment Returns API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Returns) that can be used to retrieve fulfillment returns. You can either [get a list of fulfillment returns](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listFulfillmentReturns) filtered by optional query parameters. Or you can [get an individual fulfillment return](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveFulfillmentReturns) by sending its unique identifier as a path parameter.

### Listening for fulfillment return events

You can [configure your webhooks](../../events-and-webhooks-1/webhooks/creating-a-webhook.md#step-3-create-webhooks) to listen for fulfillment return events. The `data.object` of every one of these [events](../../events-and-webhooks-1/events-1/) consists of a [fulfillment return](digital-river-coordinated-returns.md#a-fulfillment-return).

#### Return created events

When you submit a successful `POST/fulfillment-returns` request, we send you a `fulfillment_return.created` event. This indicates that your return request has been created by Digital River but not yet approved or rejected by the fulfiller.

#### Return approved events

If the fulfiller approves the return request, we send you a `fulfillment_return.pending` event. You can use this event to determine [what items can be returned](digital-river-coordinated-returns.md#returned-items) and [where they can be sent](digital-river-coordinated-returns.md#return-address) and then convey this information to the customer.

#### Return accepted events

When the fulfiller notifies us that they've received and accepted the returned products, we send you a `fulfillment_return.accepted` event. If you don't want to reimburse customers until they have returned products, your integration should wait to receive this event before [issuing refunds](../refunds/issuing-refunds.md).

#### Return rejected events

A `fulfillment_return.rejected` event indicates the fulfiller has rejected the return.
